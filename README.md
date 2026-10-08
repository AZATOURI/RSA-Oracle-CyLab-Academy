# RSA Oracle — CyLab Academy

A simple Python exploit demonstrating the multiplicative property of RSA and how a vulnerable decryption oracle can be abused.

Developed while solving a cryptography CTF challenge on CyLab Academy.

## How It Works

The challenge provides an encrypted password (`password.enc`) and access to an RSA oracle that supports encryption and decryption operations.

The exploit follows these steps:

1. **Connect to the oracle** — Open a connection to the remote challenge service.
2. **Encrypt the value 2** — Obtain the RSA ciphertext corresponding to the chosen plaintext.
3. **Abuse the decryption oracle** — Multiply the encrypted password by the generated ciphertext and submit the result for decryption.
4. **Recover the password** — Process the oracle's response to extract the password.

### RSA Multiplicative Property

RSA encryption is defined as:

$$
c = m^e \bmod n
$$

For a chosen plaintext \(r=2\), its ciphertext is:

$$
c_2 = 2^e \bmod n
$$

Multiplying the original ciphertext by \(c_2\) gives:

$$
c' = c \cdot c_2 \bmod n
$$

Decrypting the modified ciphertext produces:

$$
m' = 2m \bmod n
$$

This property allows the attacker to manipulate the plaintext through the decryption oracle.

## Python Exploit

**Requirements:**

* Python 3
* pwntools
* `password.enc`

Install pwntools:

```bash
pip install pwntools
```

## Key Takeaway

This challenge demonstrates why textbook RSA is vulnerable to multiplicative manipulation when a decryption oracle exposes raw RSA decryption results.

**Lesson:** Use RSA-OAEP for secure encryption and design oracle interfaces that do not expose sensitive plaintext information.

## Disclaimer

This code is intended for educational purposes and authorized CTF environments.
