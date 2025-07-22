# VulnScannerPro_Full
📘 GitHub README (Professional English Version)

# VulnScannerPro

**VulnScannerPro** is a modular, multi-threaded vulnerability assessment tool written in Java. It is designed to identify common web vulnerabilities by analyzing HTTP responses, headers, and version signatures. The tool is engineered with scalability and extensibility in mind — allowing security researchers and developers to easily build upon its architecture.

---

## 🧠 Architecture Overview

VulnScannerPro uses a plugin-style architecture where each scanner is a self-contained Java module. The core engine (`ScannerEngine`) handles thread management, while each module is responsible for a specific detection task. Common HTTP logic is centralized in the `HttpUtils` utility class for consistency and reuse.

VulnScannerPro/ ├── Main.java                 # CLI entry point ├── core/ │   └── ScannerEngine.java   # Coordinates scanner execution ├── modules/                 # Each file is a dedicated scanner │   ├── HttpHeaderScanner.java │   ├── CVEChecker.java ├── utils/ │   └── HttpUtils.java       # Shared HTTP logic ├── data/ │   └── cve_db.json          # Custom JSON CVE signature store

---

## ✨ Key Features

- **Multi-threaded scanning** – all modules run in parallel for high performance.
- **CVE-based signature matching** – identifies known vulnerabilities based on banner matching.
- **Modular design** – adding new scanners is as simple as creating a new class.
- **No external API dependencies** – works offline with local data.
- **Clean and reusable utility layer** – `HttpUtils` offers header/body fetch methods for new modules.

---

## 🔧 Usage

### 1. Requirements

- Java 8 or above
- `json.jar` (for `org.json` parsing) — [Download here](https://repo1.maven.org/maven2/org/json/json/)

### 2. Compilation

```bash
javac -cp .:json.jar Main.java core/*.java modules/*.java utils/*.java

3. Execution

java -cp .:json.jar Main http://example.com


---

🧪 Scanner Modules (Included)

HttpHeaderScanner.java

Analyzes response headers such as Server, X-Powered-By, and others that may disclose backend technologies or misconfigurations.

CVEChecker.java

Matches server banners against a local CVE JSON database (data/cve_db.json). This can be extended with additional entries or automated feeds.

HttpUtils.java

Utility for standardized HTTP GET requests, including full response body and headers extraction. Encourages consistency across modules.


---

🔍 Sample Output

[HttpHeaderScanner]
Server: Apache/2.4.49
X-Powered-By: PHP/7.4.3

[CVEChecker]
Found CVE: CVE-2021-41773 - Path traversal in Apache 2.4.49


---

🧩 Extending the Tool

To add a new vulnerability check:

1. Create a new class under modules/ implementing Runnable.


2. Use HttpUtils for fetching content.


3. Register your module inside ScannerEngine.



Examples:

SSLCertificateScanner.java – validate HTTPS configuration and expiry

JavaScriptLinkExtractor.java – scrape dynamic links from scripts

AdminPanelFinder.java – brute-force common admin paths



---

⚙️ Design Philosophy

Maintainability: Code is modular, cleanly separated, and follows SOLID principles.

Extensibility: Each module can be independently developed and tested.

Performance: All scans are parallelized using Java’s ExecutorService.

Zero-dependency mode: Except for the org.json library, it runs without APIs or databases.



---

📃 License

MIT License. Free for commercial or personal use. Attribution welcome.


---
