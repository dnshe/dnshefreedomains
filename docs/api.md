# DNSHE Free Domain API Documentation (v2.0)

## 📌 Overview

* **Base URL:**
  `https://api005.dnshe.com/index.php?m=domain_hub`
* **Authentication:** API Key + API Secret
* **Response Format:** JSON
* **Rate Limit:** 60 requests/minute (configurable)

---

## 🔐 Authentication

### Get API Credentials

1. Log in to DNSHE client area
2. Go to **My Domain Management**
3. Click **API Management** in sidebar
4. Create a new API Key

---

### Authentication Method

#### ✅ Recommended: HTTP Headers

```bash
curl -X GET "https://api005.dnshe.com/index.php?m=domain_hub&endpoint=subdomains&action=list" \
  -H "X-API-Key: cfsd_xxxxxxxxxx" \
  -H "X-API-Secret: yyyyyyyyyyyy"
```

#### ❌ Deprecated: URL Parameters

> Passing `api_key` and `api_secret` via URL or request body is no longer supported for security reasons.

---

## 📦 API Endpoints

---

## 1️⃣ Subdomain Management

### 1.1 List Subdomains

* **Endpoint:** `subdomains`
* **Action:** `list`
* **Method:** `GET`

```bash
curl -X GET "https://api005.dnshe.com/index.php?m=domain_hub&endpoint=subdomains&action=list" \
  -H "X-API-Key: cfsd_xxxxxxxxxx" \
  -H "X-API-Secret: yyyyyyyyyyyy"
```

#### Response Example

```json
{
  "success": true,
  "count": 2,
  "subdomains": [
    {
      "id": 1,
      "subdomain": "test",
      "rootdomain": "example.com",
      "full_domain": "test.example.com",
      "status": "active"
    }
  ]
}
```

---

### 1.2 Register Subdomain

```bash
curl -X POST "https://api005.dnshe.com/index.php?m=domain_hub&endpoint=subdomains&action=register" \
  -H "X-API-Key: cfsd_xxxxxxxxxx" \
  -H "X-API-Secret: yyyyyyyyyyyy" \
  -H "Content-Type: application/json" \
  -d '{
    "subdomain": "myapp",
    "rootdomain": "example.com"
  }'
```

---

### 1.3 Get Subdomain Details

```bash
curl -X GET "https://api005.dnshe.com/index.php?m=domain_hub&endpoint=subdomains&action=get&subdomain_id=1" \
  -H "X-API-Key: cfsd_xxxxxxxxxx" \
  -H "X-API-Secret: yyyyyyyyyyyy"
```

---

### 1.4 Delete Subdomain

```bash
curl -X POST "https://api005.dnshe.com/index.php?m=domain_hub&endpoint=subdomains&action=delete" \
  -H "X-API-Key: cfsd_xxxxxxxxxx" \
  -H "X-API-Secret: yyyyyyyyyyyy" \
  -H "Content-Type: application/json" \
  -d '{"subdomain_id": 1}'
```

---

### 1.5 Renew Subdomain

```bash
curl -X POST "https://api005.dnshe.com/index.php?m=domain_hub&endpoint=subdomains&action=renew" \
  -H "X-API-Key: cfsd_xxxxxxxxxx" \
  -H "X-API-Secret: yyyyyyyyyyyy" \
  -H "Content-Type: application/json" \
  -d '{"subdomain_id": 3}'
```

---

## 2️⃣ DNS Records Management

### List DNS Records

```bash
curl -X GET "https://api005.dnshe.com/index.php?m=domain_hub&endpoint=dns_records&action=list&subdomain_id=1" \
  -H "X-API-Key: cfsd_xxxxxxxxxx" \
  -H "X-API-Secret: yyyyyyyyyyyy"
```

---

### Create DNS Record

```bash
curl -X POST "https://api005.dnshe.com/index.php?m=domain_hub&endpoint=dns_records&action=create" \
  -H "X-API-Key: cfsd_xxxxxxxxxx" \
  -H "X-API-Secret: yyyyyyyyyyyy" \
  -H "Content-Type: application/json" \
  -d '{
    "subdomain_id": 1,
    "type": "A",
    "content": "192.168.1.100"
  }'
```

---

## 3️⃣ API Key Management

### List API Keys

```bash
curl -X GET "https://api005.dnshe.com/index.php?m=domain_hub&endpoint=keys&action=list" \
  -H "X-API-Key: cfsd_xxxxxxxxxx" \
  -H "X-API-Secret: yyyyyyyyyyyy"
```

---

## 4️⃣ Quota

```bash
curl -X GET "https://api005.dnshe.com/index.php?m=domain_hub&endpoint=quota" \
  -H "X-API-Key: cfsd_xxxxxxxxxx" \
  -H "X-API-Secret: yyyyyyyyyyyy"
```

---

## 5️⃣ WHOIS Lookup (Public API)

```bash
curl -X GET "https://api005.dnshe.com/index.php?m=domain_hub&endpoint=whois&domain=foo.example.com"
```

---

## ❗ Error Format

```json
{
  "success": false,
  "error_code": "auth_invalid_credentials",
  "message": "Invalid API key"
}
```

---

## 🚦 Rate Limiting

```json
{
  "error_code": "rate_limit_exceeded",
  "details": {
    "limit": 60,
    "remaining": 0
  }
}
```

---

## 🔐 Security Best Practices

* Store API credentials in environment variables
* Enable IP whitelist for production keys
* Rotate API keys regularly
* Always use HTTPS

---

## ❓ FAQ

**Q: Lost API Secret?**
A: Use `regenerate` to create a new one

**Q: Batch operations supported?**
A: Not supported in current version

---

## 📝 Changelog

### v2.0 (2026-04-25)

* 🚀 Official release of v2.0
* 🔧 Optimized API command structure
* ✨ Added new API capabilities
* ⚡ Improved pagination & query performance
* 🛡️ Enhanced error handling & security

---

### v1.0 (2025-10-19)

* 🎉 Initial release
* Subdomain management
* DNS record management
* API key management
* Quota support
* Rate limiting
