File extension: `*.tinyenc`

File format deail:

```text
[TAG; 2 bytes; u16; BE; 1 or 2]
[LENGTH; 4 bytes; u32; BE; Length of meta data]
[META DATA; LENGTH bytes]
[ENCRYPTED_DATA; n bytes; AES/GCM]
```

| Tag | Comment         |
|-----|-----------------|
| 1   | Normal Meta     |
| 2   | Compressed Meta |


Meta format:

| Field               | Type      | Comment                                      |
|---------------------|-----------|----------------------------------------------|
| version             | String    | Constant value: `1.1`                        |
| created             | Long      | Created time, Unix Epoch in millis           |
| userAgent           | String    | User Agent, e.g. `TinyEncrypt v0.5.1@MacOS`  |
| comment             | String    | `optional` Plain text comment                |
| encryptedComment    | String    | `optional` Encrypted comment                 |
| encryptedMeta       | String    | `optional` Encrypted Meta Data               |
| pgpEnvelop          | String    | `deprecated` PGP Publickey Encrypted DataKey |
| pgpFingerprint      | String    | `deprecated` Hex(Sha256(PGP Publickey))      |
| ageEnvelop          | String    | `deprecated` PGP Publickey Encrypted DataKey |
| ageRecipient        | String    | `deprecated` age1***                         |
| ecdhEnvelop         | String    | `deprecated` KW:***                          |
| ecdhPoint           | String    | `deprecated` 02***                           |
| envelop             | String    | `deprecated` KMS Encrypted DataKey           |
| envelops            | Envelop[] | Envelop Array                                |
| encryptionAlgorithm | String    | `optional` Default `AES/GCM`                 |
| nonce               | String    | `base64` GCM Nonce                           |
| fileLength          | Long      | File Length                                  |
| fileLastModified    | Long      | File Last Modified, Unix Epoch in millis     |
| compress            | Boolean   | Compressed or Not, GZIP if `true`            |

Envelop format:

| Field        | Type   | Comment                                |
|--------------|--------|----------------------------------------|
| type         | String | Type: `kms`, `pgp`, `age`, `ecdh`, ... |
| kid          | String | Key ID                                 |
| desc         | String | `optional` Description                 |
| encryptedKey | String | `base64` Encrypted Key                 |
