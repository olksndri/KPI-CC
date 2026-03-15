# Lab Report: Symmetric Ciphers and Cryptanalysis

## Overview

This laboratory work covers the implementation and cryptanalysis of three symmetric encryption algorithms: **Caesar**, **Vigenere**, and **Vernam** ciphers. The goal is to evaluate their cryptographic strength against **Brute Force** and **Frequency Analysis** attacks.

## 1. Caesar Cipher

* **Mechanism:** Monoalphabetic substitution with a fixed shift.
* **Cryptanalysis:**
* **Brute Force:** Successfully recovered the key (Shift: 6) in $O(n)$ time, where $n=33$ (Ukrainian alphabet).
* **Frequency Analysis:** Used Chi-squared test to compare text distribution with standard Ukrainian frequencies. Effective even on short phrases.



## 2. Vigenere Cipher

* **Mechanism:** Polyalphabetic substitution using a keyword.
* **Optimization Choice:**
* A 3-letter key (**"тим"**) was used.
* **Mathematical Justification:** For the Ukrainian alphabet ($A=33$), a 9-letter key results in $33^9 \approx 4.6 \times 10^{13}$ combinations. At a rate of $1,000,000$ keys/sec, decryption would take $\approx 1.47$ years.
* A 3-letter key results in $33^3 = 35,937$ combinations, which is processed instantly.


* **Cryptanalysis:**
* **Hybrid Attack:** Combined statistical frequency analysis (Top-3 candidates) with `control_word` validation.
* **Observation:** Frequency analysis failed on the shortest string due to insufficient statistical data but succeeded on longer texts.



## 3. Vernam Cipher (One-Time Pad)

* **Mechanism:** Key length equals message length. Key is generated using `std::mt19937` (PRNG).
* **Cryptanalysis:**
* **Brute Force:** Programmatically aborted with the status `impossible (key too long)`. For a 30-character message, the complexity is $33^{30}$, exceeding practical computation limits.
* **Frequency Analysis:** Failed as expected. Since the key is random and non-repeating, the ciphertext distribution is uniform (entropy is maximum), providing **Perfect Secrecy**.
