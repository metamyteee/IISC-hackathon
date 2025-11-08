# IISC-hackathon
# 🧠 BB84 Quantum Key Distribution Simulation

This project simulates the **Bennett-Brassard 1984 (BB84)** Quantum Key Distribution (QKD) protocol using **Qiskit**.  
It demonstrates how two parties — Alice and Bob — can securely share a cryptographic key using the principles of quantum mechanics, while detecting any eavesdropper (Eve) attempting to intercept their communication.

---

## 📘 Overview

The BB84 protocol leverages quantum physics — particularly the **no-cloning theorem** and **measurement disturbance** — to ensure that any attempt to intercept quantum information introduces detectable errors.

This simulation includes:
- A **secure communication channel** (no eavesdropping).
- An **insecure channel** where **Eve** performs an intercept-resend attack.
- **QBER (Quantum Bit Error Rate)** analysis for eavesdropper detection.

---

## ⚙️ Features

- Full implementation of **BB84 key distribution** in Qiskit.
- Configurable simulation parameters (key size, eavesdropping, etc.).
- **Batch execution optimization** for improved performance.
- Automatic **QBER calculation** and key validation.
- Comparison between **secure** and **insecure** scenarios.

---

## 🧩 BB84 Protocol Workflow

### 1. Quantum Channel (Encoding & Measurement)
- Alice randomly generates bit and basis strings.
- She encodes each bit into a qubit using:
  - **Z-basis (rectilinear):** `0 → |0⟩`, `1 → |1⟩`
  - **X-basis (diagonal):** `0 → |+⟩`, `1 → |−⟩`
- Bob measures each qubit using his own random basis choices.

### 2. Public Channel (Key Sifting)
- Bob announces his bases.
- Alice tells which bases match.
- Both discard bits where bases differ.
- The remaining bits form the **sifted key**.

### 3. Eavesdropper Detection (QBER)
- A random subset of the sifted key is compared publicly.
- The **Quantum Bit Error Rate (QBER)** is computed:
  - If QBER ≤ threshold (10%), the key is **secure**.
  - If QBER > threshold, **eavesdropping detected** — key is discarded.

---

## 🧠 Simulation Design

### 🧍 Eve: Intercept-Resend Attack
- Eve measures each qubit using a random basis.
- Resends a new qubit to Bob using her measured value.
- When Eve’s basis ≠ Alice’s, random errors occur — raising QBER.

### 🚀 Performance Optimization
- All circuits are generated, transpiled, and executed **in batch mode** using Qiskit’s **AerSimulator** for speed and efficiency.

### 🔐 Security Parameter
- `QBER_THRESHOLD = 0.10`  
  Keys exceeding this threshold are **rejected** as insecure.

---

## 📊 Results Summary

| Metric | Secure Channel (No Eve) | Insecure Channel (With Eve) |
|--------|--------------------------|------------------------------|
| Sifted Key Length | ≈ 500 bits | ≈ 500 bits |
| Errors Detected | 0 | ≈ 125 |
| QBER | 0.00 | ≈ 0.25 |
| Security Threshold | 0.10 | 0.10 |
| Outcome | ✅ Secure | ❌ Insecure (Key Discarded) |

---

## 🧾 Conclusion

The Qiskit simulation validates the **core security promise** of the BB84 protocol:
- **Secure Channel:** QBER = 0%, key accepted.
- **Insecure Channel:** QBER ≈ 25%, eavesdropping detected, key discarded.

> BB84’s security arises not from preventing eavesdropping — but from **guaranteeing its detection**.

---

## 🧠 Requirements

- Python 3.8+
- [Qiskit](https://qiskit.org/)
- NumPy
- Matplotlib (optional for visualization)

Install dependencies:

```bash
pip install qiskit numpy matplotlib
