# SCRAM68
**Stream Cipher Routine for Algol Machines**

SCRAM68 is a file encryption utility written in **ALGOL 68** for use with **Algol 68 Genie**. It combines a 256-bit ChaCha-style stream cipher with an HMAC-SHA256 integrity check.

## Synopsis

Install Algol 68 Genie...
For example:
```sh 
sudo apt install algol68g
```
or :
```sh 
sudo dnf install algol68g
```
then run with:

```sh
a68g scram68.a68 -- <-e|-d> <passphrase> <in_file> <out_file>
```

- `-e` — Encrypt a file.
- `-d` — Decrypt a file and verify its MAC.

## Output format

Encrypted files are written as text-safe output in this form:

```text
CHCA + hex(nonce) + hex(ciphertext) + hex(tag)
```

- `CHCA` is the file marker.
- `nonce` is 12 bytes, hex-encoded to 24 characters.
- `ciphertext` is hex-encoded.
- `tag` is the 32-byte HMAC-SHA256 output, hex-encoded to 64 characters.

This format is used because plain ALGOL 68 text transput does not safely preserve arbitrary binary bytes [file:122].

## Notes

- The program currently derives the encryption key as `SHA-256(passphrase)` [file:122].
- Nonces are generated internally with `get_rand(12)` [file:122].
- The entire input file is currently read into memory before encryption or decryption [file:122].
- Decryption aborts if MAC verification fails [file:122].

## Examples

```sh
a68g scram68.a68 -- -e hunter2 plain.txt secret.scram
a68g scram68.a68 -- -d hunter2 secret.scram recovered.txt
```

## Challenge

A sample encrypted challenge file is included separately.
