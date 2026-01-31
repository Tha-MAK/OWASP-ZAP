## OWASP ZAP Web Security Testing Lab

**Target:** [http://172.17.0.2/dvwa](http://172.17.0.2/dvwa)

**Tool:** OWASP ZAP

**Environment:** DVWA hosted on a local Docker network (172.17.0.2) 🐳

---

## 1) Objective 🎯

This exercise aimed to run a complete vulnerability scan against **DVWA** website using **OWASP Zed Attack Proxy (ZAP)**, identify security gaps, and document the results. 

---

## 2) Methodology & Workflow 🔍

### Step 1: Environment setup 🧪

* DVWA was verified as reachable at `http://172.17.0.2/dvwa/`.
* OWASP ZAP was started.

### Step 2: Target configuration ⚙️

* In the **URL to Attack** field, I used `172.17.0.2/dvwa`.
* The application was manually browsed to build the site map and improve scan coverage.

### Step 3: Spider crawl 🕷️

* ZAP uses a web spider to crawl the URL to identify the resources that are available there.
* It then will apply vulnerability scans to each resource.

### Step 4: Active scanning 🚦

* A full **Automated Scan** was executed against the DVWA target.
* ZAP tested input vectors for common web issues, including injection risks, configuration weaknesses, and missing defensive headers.

### Step 5: Analysis and validation 🧾

* Alerts were reviewed in the **Alerts** tab.
* Located the **Remote Code Execution – CVE-2012-1823** alert.

---

## 3) Key Findings ⚠️

### High-risk issues 🔥

**Remote Code Execution (RCE) – CVE-2012-1823**

* **Risk level:** High
* **Confidence:** Medium
* **Affected URL:** `http://172.17.0.2/dvwa/index.php`
* **Impact:** If exploited successfully, these issues can lead to full compromise of the server.

These findings suggest insufficient security hardening and defensive configuration across the application.

---

## 4) Remediation Recommendations 🔒✅

### Remote Code Execution (CVE-2012-1823)

* Upgrade PHP to a supported and secure version.
* Disable PHP CGI if it is not required.
* Harden PHP settings such as `allow_url_include` and `auto_prepend_file`.
* Enforce strict server-side input validation and filtering.

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
