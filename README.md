# NNN-CVE

NNN-CVE is a Streamlit-based penetration testing report generator that combines scanner outputs (Nmap, Nikto, Nessus), normalizes findings, maps them to CVEs, and exports professional reports.

## What It Does

- Run scans against a target (Nmap/Nikto, Nessus placeholder)
- Upload existing scanner reports (Nmap XML, Nikto XML/TXT, Nessus `.nessus`)
- Normalize findings into a common schema
- Map findings to likely CVEs using NLP/keyword similarity
- Generate downloadable outputs (PDF, CSV, JSON, HTML)
- Visualize severity, scanner sources, and findings in a dashboard

## Tech Stack

- Python 3.10+
- Streamlit
- Plotly + Pandas
- ReportLab (PDF generation)
- python-nmap
- Optional NLP stack: scikit-learn + nltk

## Project Structure

```text
NNN-CVE-main/
  app.py                                 # Main Streamlit app
  requirements.txt                       # Core dependencies
  pentest_report_generator/
    scanners/scanner_automation.py       # Nmap/Nikto automation layer
    parsers/                             # Nmap/Nikto/Nessus parsers
    utils/                               # Normalization, CVE mapping, exports, notifications
    reports/pdf_generator.py             # PDF report generator
    data/cve_data.json                   # Local CVE dataset for enrichment
  scan_results/                          # Generated raw scanner outputs
  temp_uploads/                          # Temporary uploaded files
  cve_cache/                             # Cached CVE index/database
  sample_reports/                        # Dummy sample input files
```

## Prerequisites

Install Python dependencies:

```bash
pip install -r requirements.txt
```

Install optional dependencies used by advanced features:

```bash
pip install requests scikit-learn nltk kaleido
```

Install external security tools (for live scanning mode):
- Nmap
- Nikto
- Nessus (optional; upload mode is supported even if local Nessus scanning is not configured)

## Run the App

From the project root:

```bash
streamlit run app.py
```

Streamlit will show a local URL, usually:
- [http://localhost:8501](http://localhost:8501)

## Usage

### 1. Scan Target Mode

- Enter a target hostname/IP
- Select scanners and speed/tuning options
- Start scan and review real-time logs
- Review normalized findings and severity charts
- Export report artifacts

### 2. Upload Reports Mode

- Upload one or more files:
  - Nmap XML
  - Nikto XML/TXT
  - Nessus `.nessus`
- Process uploaded reports
- Run CVE mapping and export outputs

## Exports

The app can generate:
- PDF report
- CSV findings
- JSON findings
- HTML report with interactive charts

Generated files appear with timestamped names in the project directory.

## Notes

- Nessus live scanning is currently a placeholder in `scanner_automation.py`; uploading `.nessus` reports is the practical path today.
- CVE mapping uses local CVE data first (`pentest_report_generator/data/cve_data.json`) and can fall back to NVD API if needed.
- `scan_results/`, `temp_uploads/`, and `cve_cache/` are expected runtime/output directories.

## Security & Legal Disclaimer

Use this tool only on systems you own or are explicitly authorized to test. Unauthorized scanning may violate laws and policies.

## Authors

- Arindam Singh
- Rudar Verma
