In a Chrome extension, `chrome.storage` is used to **store data persistently** — like settings, logs, tokens, etc.

There are **three main types** of storage areas provided by the `chrome.storage` API:

---

## 📦 1. `chrome.storage.local`

### ✅ Most Common — Stores Data Locally

- Data is saved **locally on the user's device**.
    
- Persistent and does **not sync** across devices.
    
- Recommended for:
    
    - Logs
        
    - Cache
        
    - Large or temporary data
        

### 📌 Limits:

- **Quota**: 5MB per extension (approx.)
    
- Data is stored as JSON (objects only, not functions or class instances)
    

### 🧪 Example:

```js
chrome.storage.local.set({ theme: "dark" });
chrome.storage.local.get(["theme"], (result) => {
  console.log("Theme:", result.theme);
});
```

---

## ☁️ 2. `chrome.storage.sync`

### ✅ Automatically Syncs Across Chrome Profiles

- Data is stored in the **user's Google account** and syncs across Chrome browsers.
    
- Good for:
    
    - Extension settings
        
    - Preferences
        
    - Lightweight data
        

### ⚠️ Limitations:

- Quota: 100KB total; max 8KB per item; 512 items
    
- Subject to **sync delays**
    
- Not always available (e.g., Incognito, signed-out profiles)
    

### 🧪 Example:

```js
chrome.storage.sync.set({ language: "en" });
chrome.storage.sync.get(["language"], (result) => {
  console.log("Language:", result.language);
});
```

---

## 🔒 3. `chrome.storage.session` (Manifest V3 only)

### ✅ Temporary, In-Memory Storage (Fast, Ephemeral)

- Lives in **memory only** (not written to disk)
    
- Data is lost when the extension is unloaded (e.g., browser restart)
    
- Useful for:
    
    - Caching
        
    - Temporary states
        
    - Reducing disk I/O
        

### 🧪 Example:

```js
chrome.storage.session.set({ tempData: "123" });
chrome.storage.session.get(["tempData"], (result) => {
  console.log("Temp:", result.tempData);
});
```

---

## ✅ Quick Comparison Table

|Feature|`local`|`sync`|`session`|
|---|---|---|---|
|Persistent|✅ Yes|✅ Yes|❌ No|
|Syncs across devices|❌ No|✅ Yes|❌ No|
|Max storage|~5MB|~100KB|Memory-limited|
|Use case|Logs, cache|Settings|Temporary state|
|Available in MV2|✅ Yes|✅ Yes|❌ No|
|Available in MV3|✅ Yes|✅ Yes|✅ Yes|

---

## 🔄 Events You Can Use

All three support `onChanged`:

```js
chrome.storage.onChanged.addListener((changes, areaName) => {
  console.log(`Changes in ${areaName}:`, changes);
});
```

---

## 🔐 Security Tip

- Don't store sensitive info like API keys or tokens unless needed, and avoid sync for that.
    
- Always validate and sanitize data before use.
    

---
