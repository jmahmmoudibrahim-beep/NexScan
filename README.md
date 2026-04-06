<p align="center">
  <h1 align="center">NexScan</h1>
  <p align="center">Advanced AI-Driven Vulnerability Scanner & Penetration Testing Tool</p>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/python-3.8+-blue.svg" alt="Python 3.8+">
  <img src="https://img.shields.io/badge/status-active-brightgreen.svg" alt="Status: Active">
  <img src="https://img.shields.io/badge/version-1.3.0-orange.svg" alt="Version 1.3.0">
</p>

---

NexScan is an AI-powered penetration testing and vulnerability scanning tool that integrates multiple AI providers (OpenAI, Grok, Ollama, Mistral, OpenRouter) to deliver intelligent payload generation, comprehensive security assessments, and professional reporting.

## Features

### Core Capabilities

- Multi-AI provider support with dynamic switching at runtime
- AI-powered, CVE-aware, context-sensitive payload generation
- Intelligent web crawling with configurable depth and threading
- Advanced reconnaissance with OSINT integration
- Professional report generation (PDF / HTML / JSON)
- Custom plugin system for extending scan functionality
- Real-time alert notifications via Email, Slack, and Discord
- Team-based distributed scanning for collaborative assessments

### Vulnerability Detection

**Core Checks**
- SQL Injection (error-based, blind, time-based)
- Cross-Site Scripting (reflected, stored, DOM-based)
- Command Injection / OS Command Execution
- Server-Side Request Forgery (SSRF)
- XML External Entity (XXE) Injection
- Path Traversal / Local File Inclusion
- Cross-Site Request Forgery (CSRF)
- Open Redirect
- CORS Misconfiguration
- Security Header Analysis

**Advanced Modules**
- Authentication & Session Testing (brute-force, session fixation, token analysis)
- API Security Testing (REST & GraphQL fuzzing, method enumeration)
- Business Logic Flaw Detection (race conditions, IDOR, price manipulation)
- File Upload Vulnerability Testing (extension bypass, content-type spoofing)
- WebSocket Security Testing (origin validation, injection, DoS)
- Server-Side Template Injection (SSTI)
- HTTP Request Smuggling
- Cache Poisoning
- JWT Token Attacks
- Insecure Deserialization

**Intelligence & Detection**
- ML-based anomaly detection for response analysis
- Advanced payload obfuscation (encoding, case variation, comment insertion)
- Enhanced OSINT reconnaissance (subdomain enum, email harvesting, breach checks)
- Interactive HTML reports with Chart.js visualizations

## Prerequisites

- Python 3.8 or higher
- API key for at least one supported AI provider:
  - OpenAI, xAI (Grok), Mistral, or OpenRouter
  - Or a local Ollama instance (no API key needed)

## Installation

### Quick Install

**Windows (PowerShell):**
```powershell
git clone https://github.com/jmahmmoudibrahim-beep/NexScan.git
cd NexScan
python -m venv venv
.\venv\Scripts\Activate
pip install -r requirements.txt
```

**Linux / macOS:**
```bash
git clone https://github.com/jmahmmoudibrahim-beep/NexScan.git
cd NexScan
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### Manual Setup

1. Clone the repository
2. Install dependencies: `pip install -r requirements.txt`
3. Copy the example config: `cp config/config.example.yaml config/config.yaml`
4. Edit `config/config.yaml` with your AI provider API keys
5. Run: `python nexscan.py -u <target-url>`

## Usage

### Quick Start

```bash
# Basic scan with default settings
python nexscan.py -u https://target.com

# Full scan with reconnaissance enabled
python nexscan.py -u https://target.com --full-scan --recon

# Scan with a specific AI provider
python nexscan.py -u https://target.com --provider grok
```

### Configuration-Driven Scanning

Create or edit `config/config.yaml`:

```yaml
target:
  url: "https://target.com"

ai_providers:
  openai:
    enabled: true
    api_key: "your-api-key"
    model: "gpt-4o"
