+++
title = "Socratic Seminar #13"
date = 2026-07-25
template = "post.html"
[extra]
+++

## Welcome to BitDevsUyo's Thirteenth Socratic Seminar!

**Thank you** to our sponsor [Btrust](https://www.btrust.tech/) 

### 📍Details
- **Date**: July 25, 2026
- **Time**: 14:00- 16:00
- **Location**: CafeOne UYO, 162 Oron Road, Uyo ([Map](https://www.google.com/maps/dir//162+Oron+Rd,+Ewet+Housing+Estate,+Uyo+520102,+Akwa+Ibom/@5.0200907,7.8685155,12.26z/data=!4m8!4m7!1m0!1m5!1m1!1s0x105d575ff4662ecf:0x7887f2f48f1d4d29!2m2!1d7.9378991!2d5.0195906?entry=ttu&g_ep=EgoyMDI1MDUxNS4wIKXMDSoASAFQAw%3D%3D))


### Agenda

### <strong>1. Digital Signature Fundamentals & Functional Flow</strong>
- [Digital Signatures (ECDSA)](https://github.com/bitcoinbook/bitcoinbook/blob/develop/ch04_keys.adoc)
- **High-Level Signature Function**:
  - `Signature = Sign(Hash(Message), Private_Key)`
- **Verification Function**:
  - `Verify(Message, Signature, Public_Key) -> True / False`

### <strong>2. Practical Math Breakdown (Step-by-Step Whiteboard Example)</strong>
- **Alice's Setup**:
  - Private Key (x) = 3
  - Generator (G) = 5
  - Public Key (Xg) = x * G = 3 * 5 = 15
  - Private Nonce (k) = 7
  - Public Nonce (kG) = k * G = 7 * 5 = 35
  - Message Challenge (e) = 11

- **Signing Process**:
  - Formula: `S = k + (e * x)`
  - Calculation: `S = 7 + (11 * 3) = 7 + 33 = 40`
  - Output Signature: `S = 40`

- **Verification Process**:
  - Left-Hand Side: `S * G = 40 * 5 = 200`
  - Term 2: `e * Xg = 11 * 15 = 165`
  - Verify Equation: `S * G == kG + (e * Xg)`
  - Calculation Check: `200 == 35 + 165`
  - Result: `200 == 200` (Signature Verified!)

### <strong>3. ECDSA Mathematics: Signing Step-by-Step</strong>
- [Generating a Signature (r, s)](https://github.com/bitcoinbook/bitcoinbook/blob/develop/ch04_keys.adoc)
- **Step 1: Message Digest**: Compute `z = SHA256(SHA256(message))`
- **Step 2: Ephemeral Nonce**: Select random secret scalar `k`
- **Step 3: Calculate r**: Compute point `R = k * G`, set `r = R.x mod n`
- **Step 4: Calculate s**: Compute `s = k^-1 * (z + r * d) mod n`
- **Signature Output Pair**: `(r, s)`

### <strong>4. ECDSA Mathematics: Verification Step-by-Step</strong>
- [Signature Verification](https://github.com/bitcoinbook/bitcoinbook/blob/develop/ch04_keys.adoc)
- **Step 1: Compute Inverse**: `w = s^-1 mod n`
- **Step 2: Compute Scalar Multipliers**:
  - `u1 = z * w mod n`
  - `u2 = r * w mod n`
- **Step 3: Reconstruct Verification Point**: `P = (u1 * G) + (u2 * Q)`
- **Verification Rule**: Signature is valid if `P.x mod n == r`

### <strong>5. Nonce Security & Practical Vulnerabilities</strong>
- [Nonce Reuse and Why It's Dangerous](https://github.com/bitcoinbook/bitcoinbook/blob/develop/ch04_keys.adoc)
- **Private Key Extraction from Nonce Reuse**:
  - `k = (z1 - z2) / (s1 - s2) mod n`
  - `d = ((s1 * k) - z1) / r mod n`
- **Deterministic Nonces (RFC 6979)**: `k = HMAC-SHA256(private_key, message_hash)`
- **Low-s Rule (BIP 62)**: Require `s <= n / 2` to prevent signature malleability

---
## 🏛 House Rules  
- Follow [Chatham House Rule](https://www.chathamhouse.org/about-us/chatham-house-rule)  
- No photos, videos, or recordings  
- Keep the space clean  
- [Learn about BitDevs](/about/)  
- Have ideas for our next seminar? [Suggest topics here](/about/find-topics)
