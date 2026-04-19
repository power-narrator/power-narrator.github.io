{% set title="Power Narrator Developer Guide" %}
<frontmatter>
  title: {{ title }}
  pageNav: 3
</frontmatter>

<br>

# {{ title }}

> [!IMPORTANT]
> **macOS Only Support**: Power Narrator currently requires **macOS** for its automation engine (AppleScript) to interface with Microsoft PowerPoint. Windows support is planned but not currently available.

## Setup & Installation

To get started with development on your local machine:

1. **Clone the repository**:
   ```bash
   git clone https://github.com/power-narrator/power-narrator-fe.git
   cd power-narrator
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Run in development mode**:
   ```bash
   npm run dev
   ```

## Build Instructions

To build and package the application for distribution:

- **Compile and Build**:
  ```bash
  npm run build
  ```
  This runs TypeScript compilation, Vite build for the frontend, and compiles the Electron main process.

- **Package for Distribution**:
  ```bash
  npm run dist
  ```
  This builds the application and creates a distributable package (e.g., `.dmg` or `.app` for macOS) using `electron-builder`.

## System Requirements

- **Operating System**: macOS (Required for AppleScript automation)
- **Node.js**: v25 or higher
- **Microsoft PowerPoint**: Desktop version with a valid license
- **Docker Desktop**: Only required if using the **Local TTS** mode

## Architecture Overview

Power Narrator is built as an Electron application with three distinct layers providing a modular and extensible architecture.

```
┌─────────────────────────────────────────┐
│           React Frontend (Vite)         │  ← src/
│ ViewerPage · SettingsModal · LandingPage│
└────────────────┬────────────────────────┘
                 │  Electron IPC (ipcRenderer / ipcMain)
┌────────────────▼────────────────────────┐
│           Electron Main Process         │  ← electron/main.ts
│   IPC Handlers · TtsManager · Store     │
└──────┬─────────────────────┬────────────┘
       │                     │
┌──────▼──────┐     ┌────────▼────────────┐
│ PptProvider │     │    TtsProvider      │
│  (Platform) │     │  (TTS Backend)      │
└──────┬──────┘     └────────┬────────────┘
       │                     │
┌────▼──────────┐    ┌─────▼────────────┐
│ MacPptProvider│    │ GcpTtsProvider   │
│ (AppleScript) │    │ LocalTtsProvider │
└──────┬────────┘    └──────────────────┘
       │
┌────────▼────────┐
│  XmlPptProvider │  ← Decorator over MacPptProvider
│   (XML CLI)     │      uses slide-voice-pptx binary
└─────────────────┘
```

### Core Design Patterns

- **Provider Pattern**: `PptProvider` and `TtsProvider` interfaces allow for multiple implementations (e.g., switching between Google Cloud and Local TTS).
- **Decorator Pattern**: `XmlPptProvider` wraps the standard provider to add XML-based manipulation capabilities via a bundled Python CLI.

## Configuration

### Environment Variables (.env)

Create a `.env` file in the root directory to configure your TTS providers:

```env
# --- Google Cloud TTS ---
# Set provider to 'gcp' and provide the path to your service account key
TTS_PROVIDER=gcp
GOOGLE_APPLICATION_CREDENTIALS=/path/to/your-google-cloud-key.json

# --- Local TTS (Mimic 3) ---
# Uncomment to use local server (default if TTS_PROVIDER is missing or not 'gcp')
# TTS_PROVIDER=local
# LOCAL_TTS_URL=http://localhost:59125/api/tts
# LOCAL_TTS_VOICE=en_UK/apope_low
```

### Google Cloud TTS (Recommended)
1. Create a GCP Service Account and download its JSON key.
2. In the app, click the **Settings (⚙)** icon and select the JSON key.
3. The app will automatically switch to GCP TTS.

### Local TTS (Offline)
Start the Mimic 3 Docker container:
```bash
docker run -it --user root -p 59125:59125 mycroftai/mimic3
```

### Compiling the PowerPoint Add-in (PPAM)

If you modify the VBA source code (`electron/scripts/ppt-tools.bas`), you must manually recompile the `.ppam` add-in file. Follow these step-by-step instructions:

1. **Open Microsoft PowerPoint**.
2. **Access the Visual Basic Editor**:
   - Go to the **Tools** menu at the top of your screen.
   - Select **Macro** → **Visual Basic Editor**.
   - *(Optional: If you have the **Developer** tab enabled in your ribbon, you can simply click **Visual Basic** there).*
3. **Clean Up Old Modules**:
   - In the **Project Explorer** window on the left side, look for a folder named **Modules**.
   - If a module named `AudioTools` already exists, right-click it and select **Remove AudioTools...**.
   - When asked "Do you want to export AudioTools before removing it?", select **No**.
4. **Import the Source Code**:
   - Go to the **File** menu in the Visual Basic Editor.
   - Select **Import File...**.
   - Navigate to your project directory and select the `electron/scripts/ppt-tools.bas` file.
   - Click **Open**. You should now see `AudioTools` listed under the Modules folder.
5. **Save as a PowerPoint Add-in**:
   - While still in the Visual Basic Editor, go to the **File** menu.
   - Select **Export...**.
   - In the "File Format" or "Save as type" dropdown menu, choose **PowerPoint Add-in (.ppam)**.
   - Ensure the filename is `ppt-tools.ppam`.
   - Save the file into the `electron/scripts/` directory of your project, overwriting the existing file if prompted.

### Loading PowerPoint Add-in (PPAM)
1. In PowerPoint, go to **Tools** → **PowerPoint Add-ins…**
2. Click **+** and select `electron/scripts/ppt-tools.ppam`.
3. Allow macro execution.

## Project Structure

- `electron/`: Main process logic, IPC handlers, and providers.
  - `platform/`: PowerPoint provider implementations.
  - `tts/`: Text-to-speech providers and managers.
  - `scripts/`: AppleScript automation and VBA macros.
- `src/`: React frontend source code built with Vite and Mantine.
- `xml/`: Python source for the optional XML CLI manipulation tool.

## XML CLI Mode

Power Narrator includes a different mode of operation that uses a Python-based CLI (`slide-voice-pptx`) to manipulate the `.pptx` XML directly, bypassing some VBA macro dependencies.

- Can be toggled in **Settings**.
- Supports audio insertion/removal and metadata queries.
- automatically closes and reopens the presentation during operations to ensure XML integrity.

## Troubleshooting

- **Gatekeeper Warning**: If macOS blocks the app, run:
  ```bash
  xattr -cr "/path/to/Power Narrator.app"
  ```
- **Local TTS 500 Error**: Verify the Docker container is running on port `59125` and the voice name in `.env` is valid.
