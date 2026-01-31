## OWASP ZAP Full Web App Scan Report (DVWA) 

**Target:** [http://172.17.0.2/dvwa/index.php](http://172.17.0.2/dvwa/index.php)
**Tool:** OWASP ZAP 2.13.0
**Environment:** DVWA hosted on a local Docker network (172.17.0.2) 🐳

---

## 1) Objective 🎯

This exercise aimed to run a complete vulnerability scan against **Damn Vulnerable Web Application (DVWA)** using **OWASP ZAP**, identify security gaps, and document the results along with practical remediation guidance. 

---

## 2) Methodology and Workflow 🔍

### Step 1: Environment setup 🧪

* DVWA was deployed and verified as reachable at `http://172.17.0.2/dvwa/index.php`.
* OWASP ZAP was started in **Standard Mode**.
* Browser traffic was proxied through ZAP using its built-in proxy.

### Step 2: Target configuration ⚙️

* The target URL was added to the **Sites** tree in ZAP.
* The application was manually browsed to build the site map and improve scan coverage.

### Step 3: Spidering (crawling) 🕷️

* ZAP Spider was used to automatically discover additional pages, parameters, and resources.
* Spider results were reviewed to confirm sufficient coverage across the application.

### Step 4: Active scanning 🚦

* A full **Active Scan** was executed against the DVWA target.
* ZAP tested input vectors for common web issues, including injection risks, configuration weaknesses, and missing defensive headers.

### Step 5: Analysis and validation 🧾

* Alerts were reviewed in the **Alerts** tab.
* Findings were assessed based on severity, confidence, and potential exploitability.

---

## 3) Key Findings ⚠️

### 3.1 High-risk issues 🔥

1. **Remote Code Execution (RCE) – CVE-2012-1823**
2. **Source Code Disclosure – CVE-2012-1823**

* **Risk level:** High
* **Confidence:** Medium
* **Affected URL:** `http://172.17.0.2/dvwa/index.php`
* **Impact:** If exploited successfully, these issues can lead to full compromise of the server.

---

### 3.2 Medium and low-risk issues 🧩

* Missing anti-CSRF protections (no anti-CSRF tokens)
* Content Security Policy (CSP) header not configured
* Missing anti-clickjacking protection (`X-Frame-Options`)
* Cookies missing `HttpOnly`
* Cookies missing `SameSite`
* Server version details exposed through HTTP headers
* Missing `X-Content-Type-Options`
* Authentication request detected
* Session management response detected
* Hidden files discovered

Overall, these findings suggest insufficient security hardening and defensive configuration across the application.

---

## 4) Remediation Recommendations 🔒✅

### Remote Code Execution (CVE-2012-1823)

* Upgrade PHP to a supported and secure version.
* Disable PHP CGI if it is not required.
* Harden PHP settings such as `allow_url_include` and `auto_prepend_file`.
* Enforce strict server-side input validation and filtering.

### Security headers hardening 🛡️

Implement and maintain these headers:

* `Content-Security-Policy`
* `X-Frame-Options`
* `X-Content-Type-Options`

Also, regularly validate header posture using automated checks.

### CSRF protection 🔐

* Add CSRF tokens to all state-changing requests.
* Validate CSRF tokens server-side for every relevant action.

### Cookie security 🍪

Set cookies with secure attributes:

* `HttpOnly`
* `Secure`
* `SameSite=Strict` (or `Lax`, depending on business needs)

### General hardening 🧱

* Remove unnecessary files/directories and block access to sensitive paths.
* Reduce information leakage by disabling verbose server banners.
* Run vulnerability scans and periodic penetration tests as part of routine security assurance.

---

## 5) Conclusion 🧠

This scan demonstrates how outdated components and weak configurations can create serious exposure, including critical exploitation paths. OWASP ZAP was effective at identifying both high-impact vulnerabilities and baseline security hygiene gaps. Continuous patching, validation, and secure-by-default configuration are key to maintaining a resilient web application. ✅

---

## 6) Disclaimer 📌

This assessment was performed on DVWA, an intentionally vulnerable application, strictly for educational and ethical cybersecurity practice.
