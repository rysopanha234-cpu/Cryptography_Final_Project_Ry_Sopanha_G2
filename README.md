<div align="center">

```
 ┌────────┐                                          ┌────────┐
 │ CLIENT │ ══ a3 f9 07 5c e1 b8 2d 90 4e 6b ═══════▶│ SERVER │
 └────────┘               ▲                          └────────┘
                          │
                   ┌─────────────┐
                   │  ATTACKER   │   "all I see is noise."
                   └─────────────┘
```

# 🛡️ SecureAPI 🛡️

### *Encrypt it. Attack it. Prove it.*

![Language](https://img.shields.io/badge/LANGUAGE-PYTHON-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Cipher](https://img.shields.io/badge/CIPHER-AES--256--GCM-2ECC71?style=for-the-badge)
![Key Exchange](https://img.shields.io/badge/KEY%20EXCHANGE-RSA--OAEP-E8590C?style=for-the-badge)
![Server](https://img.shields.io/badge/SERVER-FASTAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![Status](https://img.shields.io/badge/STATUS-IN%20DEVELOPMENT-F1C40F?style=for-the-badge)

**Design and Implementation of a Hybrid Cryptographic System for Secure API Communication**

*Cryptography Final Project · CADT · Year 3 Cybersecurity*

</div>

---

## ⚡ Overview

APIs move data between a client and a server, but someone in the middle can **read** it, **change** it, or **copy a valid request and send it again** (a replay attack).

SecureAPI is a Python system that protects API traffic with cryptography, then **attacks itself on purpose** to show the protection really works.

| Problem | Defense | Technique |
|---------|---------|-----------|
| Attacker reads the data | Encrypt every request and response | AES-256-GCM |
| Attacker changes the data | Authentication tag rejects any edit | AES-GCM tag |
| Attacker replays a request | Timestamp window + unique request ID | Replay protection |
| How to share the AES key safely | Wrap the key with the server's public key | RSA-OAEP |

## 🔄 How It Works

```
1. Client  ──── "give me your public key" ────────▶  Server
2. Client  ◀─── RSA public key ───────────────────   Server
3. Client makes a random AES-256 session key
4. Client  ──── AES key locked with RSA-OAEP ─────▶  Server (unlocks with private key)
5. Both sides now share the AES key
6. Client  ──── AES-GCM(request + time + ID) ─────▶  Server
7. Client  ◀─── AES-GCM(response) ────────────────   Server
```

## 🎯 Attack Demo (target output)


```
$ python attacks/attacker.py

[ replay attack ]        ......  REJECTED
[ tampering attack ]     ......  REJECTED
[ expired timestamp ]    ......  REJECTED
[ wrong key ]            ......  REJECTED
```

## 🚀 Installation

1. Clone the repository

```
git clone https://github.com/rysopanha234-cpu/Cryptography_Final_Project_Ry_Sopanha_G2.git
cd secureapi
```

2. Create a virtual environment

```
# Windows
python -m venv .venv
.venv\Scripts\activate

# Linux / Mac
python3 -m venv .venv
source .venv/bin/activate
```

3. Install dependencies

```
pip install -r requirements.txt
```

## 🧪 Usage

## 📂 Project Structure

```
secureapi/
├── secureapi/
│   ├── aes_gcm.py       # AES-256-GCM encrypt / decrypt
│   ├── rsa_keys.py      # RSA key generation, OAEP wrap / unwrap
│   ├── signatures.py    # RSA-PSS sign / verify
│   ├── replay.py        # timestamp and request ID checks
│   ├── server.py        # FastAPI server
│   └── client.py        # client
├── attacks/
│   └── attacker.py      # attack demo
├── tests/               # pytest tests
├── docs/                # architecture and threat model
├── keys/                # generated keys (never committed)
├── requirements.txt
└── README.md
```

## 📦 Dependencies

| Library | Used for |
|---------|----------|
| `cryptography` | AES-GCM, RSA-OAEP, RSA-PSS |
| `fastapi` | the server |
| `uvicorn` | runs the server |
| `requests` | client HTTP calls |
| `httpx` | test client for FastAPI |
| `pytest` | automated tests |

## ⚠️ Limitations

SecureAPI is a learning project that demonstrates how cryptographic building blocks work together. It is not a replacement for HTTPS/TLS, and real deployments should still use TLS.

## 👤 Author

**Ry Sopanha**
Cybersecurity, Year 3, CADT · Cryptography Final Project

<div align="center">

*Crafted with caffeine, nonces, and way too many hex bytes.*

</div>