### What is DataCache?

Need to encode a file onto paper? Want a link that won't decay when it stops being hosted? Looking for an easy way to transfer small files to your phone?

**DataCache** is a minimal, offline-capable web app that encodes files into shareable URLs and decodes them back without any servers or third parties.

### How it works

**Decode:** Open a link with `#v=1.payload` to extract and download the file.

**Encode:** Drop a file (2KB max) to wrap it with metadata and generate a shareable link with a QR code.

### Manual decoding

1. Copy the payload after `#v=1.` from the URL.
2. Replace `-` with `+` and `_` with `/`, then pad with `=` until the length is a multiple of 4.
3. Run `base64 -d` to get the binary payload.
4. Extract the file data: byte 0 = version (1), bytes 1-2 = filename length (little-endian), then filename, then MIME length (LE), then MIME, then file data, last 32 bytes = SHA-256 checksum. Save everything between the MIME and the checksum as your output file.

### Security

- All processing is local.
- No data is uploaded.
- SHA-256 checksums are used.

### Links

- undack.github.io/datacache
- mdhlf4p6e3qcnksm3rno2ldespnyzm3vovcbifibhijqppslttv2g5id.onion
- datacache.losingfoc.us
