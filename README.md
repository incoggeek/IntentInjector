# 🛠️ Intent Injector

<img width="300" height="600" alt="Intent Injector" src="https://github.com/user-attachments/assets/b2a9ec3c-8043-4d88-bd61-dc2e71f9b87a" />
<img width="300" height="600" alt="Intent Injector" src="https://github.com/user-attachments/assets/81233ac7-7963-4a38-88ad-94d8423a3f9a" />
<img width="300" height="600" alt="Intent Injector" src="https://github.com/user-attachments/assets/072c6af2-9106-4685-a2df-ac34454c68c8" />


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


## 🚀 Installation and Sideloading

Since the **Intent Injector PoC Tool** is a custom application and not available on the Google Play Store, you must install it via **sideloading** by enabling installation from unknown sources.

### 1. 📥 Download the APK File

1.  Navigate to the **Releases** section of this GitHub repository.
2.  Download the latest built application file (e.g., `Intent_injector_beta.apk`) from the **Assets** listed under the release notes.

    SHA1            939EE48D4ECBDEBABE30920FD293A58A0DE5B37F

### 2.Enable Installation from Unknown Sources

Android devices block installations from sources outside of the Play Store. You must temporarily grant permission to your file manager or browser.

1.  On your Android device, go to **Settings**.
2.  Search for **"Install unknown apps"** or navigate to **Security** $\rightarrow$ **Install unknown apps**.
3.  Find the application you used to download the file (usually **Chrome** or your **Files** app).
4.  **Toggle the switch ON** for that specific application to grant it permission to install the APK. 

### 3.Complete the Installation

1.  Open your **Files** app (or file manager) on your Android device.
2.  Navigate to the **Downloads** folder (or the location where you saved the `.apk` file).
3.  Tap the downloaded **`.apk` file** (`IntentInjector_beta.apk`).
4.  Tap **Install** when prompted by the system.

The **Intent Injector** is now installed and ready to launch from your app drawer.

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

---
## 🎥 Demonstration

[![Visit URL for Demo](https://github.com/user-attachments/assets/e79a0b7b-b8a6-4504-954d-ec1ece8f1e3c)

