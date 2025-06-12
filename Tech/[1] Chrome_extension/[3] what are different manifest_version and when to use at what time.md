In a Chrome Extension's `manifest.json`, the `manifest_version` defines the **version of the extension manifest specification** your extension follows. It affects **what APIs are available**, **how permissions are declared**, and **how features behave**.

---

## 🔢 The Manifest Versions

### ✅ 1. **Manifest V3 (Recommended & Required for New Extensions)**

- **`manifest_version: 3`**
    
- **Current standard** (as of 2025)
    
- All new extensions **must** use this
    
- MV2 is now deprecated and disabled in Chrome
    

#### 🔧 Key Features:

- **Service Worker** instead of background pages
    
- New **`host_permissions`** field
    
- `background.scripts` replaced by `background.service_worker`
    
- `declarativeNetRequest` replaces `webRequest` (for blocking requests)
    
- Better **performance** and **privacy/security**
    

#### Example:

```json
{
  "manifest_version": 3,
  "name": "My Extension",
  "version": "1.0",
  "permissions": ["storage"],
  "host_permissions": ["https://*.example.com/*"],
  "background": {
    "service_worker": "background.js"
  }
}
```

---

### ❌ 2. **Manifest V2 (Deprecated)**

- **`manifest_version: 2`**
    
- **No longer supported** in Chrome Web Store as of **January 2024**
    
- Was popular for years
    
- Uses `background.pages`, has synchronous APIs
    

#### Limitations:

- Slower and less secure
    
- Not allowed for **new** extension uploads
    
- Existing MV2 extensions are disabled in Chrome (unless in Enterprise context)
    

#### Example (Legacy only):

```json
{
  "manifest_version": 2,
  "name": "Old Extension",
  "version": "1.0",
  "background": {
    "scripts": ["background.js"]
  },
  "permissions": ["tabs", "https://*.example.com/"]
}
```

---

### ❌ 3. **Manifest V1 (Obsolete)**

- **Deprecated years ago**, before MV2
    
- Had major security and performance flaws
    
- No longer relevant
    

---

## 🧭 Which One Should You Use?

|**Use Case**|**Recommended Version**|
|---|---|
|New Chrome Extension|✅ Manifest V3|
|Publishing to Chrome Web Store|✅ Manifest V3|
|Maintaining old extension (temporary)|Only if you're in an enterprise with MV2 support enabled|
|Just experimenting locally|✅ Use MV3 — MV2 is unsupported in most environments|

---

### 🛑 Warning

- As of 2024, **Chrome Web Store has fully phased out MV2**.
    
- MV2 extensions can no longer be installed or updated by normal users.
    

---

If you’re starting fresh, **always use Manifest V3**. I can help you convert an MV2 manifest to MV3 if needed — just share it!