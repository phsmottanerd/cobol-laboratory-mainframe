
<p align="center">
  <img src="./assets/cobol-mainframe-terminal.gif"
       alt="COBOL Mainframe Performance Lab">
</p>




# COBOL MAINFRAME PERFORMANCE LAB

<p align="center">
  <img src="./assets/cobol-mainframe-terminal.gif" alt="COBOL Mainframe Performance Lab">
</p>

<p align="center">
  <strong>COBOL • BATCH • PERFORMANCE • PYTHON • IBM Z / MAINFRAME</strong>
</p>

<p align="center">

**Paulo Henrique Santana Motta**

**Administrador Linux | Analista de Sistemas | SOC Analyst | Cybersecurity | Automação**

</p>

> Laboratório técnico de COBOL focado em processamento batch, desempenho, operações de arquivo, métricas de execução, evidências técnicas e automação de análise com Python.

---

## 🎯 Objetivo

Este projeto foi desenvolvido como um laboratório técnico para explorar, medir e documentar **processamento COBOL em workloads controlados**.

A proposta não é apenas executar um programa COBOL, mas construir um fluxo completo:

```text
┌─────────────────────────────────────────────────────────────┐
│                  COBOL PERFORMANCE WORKFLOW                 │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   SOURCE CODE                                               │
│       │                                                     │
│       ▼                                                     │
│   WORKLOAD                                                  │
│       │                                                     │
│       ▼                                                     │
│   EXECUTION                                                 │
│       │                                                     │
│       ▼                                                     │
│   PERFORMANCE METRICS                                       │
│       │                                                     │
│       ▼                                                     │
│   TECHNICAL EVIDENCE                                        │
│       │                                                     │
│       ▼                                                     │
│   PYTHON ANALYSIS                                           │
│       │                                                     │
│       ▼                                                     │
│   AUTOMATED REPORT                                          │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

O laboratório demonstra, de forma prática e reproduzível:

* COBOL;
* processamento batch;
* processamento de grandes volumes;
* leitura sequencial de arquivos;
* escrita sequencial de arquivos;
* medição de CPU;
* medição de tempo de execução;
* observação de memória;
* page faults;
* métricas de filesystem;
* validação de registros processados;
* preservação de evidências;
* análise automatizada com Python;
* geração de relatório técnico;
* fundamentos relacionados ao ecossistema IBM Z/Mainframe.

O desenvolvimento inicial foi realizado com **GnuCOBOL 3.2.0 sobre Linux/WSL2**, permitindo construir e validar os workloads antes de uma futura evolução para ambientes Mainframe.

---

## 🏗️ Arquitetura

```text
                     ┌─────────────────────┐
                     │    COBOL SOURCE     │
                     └──────────┬──────────┘
                                │
                                ▼
                     ┌─────────────────────┐
                     │      WORKLOADS      │
                     └──────────┬──────────┘
                                │
                    ┌───────────┴───────────┐
                    ▼                       ▼
             ┌─────────────┐        ┌─────────────┐
             │ CPU PROCESS │        │  BATCH I/O  │
             └──────┬──────┘        └──────┬──────┘
                    │                      │
                    └──────────┬───────────┘
                               ▼
                     ┌─────────────────────┐
                     │  /usr/bin/time -v  │
                     └──────────┬──────────┘
                                │
                                ▼
                     ┌─────────────────────┐
                     │    RESULTS/*.TXT   │
                     └──────────┬──────────┘
                                │
                                ▼
                 ┌────────────────────────────┐
                 │ PYTHON PERFORMANCE ANALYZER│
                 └─────────────┬──────────────┘
                               │
                               ▼
                 ┌────────────────────────────┐
                 │ PERFORMANCE-REPORT.MD      │
                 └────────────────────────────┘
```

A arquitetura separa:

```text
COBOL
  ↓
PROCESSAMENTO
  ↓
MEDIÇÃO
  ↓
EVIDÊNCIA
  ↓
ANÁLISE
  ↓
RELATÓRIO
```

Essa separação permite repetir os experimentos e analisar os resultados sem misturar a lógica de processamento COBOL com a camada de análise.

---

## 🧪 Experimentos

| Experimento             |  Registros |  Tempo |  CPU |
| ----------------------- | ---------: | -----: | ---: |
| Baseline CPU            |  1.000.000 | 0,09 s | 100% |
| Workload 02 — CPU       | 50.000.000 | 4,84 s |  99% |
| Workload 03 — Batch I/O |    100.000 | 0,05 s |  62% |
| Workload 04 — Batch I/O |  1.000.000 | 0,33 s |  98% |

### Workload 01 — Baseline CPU

O primeiro experimento estabelece uma referência inicial de execução.

O programa executa operações repetitivas em memória e mantém um contador dos registros processados.

Objetivo:

```text
Estabelecer uma linha de base
             │
             ▼
Executar workload controlado
             │
             ▼
Medir CPU e tempo
             │
             ▼
Preservar evidência
```

Resultado:

```text
Records:  1.000.000
Elapsed:  0,09 s
CPU:      100%
```

---

### Workload 02 — 50 milhões

O segundo experimento aumenta significativamente a quantidade de operações.

```text
1.000.000
    │
    ▼
50.000.000
```

O objetivo é observar o comportamento do processamento quando a carga aumenta.

Resultado:

```text
Records:  50.000.000
Elapsed:  4,84 s
CPU:      99%
```

Esse workload funciona como uma referência de **processamento intensivo em CPU** dentro do ambiente local utilizado.

---

### Workload 03 — Batch I/O

O terceiro experimento introduz operações reais de arquivo.

Fluxo:

```text
INPUT FILE
    │
    ▼
OPEN INPUT
    │
    ▼
READ
    │
    ▼
PROCESS
    │
    ▼
WRITE
    │
    ▼
READ NEXT
    │
    ▼
EOF
    │
    ▼
CLOSE
```

Foram processados:

```text
Records Read:     100.000
Records Written:  100.000
```

Resultado:

```text
Elapsed: 0,05 s
CPU:     62%
```

O resultado do arquivo de saída também foi validado posteriormente para confirmar a quantidade efetivamente gravada.

---

### Workload 04 — Batch I/O — 1 milhão

O quarto experimento mantém a mesma lógica do Batch I/O, porém aumenta significativamente o volume.

```text
100.000
   │
   ▼
1.000.000
```

Resultado:

```text
Records Read:     1.000.000
Records Written:  1.000.000
Elapsed:          0,33 s
CPU:              98%
```

Esse experimento permite observar o comportamento do mesmo fluxo de processamento sob uma carga maior.

---

# 📊 Métricas de Execução

As execuções foram medidas utilizando:

```bash
/usr/bin/time -v
```

Entre as métricas coletadas estão:

```text
User CPU Time
System CPU Time
Elapsed Time
CPU %
Maximum RSS
Major Page Faults
Minor Page Faults
Filesystem Inputs
Filesystem Outputs
Exit Status
```

Além dessas métricas, os próprios programas COBOL registram:

```text
Records Processed
Records Read
Records Written
```

---

## 🔬 Aplicação x Sistema Operacional

Uma preocupação importante do laboratório é não confundir métricas diferentes.

### Métricas da aplicação

Produzidas pelo próprio programa COBOL:

```text
Records Processed
Records Read
Records Written
```

### Métricas do processo

Produzidas pelo sistema operacional:

```text
CPU
Elapsed
RSS
Page Faults
Filesystem I/O
Exit Status
```

Assim, uma métrica de filesystem apresentada pelo `/usr/bin/time` não é interpretada automaticamente como quantidade de registros processados.

> **Nota:** nos workloads de I/O, a quantidade real de registros processados foi validada separadamente pelos arquivos gerados.

---

# 🐍 Python Performance Analyzer

O projeto possui uma camada de automação desenvolvida em Python.

Arquivo:

```text
analyzer/analyzer.py
```

O Analyzer percorre os resultados armazenados em `results/`, identifica as principais métricas e consolida os experimentos.

Fluxo:

```text
RESULTS/*.TXT
      │
      ▼
PYTHON
      │
      ├── Records
      ├── Elapsed
      └── CPU
      │
      ▼
CONSOLIDATION
      │
      ▼
PERFORMANCE-REPORT.MD
```

O relatório apresenta:

* experimento;
* quantidade de registros;
* tempo decorrido;
* utilização de CPU;
* resumo do ambiente;
* descrição dos workloads;
* objetivo do laboratório.

Executando:

```bash
python3 analyzer/analyzer.py
```

O resultado é gerado automaticamente em:

```text
results/performance-report.md
```

---

# 📂 Estrutura do Projeto

```text
cobol-mainframe-performance-lab/
│
├── analyzer/
│   └── analyzer.py
│
├── data/
│   └── input.dat
│
├── results/
│   ├── baseline.txt
│   ├── workload-02.txt
│   ├── workload-03.txt
│   ├── workload-04.txt
│   └── performance-report.md
│
└── src/
    ├── performance_lab.cob
    └── batch_io_lab.cob
```

### `src/`

Contém os programas COBOL utilizados nos experimentos.

### `data/`

Contém os dados utilizados pelos workloads de processamento de arquivo.

### `results/`

Contém as evidências das execuções e o relatório consolidado.

### `analyzer/`

Contém a automação Python responsável pela análise dos resultados.

---

# 🧰 Tecnologias

```text
┌─────────────────────────────────────────────┐
│ COBOL MAINFRAME PERFORMANCE STACK           │
├─────────────────────────────────────────────┤
│                                             │
│ COBOL              → Workloads              │
│ GnuCOBOL 3.2.0     → Compiler/Runtime      │
│ Linux              → Execution Environment   │
│ WSL2               → Linux Laboratory       │
│ Bash               → Automation             │
│ /usr/bin/time      → Performance Metrics    │
│ Python 3           → Result Analysis        │
│ Git / GitHub       → Version Control        │
│                                             │
└─────────────────────────────────────────────┘
```

---

# ⚙️ Compilação

## CPU workload

```bash
cobc -x -free -o results/performance_lab src/performance_lab.cob
```

## Batch I/O

```bash
cobc -x -free -o results/batch_io_lab src/batch_io_lab.cob
```

---

# ▶️ Execução

## CPU

```bash
/usr/bin/time -v ./results/performance_lab
```

## Batch I/O

```bash
/usr/bin/time -v ./results/batch_io_lab
```

## Analyzer

```bash
python3 analyzer/analyzer.py
```

---

# 🔬 Evidências

Cada workload possui seu próprio registro de execução.

```text
results/
│
├── baseline.txt
├── workload-02.txt
├── workload-03.txt
├── workload-04.txt
└── performance-report.md
```

Isso cria uma trilha técnica:

```text
SOURCE
  ↓
COMPILE
  ↓
EXECUTE
  ↓
MEASURE
  ↓
VALIDATE
  ↓
STORE EVIDENCE
  ↓
ANALYZE
  ↓
REPORT
```

O objetivo é que os resultados possam ser inspecionados posteriormente, em vez de depender somente de uma execução momentânea no terminal.

---

# 🖥️ Conceito Mainframe

O laboratório foi estruturado com uma visão de evolução para o ecossistema Mainframe.

O ambiente atual é:

```text
GnuCOBOL
Linux
WSL2
```

A arquitetura futura é:

```text
GnuCOBOL
    │
    ▼
Batch Processing
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

Posteriormente:

```text
IBM Z / z/OS
      │
      ├── JCL
      ├── VSAM
      ├── DB2
      ├── CICS
      └── Dataset Management
```

O projeto, portanto, serve como uma **ponte prática entre desenvolvimento COBOL local e estudos posteriores de Mainframe**.

---

# 🚀 Próxima Evolução

## Fase atual — concluída

```text
✓ COBOL
✓ CPU workload
✓ 50 milhões de operações
✓ Batch I/O
✓ 100 mil registros
✓ 1 milhão de registros
✓ Métricas de execução
✓ Evidências técnicas
✓ Python Analyzer
✓ Relatório automatizado
```

## Próxima fase

```text
JCL
 │
 ▼
JOB
 │
 ▼
EXEC
 │
 ▼
DD
 │
 ▼
DATASETS
```

Depois:

```text
VSAM
 │
 ▼
TK5 / MVS 3.8j
 │
 ▼
IBM Z / z/OS
```

Possíveis extensões:

* JCL;
* VSAM;
* processamento batch em ambiente Mainframe;
* datasets;
* DB2;
* CICS;
* automação Python;
* monitoramento;
* análise de datasets;
* integração com ferramentas IBM Z.

---

# ⚠️ Escopo

Este projeto é um laboratório local de desenvolvimento e benchmarking utilizando **GnuCOBOL sobre Linux/WSL2**.

Os resultados apresentados representam o ambiente utilizado durante os testes.

Eles **não são apresentados como benchmarks de um IBM Z real**.

O objetivo é demonstrar conhecimentos práticos relacionados a:

* COBOL;
* processamento batch;
* operações de arquivo;
* medição de desempenho;
* análise de execução;
* organização de evidências;
* automação com Python;
* fundamentos de Mainframe.

A evolução para IBM Z/z/OS será realizada em etapas posteriores.

---

# 👤 Autor

## Paulo Henrique Santana Motta

**Administrador Linux | Analista de Sistemas | SOC Analyst | Cybersecurity | Automação**

### Áreas de interesse

```text
COBOL
IBM Z
z/OS
Linux
Cybersecurity
Python
Automação
Mainframe
```

---

# 📌 Status

```text
╔══════════════════════════════════════════════════════════════╗
║                 COBOL MAINFRAME LAB                         ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  COBOL ......................... ONLINE                     ║
║  CPU WORKLOAD .................. ONLINE                     ║
║  BATCH PROCESSING .............. ONLINE                     ║
║  FILE I/O ...................... ONLINE                     ║
║  PERFORMANCE METRICS ........... ONLINE                     ║
║  PYTHON ANALYZER ............... ONLINE                     ║
║  REPORTING ..................... ONLINE                     ║
║                                                              ║
║  MAINFRAME ROADMAP ............. IN PROGRESS                ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
```

**Laboratório funcional — primeira versão concluída.**

### COBOL + Batch + Performance + Python Analyzer + Evidências + Relatório automatizado

---

<p align="center">

**COBOL • BATCH • PERFORMANCE • PYTHON • LINUX • IBM Z**

</p>

<p align="center">

**Built by Paulo Henrique Santana Motta**

</p>
