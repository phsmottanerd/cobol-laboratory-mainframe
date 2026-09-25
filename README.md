from pathlib import Path
from PIL import Image, ImageDraw, ImageFont
import math

out = Path("/mnt/data/cobol_laboratory_mainframe_assets")
out.mkdir(parents=True, exist_ok=True)
(out / "assets").mkdir(exist_ok=True)

# ---------- README ----------
readme = r"""# COBOL MAINFRAME PERFORMANCE LAB

<p align="center">
  <img src="./assets/cobol-mainframe-terminal.gif" alt="COBOL Mainframe Performance Lab animated terminal banner">
</p>

<p align="center">
  <strong>COBOL • BATCH PROCESSING • PERFORMANCE • PYTHON AUTOMATION • IBM Z / MAINFRAME</strong>
</p>

<p align="center">
  <a href="./cobol-mainframe-performance-lab/">📁 Laboratory source</a> •
  <a href="./cobol-mainframe-performance-lab/results/performance-report.md">📊 Performance report</a> •
  <a href="./assets/cobol-mainframe-terminal.svg">🖥️ SVG banner</a>
</p>

---

## 🟢 LABORATORY OVERVIEW

**COBOL Mainframe Performance Lab** is a practical engineering laboratory focused on **COBOL batch processing, workload execution, operating-system measurements, performance evidence and Python-based result analysis**.

The project was built to demonstrate a professional workflow rather than a simple CRUD application:

```text
┌──────────────────────────────────────────────────────────────────────┐
│                    COBOL MAINFRAME PERFORMANCE LAB                  │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  COBOL SOURCE                                                       │
│       │                                                              │
│       ▼                                                              │
│  REPEATABLE WORKLOADS ───────► CPU / TIME / MEMORY / I/O METRICS    │
│       │                                      │                       │
│       ▼                                      ▼                       │
│  BATCH PROCESSING                    RESULTS/*.TXT                  │
│                                              │                       │
│                                              ▼                       │
│                                  PYTHON PERFORMANCE ANALYZER         │
│                                              │                       │
│                                              ▼                       │
│                                  PERFORMANCE-REPORT.MD               │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
