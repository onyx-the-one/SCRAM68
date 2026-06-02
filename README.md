# SCRAM68
**Stream Cipher Routine for Algol Machines**

SCRAM68 is a transput utility for the encipherment and authentication of sequential data sets. Written in **ALGOL 68 (Revised Report)**, it implements a 256-bit ChaCha stream cipher coupled with an HMAC-SHA256 integrity check.

## Synopsis

```sh
a68g scram68.a68 <-e|-d> <passphrase> <in_file> <out_file>
```

* **`-e`** : Encipher data set (yields `CHCA` header + ciphertext + MAC)
* **`-d`** : Decipher and verify data set

## Notes on Operation

1. **Entropy:** The supervisor must permit read access to `/dev/urandom` for initialization vectors.
2. **Core Memory:** Allocation is currently proportional to the input data set size. Caution is advised when processing large spools.
3. **Transput:** Ensure 8-bit byte transput capabilities on the host terminal.
