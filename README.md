# NITRO 5G-IoT Books

Course materials for the **NITRO** 5G/IoT security training track — module books, lecture
audio, lab diagrams, and the ML exercise dataset, covering attacks against a simulated 5G
mobile core and the defences against them.

All lab work targets a **local Open5GS + UERANSIM stack running in Docker**. Nothing here
should be pointed at a production or carrier network.

---

## ⚠️ Notice on these materials

These are **licensed course materials** (book chapters and recorded lectures) owned by
their respective rights holders. This repository is published for study and reference only
and is **not a redistribution channel**. The lectures and books remain under copyright; no
licence to redistribute them is granted by this repository.

If you are the rights holder and want this taken down or made private, open an issue or
contact the repository owner directly.

---

## Cloning

Media and datasets are stored with **Git LFS** (~363 MB). You need the LFS client, or you
will get 133-byte pointer files instead of real content.

```bash
# install once
git lfs install

git clone https://github.com/dr-skaragiannis/NITRO-5G-IOT-BOOKS.git
git lfs pull          # if you cloned without the LFS client
```

---

## Contents

| Path | What it is |
|---|---|
| `Module 00/` – `Module 09/` | One directory per module: book chapter (`.docx`), lecture audio (`.m4a`), diagrams (`.png`), and lab walkthroughs (`.json`) |
| `Module 09/Exercise_Dataset/exercise.csv` | ~87 MB flow dataset for the Module 08–09 ML exercises |
| `Module 09/From_Poison_to_Antidote_….ipynb` | Jupyter notebook: poisoning attack + robust model defence |
| `Module 09/Module 09.7z` | Archived copy of the Module 09 material |

### `.docx` — the books
### `.m4a` / `.mp3` — lecture audio
### `.png` — architecture and attack diagrams
### `.json` — machine-readable lab guides

Each module's `.json` file is a structured walkthrough with per-step `command`,
`expected_output`, `explanation`, and (for the CTF modules) `associated_flags`. They are
plain JSON and easy to parse, so you can drive a lab tool straight off them.

---

## Modules

| # | Topic |
|---|---|
| 00 | Introduction to Open5GS; gNB SearchList and AMF fundamentals |
| 01 | Ping and basic communication in a 5G network |
| 02 | IMSI flood attack on the 5G core network |
| 03 | Executing a custom replay attack in a 5G network |
| 04 | Reconnaissance on a 5G network |
| 05 | Changing / adding network slices in an Open5GS lab |
| 06 | Cascading effects via network slice propagation & session hijacking using IMSI spoofing |
| 07 | Docker and host escape in 5G simulations |
| 08 | NetFlow extraction and ML-IDS adversarial AI |
| 09 | Adversarial AI and model robustness |

---

## Technical stack

The labs assume the following stack is already running:

- **Open5GS** — open-source 5G mobile core (AMF, SMF, UPF, UDM, …)
- **UERANSIM** — 5G UE / gNB simulator
- **Docker Compose** — orchestrating the core, gNBs, and UEs
- **tshark / Wireshark** — packet capture, NGAP and NAS dissection
- **nmap**, **arp-scan**, **iperf3** — recon and throughput testing
- **scapy** — crafted PFCP / SCTP packets
- **Jupyter**, **pandas**, **scikit-learn** — Modules 08–09 only

---

## Modules 08–09: the exercise dataset

`Module 09/Exercise_Dataset/exercise.csv` is a labelled network-flow dataset with
`Label` / `Mapped_Label` columns plus TCP flag counters, per-protocol indicators, and
statistical aggregates (min/max/avg/std/variance, inter-arrival times).

Module 08 trains a Decision Tree ML-IDS on it, then label-flips `ICMP_FLOOD` → `Benign` to
measure Attack Success Rate. Module 09 shows the defence: `max_depth` plus
`class_weight='balanced'`, which drops ASR at 50% poisoning from **55.3% to 2.1%**.

The notebook currently fetches the dataset from
`github.com/Exercise-Dataset/Exercise_Dataset`. The CSV is **also vendored in this repo**
under `Module 09/Exercise_Dataset/`, so you can skip the clone and point your notebook at
the local copy.

---

## Attribution

Course content © its respective authors. The underlying software and tools — Open5GS,
UERANSIM, Docker, Wireshark/tshark, nmap, scapy, scikit-learn — are the property of their
respective maintainers and carry their own licences.
