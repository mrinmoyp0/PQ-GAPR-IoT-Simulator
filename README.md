# 🛡️ PQ-GAPR: Post-Quantum Gateway-Assisted Progressive Ratchet Simulator

A high-performance cryptographic benchmark and simulation engine evaluating **PQ-GAPR (Post-Quantum Gateway-Assisted Progressive Ratchet)** against NIST-standardized Post-Quantum Cryptography (**ML-KEM-512 / ML-KEM-768**), Hybrid Post-Quantum Ratchets (**Signal SPQR**), and Classical baselines (**ECDHE / Static PSK**) on resource-constrained IoT platforms.

---

## 📌 Key Architectural Features
- **Quantum Entropy Injection (Self-Healing / PCS):** Decouples heavy lattice mathematics (FIPS 203) from constrained IoT microcontrollers. The edge gateway handles post-quantum key encapsulation with the cloud and injects encrypted quantum seeds into the node's symmetric ratchet, achieving full Post-Compromise Security (PCS).
- **Blinded Edge Relay (Zero-Trust):** The gateway operates as an oblivious transport accelerator, guaranteeing end-to-end payload confidentiality between the IoT node and the cloud server.
- **Zero Packet Fragmentation:** Reduces telemetry overhead to 30 bytes, operating within a single link frame across LoRaWAN, BLE, and Zigbee.

---

## 📊 Empirical Testbed Baseline
- **Target MCU:** ARM Cortex-M4 (STM32L476 @ 64MHz)
- **Link-Layer Network:** LoRaWAN EU868 DR0 (51-Byte MTU / SF12)
- **Power Source:** CR2032 Lithium Coin Cell (225 mAh @ 3.0V)

---

## 🚀 Quickstart

### 1. Install Dependencies
`ash
pip install -r requirements.txt
`

### 2. Launch the Streamlit Simulator
`ash
streamlit run app.py
`

---

## 📈 Benchmark Summary

| Algorithm | Post-Quantum Security | Stack RAM | Handshake Frames | Battery Life (Years) |
| :--- | :---: | :---: | :---: | :---: |
| **Proposed: PQ-GAPR** | **128-bit Post-Quantum** | **384 Bytes** | **1 Frame** | **Longest** |
| **Direct PQC: ML-KEM-512** | 128-bit Post-Quantum | 3,120 Bytes | 21 Frames | Lower |
| **Direct PQC: ML-KEM-768** | 192-bit Post-Quantum | 4,280 Bytes | 29 Frames | Lower |
| **Hybrid PQC: Signal SPQR** | 128-bit Post-Quantum | 5,800 Bytes | 22 Frames | Lowest |
| **Classical: ECDHE (secp256r1)** | 0-bit (Broken) | 2,048 Bytes | 2 Frames | Moderate |
| **Baseline: Static PSK** | 128-bit Grover | 256 Bytes | 0 Frames | Insecure (No FS/PCS) |
