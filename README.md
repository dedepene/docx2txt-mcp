# docx2txt-mcp

A tiny FastMCP tool that converts .docx files to plain text using python-docx.

This repository contains a small FastMCP server (`server.py`) exposing a tool named `docx_to_txt` that accepts either a local file path or the raw bytes of a `.docx` file and returns the document text.

## Prerequisites

- Windows (instructions below use cmd.exe)
- Python 3.12 (the project was developed with CPython 3.12)
- Node.js + npm (for installing the Gemini CLI)

## 1) Create and activate Python virtual environment (Windows, cmd.exe)

Open a cmd.exe terminal in the project root (`d:\Code\projects\mcp\docx2txt`) and run:

```cmd
python -m venv .venv
.venv\Scripts\activate
```

After activation, install the Python dependencies:

```cmd
pip install -r requirements.txt
```

## 2) Install the Google Gemini CLI

Install the latest Gemini CLI globally via npm:

```cmd
npm install -g @google/gemini-cli@latest
```

Verify the install is on your PATH and working:

```cmd
gemini --version
```

Note: The Gemini CLI may require additional setup or authentication depending on how you plan to use it. If you need to authenticate or configure credentials, follow Google's official Gemini CLI documentation.

## Gemini CLI configuration files (Windows)

Below is a quick reference for where the Gemini CLI looks for configuration and settings on Windows, and the precedence order used when multiple configuration files are present.

| File Type | Path on Windows | Precedence |
|---|---|---|
| User Settings (Global) | `%USERPROFILE%\\.gemini\\settings.json` | Overrides system defaults. |
| Project Settings (Local) | `\.gemini\\settings.json` (in your project's root) | Overrides user and system defaults. |
| System Settings (System-wide Override) | `C:\\ProgramData\\gemini-cli\\settings.json` | Highest precedence, overrides all others. |
| System Defaults (Base Layer) | `C:\\ProgramData\\gemini-cli\\system-defaults.json` | Lowest precedence. |

## Sample Gemini CLI config

You can use the following sample Gemini CLI configuration as a starting point. Copy it to your global user settings (`%USERPROFILE%\\.gemini\\settings.json`) or to a local project file (`.gemini\\settings.json`) and edit paths as needed for your environment.

```json
{
	"security": {
		"auth": {
			"selectedType": "oauth-personal"
		}
	},

	"mcpServers": {
		"DocxConverter": {
			"command": "D:\\Code\\projects\\mcp\\docx2txt\\.venv\\Scripts\\python.exe",
			"args": [
				"server.py"
			],
			"cwd": "D:\\Code\\projects\\mcp\\docx2txt\\"
		}
	}
}
```

