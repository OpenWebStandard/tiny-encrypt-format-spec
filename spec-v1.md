# Tiny Encrypt Format Spec

File format:

```
File            ::= Magic Format_Version Tlv+
Magic           ::= 0xECF0
Format_Version  ::= 2bytes[BE]
Tlv             ::= Tlv_Tag Tlv_Length_Tag Tlv_Length Tlv_Body
Tlv_Tag         ::= 2bytes[BE]
Tlv_Length_Type ::= 1byte
Tlv_Length      ::= 4bytes[BE]
Tlv_Body        ::= Tlv_Length bytes binary | Chunks
Chunks          ::= Chunk_Body* | Chunk_End
Chunk_Body      ::= 4bytes[BE] bytes
Chunk_End       ::= 0x00000000
```

Format_Version
Constantly `0x01`

Tlv_Tag
```
0x0000 - reserved
0x0001 - file meta
```

Tlv_Length_Type
```
0x00 - reserved
0x01 - assigned length
0x02 - chunked
```

File meta is JSON format, sample
```
{
  "userAgent": "tiny_encrypt_rs/1.0 macos"
  "envelops": [
    { "format": "", "id": "", "fingerprint": "", "envelop": "" }
  ]
}
```


