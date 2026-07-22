# Room: Web Application Basics - TryHackMe

This folder documents my notes from the **Web Application Basics** room — the opening room of the **Web Hacking** module (Module 8) on TryHackMe. It establishes the foundational vocabulary every web pentester needs: URLs, HTTP, headers, status codes, and the front-end/back-end split.

## 🎯 Learning Objectives

*   Break down the anatomy of a **URL**.
*   Understand the structure of **HTTP requests and responses**.
*   Read common **HTTP methods, status codes, and headers**.
*   Distinguish **front end** from **back end** and use browser DevTools.

---

## 🔗 1. Anatomy of a URL

A URL is more than an address — each part has a role:

```
  https://user:pass@www.example.com:443/path/to/page?search=query#section
  └─┬─┘   └───┬───┘ └──────┬───────┘└┬┘└────┬─────┘└─────┬──────┘└──┬───┘
  scheme   userinfo       host      port    path      query string  fragment
```

*   **Scheme:** protocol used (`http` / `https`).
*   **Host:** domain or IP of the server.
*   **Port:** entry point (80 for HTTP, 443 for HTTPS by default).
*   **Path:** location of the resource on the server.
*   **Query string:** parameters passed to the page (`?key=value`).
*   **Fragment:** in-page anchor, handled client-side only.

---

## 📨 2. HTTP Requests & Responses

Every interaction is a request/response pair.

```http
# --- Example request ---
GET /index.html HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0
Accept: text/html
Cookie: session=abc123
```

```http
# --- Example response ---
HTTP/1.1 200 OK
Content-Type: text/html
Set-Cookie: session=xyz789
Server: nginx

<html>...</html>
```

### Common Methods
*   **GET** — retrieve data.
*   **POST** — submit data (forms, logins).
*   **PUT** — create/replace a resource.
*   **DELETE** — remove a resource.

### Status Code Families
*   **1xx** — Informational
*   **2xx** — Success (e.g. `200 OK`, `201 Created`)
*   **3xx** — Redirection (e.g. `301`, `302`)
*   **4xx** — Client error (e.g. `401 Unauthorized`, `403 Forbidden`, `404 Not Found`)
*   **5xx** — Server error (e.g. `500 Internal Server Error`)

---

## 🧩 3. Headers Worth Knowing

*   **Request:** `Host`, `User-Agent`, `Referer`, `Cookie`, `Content-Type`, `Authorization`.
*   **Response:** `Set-Cookie`, `Content-Type`, `Server`, `Location`, `Cache-Control`.

Headers are a rich source of information during recon — the `Server` header can leak the tech stack, and cookies reveal how sessions are handled.

---

## 🖥️ 4. Front End vs Back End & Tooling

*   **Front end:** what runs in the browser — HTML (structure), CSS (styling), JavaScript (behaviour). Fully visible and inspectable by the client.
*   **Back end:** server-side logic, databases, and APIs the user never sees directly.

```bash
# Inspect requests/responses from the command line
curl -v http://<TARGET_IP>          # verbose: see headers
curl -X POST -d "user=admin" http://<TARGET_IP>/login
```

Browser **DevTools** (Elements + Network tab) let me inspect the DOM, replay requests, and read exactly what the server sends back.

---

## 🧠 Lessons Learned

*   The front end is fully client-controlled — anything enforced only in the browser (hidden fields, disabled buttons, JS validation) can be bypassed. Real security lives in the back end.
*   Reading HTTP status codes and headers fluently is the baseline skill for everything that follows in web hacking (enumeration, auth bypass, injection).
*   `curl` and DevTools are the two tools I'll reach for constantly — one for scripting requests, one for interactive inspection.

---
*Disclaimer: All activities were performed legally within TryHackMe's sandboxed lab environment for educational purposes.*
