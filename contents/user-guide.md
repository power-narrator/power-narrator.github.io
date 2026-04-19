{% set title="Power Narrator User Guide" %}
<frontmatter>
  title: {{ title }}
  pageNav: 3
</frontmatter>

<br>

# {{ title }}

Welcome to Power Narrator! This guide will help you install and set up the application on your macOS device.

## Prerequisites

Before installing, ensure your system meets the following requirements:
- **macOS**: The application is currently only supported on macOS due to automation dependencies.
- **Microsoft PowerPoint**: A licensed desktop version of PowerPoint must be installed.
- **Internet Connection**: Required for application setup and Google Cloud TTS narration.
- **GCP Service Account Key**: Required for Google Cloud TTS narration.

## Download

You can find the latest version of Power Narrator and the required PowerPoint Add-in on our release page:

👉 **[Download Power Narrator (Releases)](https://github.com/power-narrator/power-narrator-fe/releases)**

Please download both the `.dmg` (application) and the `ppt-tools.ppam` (PowerPoint Add-in).

---

## Installation Steps

### 1. Install the Application
1. Open the downloaded `.dmg` file.
2. Drag the **Power Narrator** icon into your **Applications** folder.
3. Open Power Narrator from your Applications folder.
   - *Note: If you see a "security" or "unidentified developer" warning, right-click the app and select **Open**, or go to **System Settings** → **Privacy & Security** and select **Open Anyway**.*

### 2. Install the PowerPoint Add-in (PPAM)
For the application to interact with PowerPoint, you must install the helper add-in:
1. Open **Microsoft PowerPoint**.
2. In the top menu bar, go to **Tools** → **PowerPoint Add-ins…**.
3. Click the **+** (Plus) button.
4. Navigate to and select the `ppt-tools.ppam` file you downloaded.
5. If prompted, click **Enable Macros**.
6. Ensure the `ppt-tools` item is checked in the list and click **OK**.

### 3. Basic Configuration
When you first open the app, you will need to configure your narration voice:
- **Settings (⚙)**: Click the gear icon to set up your Google Cloud TTS key.
- **Select File**: Click the landing page to select a `.pptx` file and start narrating!

---