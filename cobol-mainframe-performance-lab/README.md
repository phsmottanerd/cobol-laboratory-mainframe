# COBOL MAINFRAME PERFORMANCE LAB

**Paulo Henrique Santana Motta**

**Administrador Linux | Analista de Sistemas | SOC Analyst | Cybersecurity | Automação**

> Laboratório técnico de COBOL focado em processamento batch, desempenho, operações de arquivo, métricas de execução e automação de análise com Python.

---
## 🎯 Objetivo

Este projeto demonstra, de forma prática e reproduzível, conceitos relacionados a:

- COBOL
- processamento batch
- processamento de grandes volumes
- operações de leitura e escrita em arquivos
- medição de CPU e tempo de execução
- análise de resultados
- automação com Python
- organização de evidências técnicas
- fundamentos relacionados a ambientes IBM Z/Mainframe

O laboratório foi desenvolvido inicialmente em **GnuCOBOL sobre Linux/WSL2**, permitindo desenvolver, executar, medir e documentar os experimentos antes de uma futura adaptação para ambientes Mainframe.

---

## 🏗️ Arquitetura

```text
COBOL SOURCE
     │
     ▼
  WORKLOADS
     │
     ▼
BENCHMARK / OS METRICS
     │
     ▼
RESULTS/*.TXT
     │
     ▼
PYTHON PERFORMANCE ANALYZER
     │
     ▼
PERFORMANCE-REPORT.MD
```

---
## 🧪 Experimentos

| Experimento | Registros | Tempo | CPU |
|---|---:|---:|---:|
| Baseline | 1.000.000 | 0,09 s | 100% |
| Workload 02 | 50.000.000 | 4,84 s | 99% |
| Workload 03 | 100.000 | 0,05 s | 62% |
| Workload 04 | 1.000.000 | 0,33 s | 98% |

### Workload 01 — Baseline CPU

Processamento repetitivo em memória para estabelecer uma referência inicial de execução.

### Workload 02 — 50 milhões

Ampliação significativa da carga de processamento para observar o comportamento do programa sob maior volume de operações.

### Workload 03 — Batch I/O

Leitura de **100.000 registros** e gravação de **100.000 registros** em arquivo.

### Workload 04 — Batch I/O — 1 milhão

Leitura e gravação de **1.000.000 de registros**, aumentando o volume do processamento.

---
## 🧰 Tecnologias

- COBOL
- GnuCOBOL 3.2.0
- Python 3
- Linux
- WSL2
- Bash
- `/usr/bin/time`

---

## 📂 Estrutura do Projeto

```text
cobol-mainframe-performance-lab/
├── analyzer/
│   └── analyzer.py
├── data/
│   └── input.dat
├── results/
│   ├── baseline.txt
│   ├── workload-02.txt
│   ├── workload-03.txt
│   ├── workload-04.txt
│   └── performance-report.md
└── src/
    ├── performance_lab.cob
    └── batch_io_lab.cob
```

---

## 🐍 Python Performance Analyzer

O arquivo `analyzer/analyzer.py` processa automaticamente os resultados dos experimentos e gera o relatório `results/performance-report.md`.

O relatório consolida:

- quantidade de registros
- tempo de execução
- utilização de CPU
- resumo dos experimentos
- ambiente utilizado

---
## 🔬 Evidências

Os resultados individuais ficam armazenados em `results/`.

Cada arquivo `.txt` registra as métricas obtidas durante a execução.

Nos workloads de I/O, a quantidade real de registros processados também foi validada diretamente pelos arquivos gerados.

> **Nota:** as métricas de filesystem apresentadas pelo `/usr/bin/time` são métricas do sistema operacional e não representam a quantidade de registros processados.

---

## ⚙️ Compilação

Exemplo de compilação com GnuCOBOL:

```bash
cobc -x -free -o results/performance_lab src/performance_lab.cob
```

Para o programa de Batch I/O:

```bash
cobc -x -free -o results/batch_io_lab src/batch_io_lab.cob
```

---

## 🐍 Executando o Analyzer

```bash
python3 analyzer/analyzer.py
```

O relatório será criado automaticamente em `results/performance-report.md`.

---

## 🚀 Próxima Evolução

```text
GnuCOBOL
   │
   ▼
Batch Processing
   │
   ▼
Performance Analysis
   │
   ▼
JCL
   │
   ▼
VSAM
   │
   ▼
TK5 / MVS 3.8j
   │
   ▼
IBM Z / z/OS
```

Possíveis extensões:

- JCL
- VSAM
- processamento batch em ambiente Mainframe
- DB2
- CICS
- análise de datasets
- automação Python
- integração com ambientes IBM Z

---
## ⚠️ Escopo

Este projeto é um laboratório local de desenvolvimento e benchmarking com GnuCOBOL.

Os resultados apresentados representam o ambiente Linux/WSL2 utilizado durante os testes e não são apresentados como medições de desempenho de um Mainframe IBM Z real.

O objetivo é demonstrar conhecimentos práticos de COBOL, processamento batch, medição de desempenho, análise de resultados e preparação para uma evolução posterior para ambientes Mainframe.

---

## 👤 Autor

**Paulo Henrique Santana Motta**

Administrador Linux | Analista de Sistemas | SOC Analyst | Cybersecurity | Automação

**Áreas de interesse:**

`COBOL` · `IBM Z` · `z/OS` · `Linux` · `Cybersecurity` · `Python` · `Automação` · `Mainframe`

---

## 📌 Status

**Laboratório funcional — primeira versão concluída.**

COBOL + Batch + Performance + Python Analyzer + Relatório automatizado.
