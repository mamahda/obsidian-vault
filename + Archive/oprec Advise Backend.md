# DAST Tool Prototype — Architecture & API

## Architecture Overview

Proyek ini menggunakan pola **Service Repository Pattern** dengan arsitektur berlapis:

```
HTTP Request
     ↓
Controller   → validasi input, return JSON response
     ↓
Service      → business logic, orkestrasi proses
     ↓
Repository   → abstraksi query database
     ↓
Model        → Eloquent ORM
     ↓
Database (SQLite)
```

### Kenapa pakai pola ini?

- **Controller tetap tipis** — tidak ada logika bisnis di sini, cukup terima request dan kembalikan response
- **Service bisa ditest secara terisolasi** — bisa mock Repository-nya tanpa perlu koneksi database sungguhan
- **Repository bisa diganti** — misal SQLite → PostgreSQL, cukup ubah implementasi Repository tanpa sentuh Service
- **DummyScannerService bisa diganti** — begitu integrasi OWASP ZAP siap, tinggal swap implementasinya via Service Container Laravel, Service layer tidak perlu diubah

---

## Project Structure

```
app/
├── Http/
│   └── Controllers/
│	  	  ├── Requests/
│       │   └── StoreScanRequest.php
│       ├── ScanController.php
│       ├── VulnerabilityController.php
│       └── DashboardController.php
│
├── Services/
│   ├── ScanService.php
│   ├── DummyScannerService.php
│   └── DashboardService.php
├── Repositories/
│   ├── ScanRepository.php
│   └── VulnerabilityRepository.php
├── Models/
│   ├── Scan.php
│   └── Vulnerability.php
└── Enums/
    ├── ScanStatus.php
    └── Severity.php
```

---

## Enums

### `ScanStatus`

```php
enum ScanStatus: string {
    case PENDING   = 'pending';
    case RUNNING   = 'running';
    case COMPLETED = 'completed';
}
```

### `Severity`

```php
enum Severity: string {
    case CRITICAL = 'critical';
    case HIGH     = 'high';
    case MEDIUM   = 'medium';
    case LOW      = 'low';
    case INFO     = 'info';
}
```

Keduanya di-cast langsung di Eloquent Model, jadi nilai yang masuk ke database selalu valid dan tidak perlu validasi manual berulang di tiap layer.

---

## API Reference

Base URL: `/api`  
Response format: JSON

---

### Scans

#### `POST /scans`

Mendaftarkan URL target baru untuk dipindai.

**Request body:**

```json
{
    "target_url": "https://example.com"
}
```

**Response `201`:**

```json
{
    "data": {
        "id": 1,
        "target_url": "https://example.com",
        "status": "pending",
        "created_at": "2026-06-30T10:00:00.000000Z",
        "updated_at": "2026-06-30T10:00:00.000000Z"
    }
}
```

---

#### `GET /scans`

Mengambil semua target scan yang terdaftar.

**Response `200`:**

```json
{
    "data": [
        {
            "id": 1,
            "target_url": "https://example.com",
            "status": "completed",
            "created_at": "...",
            "updated_at": "..."
        }
    ]
}
```

---

#### `GET /scans/{id}`

Detail satu scan beserta hasil kerentanannya.

**Response `200`:**

```json
{
    "data": {
        "id": 1,
        "target_url": "https://example.com",
        "status": "completed",
        "vulnerabilities": [
            {
                "id": 1,
                "type": "SQL Injection",
                "severity": "critical",
                "description": "..."
            }
        ]
    }
}
```

---

#### `POST /scans/{id}/start`

Memulai proses simulasi scan terhadap target.

State machine status: `pending` → `running` → `completed`

Jika status bukan `pending`, endpoint ini akan menolak request (409 Conflict).

**Response `200`:**

```json
{
    "data": {
        "id": 1,
        "status": "completed",
        "total_vulnerabilities_found": 4,
        "vulnerabilities": [
            { "type": "SQL Injection",          "severity": "critical" },
            { "type": "Cross Site Scripting",   "severity": "high"     },
            { "type": "Security Misconfiguration", "severity": "medium" },
            { "type": "Missing CSP Header",     "severity": "low"      }
        ]
    }
}
```

---

### Vulnerabilities

#### `GET /vulnerabilities`

Mengambil semua kerentanan dari semua scan.

**Query params:**

|Param|Tipe|Contoh|Keterangan|
|---|---|---|---|
|`severity`|`string`|`critical`|Filter berdasarkan tingkat severity|

**Contoh:** `GET /vulnerabilities?severity=critical`

**Response `200`:**

```json
{
    "data": [
        {
            "id": 1,
            "scan_id": 1,
            "type": "SQL Injection",
            "severity": "critical",
            "description": "..."
        }
    ]
}
```

---

### Dashboard

#### `GET /dashboard`

Statistik agregat dari seluruh data scan dan kerentanan. Semua agregasi dilakukan di level database via `GROUP BY`, bukan di PHP.

**Response `200`:**

```json
{
    "data": {
        "total_scans": 5,
        "total_vulnerabilities": 18,
        "count_by_severity": {
            "critical": 3,
            "high":     6,
            "medium":   5,
            "low":      3,
            "info":     1
        },
        "count_by_status": {
            "pending":   1,
            "running":   0,
            "completed": 4
        }
    }
}
```

---

## Scan Execution Flow

```
POST /scans/{id}/start
        ↓
ScanController@start
        ↓
ScanService->startScan($id)
        ↓
Validasi status == pending  ──[gagal]──→  409 Conflict
        ↓ [lolos]
Update status → RUNNING
        ↓
DummyScannerService->generateFindings($scan)
        ↓
VulnerabilityRepository->bulkInsert($findings)
        ↓
Update status → COMPLETED
        ↓
Return response JSON
```

## Future: Ganti DummyScannerService dengan OWASP ZAP

Karena `ScanService` bergantung ke interface, bukan ke kelas konkret, penggantiannya cukup:

1. Buat `ZapScannerService` yang implement `ScannerEngineInterface`
2. Bind di `AppServiceProvider` berdasarkan config/env:

```php
$this->app->bind(ScannerEngineInterface::class, fn() =>
    config('scanner.engine') === 'zap'
        ? new ZapScannerService()
        : new DummyScannerService()
);
```

3. `ScanController` dan `ScanService` tidak perlu diubah sama sekali.