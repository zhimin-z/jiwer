# Unified Evaluation Workflow Support

This document catalogs which strategies from the unified evaluation workflow are natively supported by JiWER. A strategy is considered "supported" only if JiWER provides it natively in its full installation—meaning that once JiWER is fully installed, the strategy can be executed directly without implementing custom modules or integrating external libraries.

## Supported Strategies

### Phase 0: Provisioning (The Runtime)

#### Step A: Harness Installation

- ✅ **Strategy 1: Git Clone** - JiWER can be cloned from the source code repository (`git clone https://github.com/jitsi/jiwer.git`) and installed manually from source
- ✅ **Strategy 2: PyPI Packages** - JiWER can be installed via `pip install jiwer` or `uv add jiwer`

#### Step B: Credential Configuration

- ❌ **No strategies supported** - JiWER does not require authentication with model APIs, artifact repositories, or evaluation platforms

---

### Phase I: Specification (The Contract)

#### Step A: SUT Preparation

- ✅ **Strategy 3: Algorithm Implementation (In-Memory Structures)** - JiWER implements algorithmic data structures for text similarity evaluation, specifically Levenshtein edit distance algorithms (using RapidFuzz library) for comparing reference and hypothesis text sequences

#### Step B: Benchmark Preparation (Inputs)

- ✅ **Strategy 1: Benchmark Data Preparation (Offline)** - JiWER accepts predefined test inputs as:
  - Single or multiple reference/hypothesis string pairs via Python API
  - New-line delimited text files via CLI
  - Optional preprocessing through transformation pipeline (text normalization, case conversion, punctuation removal, etc.)

#### Step C: Benchmark Preparation (References)

- ✅ **Strategy 1: Ground Truth Preparation** - JiWER uses reference text as ground truth for comparison against hypothesis text through edit distance alignment

---

### Phase II: Execution (The Run)

#### Step A: SUT Invocation

- ✅ **Strategy 1: Batch Inference** - JiWER processes multiple reference/hypothesis pairs in a single evaluation run, computing error metrics across all samples

---

### Phase III: Assessment (The Score)

#### Step A: Individual Scoring

- ✅ **Strategy 1: Deterministic Measurement** - JiWER computes deterministic error metrics using edit distance calculations:
  - Word Error Rate (WER)
  - Character Error Rate (CER)
  - Match Error Rate (MER)
  - Word Information Lost (WIL)
  - Word Information Preserved (WIP)
  - Alignment-based metrics (substitutions, insertions, deletions, hits)

#### Step B: Aggregate Scoring

- ✅ **Strategy 1: Distributional Statistics** - JiWER aggregates per-instance scores into benchmark-level metrics by computing overall error rates across all reference/hypothesis pairs

---

### Phase IV: Reporting (The Output)

#### Step A: Insight Presentation

- ❌ **No strategies supported** - JiWER provides basic console output and alignment visualization but does not natively support:
  - Execution tracing with detailed logs
  - Subgroup analysis by demographic groups or data domains
  - Regression alerting against historical baselines
  - Chart generation (radar charts, histograms, trend plots)
  - Dashboard creation with interactive web interfaces
  - Leaderboard publication to external platforms

---

## Summary

JiWER natively supports **8 out of 66 total strategies** across the unified evaluation workflow:

**Supported Phases:**
- Phase 0: Provisioning - 2/10 strategies (20%)
- Phase I: Specification - 3/11 strategies (27%)
- Phase II: Execution - 1/4 strategies (25%)
- Phase III: Assessment - 2/6 strategies (33%)
- Phase IV: Reporting - 0/6 strategies (0%)

**Core Capability:** JiWER is a focused evaluation tool specialized in computing text similarity error metrics (WER, CER, etc.) for automatic speech recognition systems. It provides the essential capabilities for deterministic text comparison but does not include advanced features like model serving, synthetic data generation, uncertainty quantification, or interactive dashboards.
