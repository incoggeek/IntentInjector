# 🛠️ Intent Injector

## A Proof-of-Concept Utility for Vulnerability Discovery

This tool is a self-contained Android application designed to test the security of installed applications by directly injecting malicious payloads into exported Android components (Activities, Services, Broadcast Receivers, and Content Providers) via **Intent manipulation**.

It is intended strictly for **educational purposes, security research, and penetration testing** on applications where explicit authorization has been granted.

---

## ✨ Features

The PoC tool is built to streamline the security analysis workflow:

| Feature | Description | Security Relevance |
| :--- | :--- | :--- |
| **Component Targeting** | Explicitly targets any installed app by package name and its Fully Qualified Class Name (FQCN), Intent Action, or Content URI. | Tests for **Unauthorized Component Launch** (ACSL). |
| **Package Resolution** | Automatically resolves partial package names (e.g., `com.app`) to the full package ID on the device. | Improves testing workflow speed and usability. |
| **Payload Injection** | Dynamically attaches custom data (Extras) to the outbound Intent. Supports *universal type injection* (string, boolean, integer, double). | Core function for **Parameter Tampering** and **Payload Injection** attacks. |
| **Manifest Scanner** | Scans the target package's `AndroidManifest.xml` via the `PackageManager` to list all **exported** Activities, Services, Receivers, and Content Providers. | Essential for **Enumeration**—identifying public attack surface. |
| **Built-in Payloads** | Includes easy-to-copy templates for common attacks, including **SQL Injection (SQLi)** and **Path Traversal/Local File Inclusion (LFI)**. | Facilitates quick execution of known exploit patterns. |

---

## 💣 Supported Attacks (Usage Scenarios)

This tool allows a tester to manually execute the following vulnerability checks against target applications:

### 1. **Data Disclosure / Path Traversal**
* **Target:** Vulnerable Activities or Services that accept a file path or URI as an Intent Extra.
* **Payload Example:** `../../../../data/data/TARGET_PACKAGE_NAME/shared_prefs/user_data.xml`
* **Goal:** Trick the target app into loading a sensitive, private file (like shared preferences or databases) via a relative path traversal attack.

### 2. **Authentication Bypass (SQLi)**
* **Target:** Components that pass Intent Extras directly into an unsanitized local SQLite database query (often in a content provider or service).
* **Payload Example (Value):** `' OR 1=1 --`
* **Goal:** Bypass local authentication checks, often seen in login screens or Content Provider queries.

### 3. **Unauthorized Component Access**
* **Target:** Any **exported** component, especially admin or privileged Activities/Services.
* **Goal:** Launch internal functionality (e.g., a Settings screen or a data viewing page) without proper user authentication or navigation checks.

---

## 🚀 Getting Started

### Prerequisites

* Android Studio (Latest Version)
* A physical Android Device or Emulator (API 30+ requires the `QUERY_ALL_PACKAGES` permission in the Manifest to scan other apps).

### Usage Steps

1.  **Target ID:** In the **Target Package Name** field, enter the package ID of the application you wish to test (e.g., `com.example.vulnerableapp`).
2.  **Discovery (Optional):** Click **"Scan Target Manifest"** to get a list of exposed FQCNs and URIs to use in the `FQCN / Intent Action / Provider URI` field.
3.  **Select Type:** Choose the component type (Activity, Service, etc.) from the dropdown.
4.  **Inject Payload:** Use **"Add Extra to Intent Bundle"** to define your payload (`key=value`). Use the **'C'** button to quickly copy the value/payload input.
5.  **Execute:** Click **"LAUNCH TARGET COMPONENT"**.
6.  **Verify:** Check the target app for crashes or unintended behavior. Review the **"Notes/Clipboard"** screen for a persistent log of the attempt outcome, including any `SecurityException` details.

---

## ⚠️ Disclaimer and Security Warning

This application is designed for research and educational purposes only. Do **NOT** use this tool to attack any application or system for which you do not have explicit, written authorization from the owner. Unauthorized use is illegal and unethical. The author takes no responsibility for any misuse of this software.

---