scanner:
  default_threads: 5
  default_depth: 2
  timeout: 10

vulnerability_scanner:
  enabled_checks:
    - sql_injection
    - xss
    - command_injection
    - ssrf
    - xxe
    - path_traversal

reporting:
  default_format: html
```

Then run:

```bash
python nexscan.py -c config/config.yaml
```

### Command Line Options

| Argument | Description |
|---|---|
| `-u, --url` | Target URL to scan |
| `-c, --config` | Path to configuration file |
| `--provider` | AI provider to use (openai, grok, ollama, mistral, openrouter) |
| `--depth` | Crawl depth (default: 2) |
| `--threads` | Number of threads (default: 5) |
| `--full-scan` | Enable all vulnerability checks |
| `--recon` | Enable reconnaissance module |
| `-o, --output` | Output report path |
| `--format` | Report format: html, pdf, json (default: html) |
| `-v, --verbose` | Enable verbose output |

## Project Structure

```
NexScan/
├── nexscan.py                  # Main entry point
├── requirements.txt            # Python dependencies
├── setup.py                    # Package setup
├── config/
│   └── config.example.yaml     # Example configuration
├── core/
│   ├── scanner_engine.py       # Core scanning engine & crawler
│   ├── vulnerability_scanner.py # Vulnerability detection (45+ checks)
│   ├── ai_payload_generator.py # AI-powered payload generation
│   ├── report_generator.py     # PDF/HTML/JSON report generation
│   └── plugin_manager.py       # Custom plugin loader
├── ai_providers/
│   ├── provider_manager.py     # Multi-provider manager
│   ├── openai_provider.py      # OpenAI integration
│   ├── grok_provider.py        # xAI Grok integration
│   ├── ollama_provider.py      # Local Ollama integration
│   ├── mistral_provider.py     # Mistral AI integration
│   └── openrouter_provider.py  # OpenRouter integration
├── modules/
│   ├── reconnaissance/         # Recon & OSINT modules
│   ├── api_security/           # REST & GraphQL testing
│   ├── authentication/         # Auth & session testing
│   ├── business_logic/         # Business logic flaw detection
│   ├── file_upload/            # File upload testing
│   ├── websocket/              # WebSocket security testing
│   ├── ml_detection/           # ML anomaly detection
│   ├── payload_obfuscation/    # Payload encoding & obfuscation
│   ├── collaboration/          # Team-based scanning
│   └── reporting/              # Interactive HTML reports
├── utils/
│   ├── config_loader.py        # YAML config loader
│   ├── http_client.py          # HTTP client with retries
│   ├── logger.py               # Logging utility
│   ├── notification_manager.py # Email/Slack/Discord alerts
│   └── parser.py               # URL & response parsers
├── plugins/                    # Custom scanner plugins
└── examples/                   # Usage examples
```

## Troubleshooting

### PDF Report Generation

If PDF generation fails, install the required system dependency:

```bash
# Ubuntu/Debian
sudo apt-get install wkhtmltopdf

# macOS
brew install wkhtmltopdf

# Windows - download installer from wkhtmltopdf.org
```

### Common Issues

1. **Import errors**: Make sure all dependencies are installed: `pip install -r requirements.txt`
2. **AI provider errors**: Verify your API key is correct in `config/config.yaml`
3. **Timeout errors**: Increase the `timeout` value in your config
4. **SSL errors**: Set `verify_ssl: false` in the scanner config (not recommended for production)

## Disclaimer

**This tool is intended for authorized security testing only.**

- Only use on systems you own or have explicit written permission to test
- Unauthorized access to computer systems is illegal
- The developers are not responsible for any misuse of this tool
- Always follow responsible disclosure practices

## Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues.

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes
4. Push to the branch: `git push origin feature/your-feature`
5. Open a pull request

## License

This project is provided as-is for educational and authorized security testing purposes.

## Acknowledgments

- Built with support from multiple AI provider APIs
- Inspired by the open-source security research community

---

<p align="center"><b>NexScan</b> — Next-Gen AI Security Scanner</p>
