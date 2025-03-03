---
slug: "/secure-storage-api-key"
title: "Securely Storing and Using API Keys: A Practical Guide"
description: "Lets interact with your Javascript robots"
pubDate: "2025-03-03"
hero: "/images/posts/secure-keys/secure-keys.jpg"
tags: ["frontend", "backend", "security"]
layout: "../../layouts/BlogPostLayout.astro"
---

In this article, I'll discuss a better approach to storing and using API keys in your web applications. API keys are essentially the passwords to various services your application might use, so keeping them secure is critically important. Unfortunately, many common approaches have significant vulnerabilities.

## Common Vulnerabilities in API Key Storage

Before diving into the solution, let's examine three common but problematic ways developers often handle API keys.

### 1. Saving Keys Directly to a Database

This approach might seem secure at first glance but comes with several risks:

Accidental exposure through version control if you forget to ignore environment files
Your database provider could experience a security breach
Anyone with database access can see keys in plain text

### 2. Storing in Local Storage

Browser local storage is convenient but extremely vulnerable:

Malicious Chrome extensions can scrape and steal your keys
Any JavaScript running on your site can access local storage
Cross-site scripting (XSS) attacks can extract this information

### 3. Backend-Only Storage

While keeping keys on the backend is better, there are still issues:

If you're storing keys in plain text, a server breach means immediate exposure
Even encrypted storage has risks - if your encryption key is compromised, so are all your API keys

The fundamental problem with all these approaches is that they typically represent single points of failure - if one system is compromised, your API keys are exposed.

## A More Secure Solution: Split Storage

Here's a more robust approach that eliminates single points of failure:

1. Accept the user's API key on your frontend
1. Generate a unique encryption key
1. Encrypt the API key with this encryption key
1. Store the encrypted API key locally (client-side)
1. Store only the encryption key in your database (server-side)
1. When needed, retrieve both pieces and decrypt the API key for use

This approach is significantly safer because:

Only the encrypted version of the API key is available on the frontend
Only the encryption key (which is useless by itself) is stored in your database
An attacker would need to compromise both your frontend application AND your database to steal usable API keys

### Implementation Example

Let's look at how you might implement this in a JavaScript application:

```javascript
// On your frontend when user enters their API key
async function securelyStoreApiKey(apiKey) {
  // Generate a random encryption key
  const encryptionKey = generateRandomKey(32) // 256 bits

  // Encrypt the API key
  const encryptedApiKey = await encryptApiKey(apiKey, encryptionKey)

  // Store encrypted API key locally
  localStorage.setItem("encryptedApiKey", encryptedApiKey)

  // Send encryption key to backend
  await fetch("/store-encryption-key", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ encryptionKey, userId: currentUser.id }),
  })
}

// When you need to use the API key
async function getDecryptedApiKey() {
  // Get encrypted API key from local storage
  const encryptedApiKey = localStorage.getItem("encryptedApiKey")

  // Get encryption key from backend
  const response = await fetch("/get-encryption-key")
  const { encryptionKey } = await response.json()

  // Decrypt and use the API key
  const apiKey = await decryptApiKey(encryptedApiKey, encryptionKey)
  return apiKey
}
```

The actual encryption/decryption functions would use the Web Crypto API or a trusted library.

### Why This Works

The beauty of this approach is that neither storage location contains enough information to compromise the API key. An attacker would need to:

Access the user's local storage to get the encrypted API key
Breach your database to get the encryption key
Connect these two pieces of information to the same user

This dramatically raises the bar for potential attackers and removes single points of failure from your security architecture.

### Conclusion

While no security solution is perfect, this split-storage approach significantly improves API key security compared to common alternatives. By dividing the sensitive information across different systems, you create a much more robust security model that can withstand compromises of individual components.
Remember that good security is about layers of protection - this approach adds an important layer that many applications are missing.

# Thanks for reading 🙏

If there is anything I have missed, or if there is a better way to do something then please let me know.
