The `chrome.webRequest` API in Chrome extensions allows you to **observe and manipulate network requests** (like HTTP requests/responses) made by the browser.

This is a **powerful API**, and depending on what you want to do (log, block, redirect, modify headers, etc.), you’ll use different **webRequest events**.

---

## 🔌 List of `chrome.webRequest` Events

Here are the main events in the `chrome.webRequest` API:

|**Event**|**When It Fires**|**Use Case Example**|
|---|---|---|
|`onBeforeRequest`|Before a request is sent|Cancel or redirect a request|
|`onBeforeSendHeaders`|Before sending request headers|Modify request headers|
|`onSendHeaders`|Right after sending request headers|Observe headers actually sent|
|`onHeadersReceived`|After response headers are received|Modify response headers|
|`onAuthRequired`|When a request requires authentication|Provide credentials programmatically|
|`onResponseStarted`|When the first byte of response is received|Log responses|
|`onBeforeRedirect`|When a response is about to redirect|Track redirects|
|`onCompleted`|When the request is fully completed|Log completed requests|
|`onErrorOccurred`|When a request fails (e.g., timeout, DNS failure)|Log or retry failed requests|

---

## 🧪 Example Use Cases

### ✅ Log All Network Requests

```js
chrome.webRequest.onCompleted.addListener(
  (details) => {
    console.log("Request completed:", details);
  },
  { urls: ["<all_urls>"] }
);
```

---

### 🚫 Block Requests

```js
chrome.webRequest.onBeforeRequest.addListener(
  (details) => {
    return { cancel: true };
  },
  { urls: ["*://ads.example.com/*"] },
  ["blocking"]
);
```

---

### ✏️ Modify Headers (MV3 requires `declarativeNetRequest`)

In Manifest V3, **you can no longer modify request headers using `webRequest`** with `"blocking"` — instead, use `declarativeNetRequest`.

**BUT**, if you still use it for observation (logging), you can use:

```js
chrome.webRequest.onBeforeSendHeaders.addListener(
  (details) => {
    console.log("Headers:", details.requestHeaders);
  },
  { urls: ["<all_urls>"] },
  ["requestHeaders"]
);
```

---

## 🧠 Important Notes

### 🔐 Required Permissions

- `"webRequest"` — to observe requests
    
- `"webRequestBlocking"` — to block or modify
    
- `"host_permissions"` — to specify which URLs you're monitoring
    

```json
"permissions": ["webRequest", "webRequestBlocking"],
"host_permissions": ["<all_urls>"]
```

---

### ⚠️ Manifest V3 Restrictions

In Manifest V3:

- You **cannot block or modify** headers using `webRequest` unless in **Enterprise mode**.
    
- Use `declarativeNetRequest` for blocking or rewriting.
    
- You **can still observe** requests with `webRequest` (e.g., for logging).
    

---

## 🛠️ Debugging Tip

Use the **DevTools Network tab** or `chrome://extensions → Inspect views` to see what your listeners are logging or blocking.

---
