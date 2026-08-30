# 🛡️ PQ-GAPR: Post-Quantum Gateway-Assisted Key-Insulated Ratchet Simulator

A high-performance cryptographic benchmark and simulation engine evaluating **PQ-GAPR (Post-Quantum Gateway-Assisted Key-Insulated Ratchet)** against NIST-standardized Post-Quantum Cryptography (**ML-KEM-512 / ML-KEM-768 / FIPS 203**), Chunked Post-Quantum Ratchets (**Signal SPQR**), and Classical baselines (**ECDHE / Static PSK**) on resource-constrained IoT platforms.

---

## 📌 Key Architectural Features
- **Key-Insulated Lattice Delegation:** Instantiates the formal lineage of Key-Insulated Cryptography (Dodis et al.) for constrained LPWAN nodes. The Edge Gateway acts as a cryptographic helper executing ML-KEM key encapsulations with the cloud and injecting post-quantum update tokens ($SS_{\text{fresh}}$) into the node.
- **Hardware TRNG Ratchet Mixing:** The IoT node mixes fresh on-device True Random Number Generator entropy ($N_{\text{node},E}$) alongside the gateway's quantum entropy ($CK_{E+1} = \text{HKDF}(CK_E, SS_{\text{fresh}}, N_{\text{node},E})$), achieving true Post-Compromise Security (PCS) under transient state compromise while keeping the gateway strictly oblivious to payload keys.
- **Zero Asymmetric Overhead on Node:** Reduces peak MCU stack RAM to **384 Bytes** (**87.7% reduction vs. ML-KEM-512** and **93.4% reduction vs. Signal SPQR**).
- **Zero MTU Packet Fragmentation:** Retains a compact 30-byte telemetry overhead, eliminating link fragmentation and ensuring strict statutory compliance with the **LoRaWAN EU868 1% sub-band duty-cycle regulations**.

---

## 📊 Empirical Testbed Baseline
- **Target MCU:** ARM Cortex-M4 (STM32L476 @ 64MHz)
- **Link-Layer Network:** LoRaWAN EU868 DR0 (51-Byte MTU / SF12)
- **Power Source:** CR2032 Lithium Coin Cell (225 mAh @ 3.0V / 2,430 Joules)

---

## 🚀 Quickstart

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Launch the Interactive Simulator
```bash
streamlit run app.py
```

---

## 📈 Comprehensive Benchmark Summary (LoRaWAN DR0 / SF12)

| Cryptographic Protocol | Post-Quantum Security | Peak Stack RAM | Handshake Frames (TX↑/RX↓) | Peak Handshake Energy | Battery Life (Hourly Metering) | Battery Life (Daily Deployment) |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **⭐ Proposed: PQ-GAPR** | **128-bit Post-Quantum** | **384 B** | **3 (1↑ / 2↓)** | **383.9 mJ** | **209.2 Days** | **4.23 Years (1,545 d)** |
| **Direct PQC: ML-KEM-512** | 128-bit Post-Quantum | 3,120 B | 43 (21↑ / 22↓) | 7,508.2 mJ | 162.6 Days | **3.88 Years (1,417 d)** |
| **Direct PQC: ML-KEM-768** | 192-bit Post-Quantum | 4,280 B | 61 (29↑ / 32↓) | 10,723.6 mJ | 147.1 Days | **3.73 Years (1,363 d)** |
| **Hybrid PQC: Signal SPQR** | 128-bit Post-Quantum | 5,800 B | 44 (22↑ / 22↓) | 7,888.1 mJ | 108.7 Days | **3.29 Years (1,200 d)** |
| **Classical: ECDHE (secp256r1)** | 0-bit (Broken) | 2,048 B | 4 (2↑ / 2↓) | 641.7 mJ | 209.3 Days | **4.23 Years (1,545 d)** |
| **Baseline: Static PSK (AES-128)** | 128-bit Grover | 256 B | 0 | 0.0 mJ | 215.1 Days | **4.26 Years (1,558 d)** |

---

## 🔬 Key Evaluation Takeaways
1. **RAM Footprint:** PQ-GAPR requires only **384 B** of RAM—an **87.7% reduction vs. ML-KEM-512** (3,120 B), a **91.0% reduction vs. ML-KEM-768** (4,280 B), and a **93.4% reduction vs. Signal SPQR** (5,800 B).
2. **Operational Battery Longevity:** In daily reporting deployments, PQ-GAPR achieves **4.23 Years**, operating within 0.7% of the unencrypted Static PSK baseline (4.26 Years) while providing full post-quantum forward secrecy and post-compromise self-healing.
3. **Over-the-Air Resilience:** Direct ML-KEM requires 43–61 fragmented frames over SF12 airtime ($69\text{--}98\text{ s}$ radio active time), while PQ-GAPR completes in a compact 3-frame exchange.
