
# TimeGuard: Channel-wise Pool Training for Backdoor Defense in Time Series Forecasting

This repository provides code to (1) **run TSF backdoor attacks** to produce poisoned data, and (2) **apply TimeGuard** to defend against them.

---

## Table of Contents
- [1. Prerequisites](#1-prerequisites)
- [2. Configuration](#2-configuration)
- [3. Run the Framework](#3-run-the-framework)
  - [3.1 Running Attacks](#31-running-attacks)
  - [3.2 Running TimeGuard](#32-running-timeguard)
- [4. Datasets](#4-datasets)
- [Acknowledgement](#acknowledgement)

---

## 1. Prerequisites

- Python **3.10+**

- Install dependencies:

  ```bash
  pip install -r requirements.txt
  ```
---


## 2. Configuration

- `configs/default_config.yaml`
  Global defaults (model, dataset, target pattern list, etc.)

- `configs/attacks/*.yaml`
  Attack configurations (hyperparameters, training details, poison rate, trigger settings, etc.)

- `configs/timeguard/**/TimeGuard.yaml`
  TimeGuard defense configurations per dataset / model / attack save folder results from attack methods

---

## 3. Run the Framework

### 3.1 Running Attacks

Train an attacker and generate a poisoned dataset (**BackTime** on **PEMS03**):

```bash
python attack_backtime_run.py \
  --train_config_path configs/attacks/PEMS03_backtime_FEDformer_1212_attack.yaml
```

---

### 3.2 Running TimeGuard

Apply **TimeGuard** against a specified attack setting (example: defend against the above BackTime attack):

```bash
python defense_timeguard.py \
  --defense_config_path configs/timeguard/PEMS03_backtime_FEDformer_1212/FEDformer/TimeGuard.yaml
```

## 4. Datasets

TimeGuard is validated on three real-world datasets and put it in under `./data` folder:

- **PEMS03** (Traffic flow)
  Provided in the  repository under `./data`.
- **Weather** (U.S. climate across locations)
  Download from Time-Series-Library:
  [https://github.com/thuml/Time-Series-Library](https://github.com/thuml/Time-Series-Library)
- **ETTm1** (Electricity transformer temperature / load series)
  Download from Time-Series-Library:
  [https://github.com/thuml/Time-Series-Library](https://github.com/thuml/Time-Series-Library)
---

## Acknowledgement

- [BackTime](https://github.com/xiaolin-cs/BackTime): For its excellent work and repository, which this project builds on.
- [Time-Series-Library](https://github.com/thuml/Time-Series-Library): For TSF model implementations and dataset references.
- [BackdoorBench](https://github.com/SCLBD/BackdoorBench) and [BackdoorBox](https://github.com/THUYimingLi/BackdoorBox): For baseline defense implementation details and references.