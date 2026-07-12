### What is DataCache?

Need to encode a file onto paper? Want a link that won't decay when it stops being hosted? Looking for an easy way to transfer small files to your phone?

**DataCache** is a minimal, offline-capable web app that encodes files into shareable URLs and decodes them back without any servers or third parties.

### How it works

**Decode:** Open a link with `#v=1.payload` to extract and download the file.

**Encode:** Drop a file to compress it, wrap it with metadata, and generate a shareable link with a QR code.

### Manual decoding

1. Copy the payload after `#v=1.` from the URL.
2. Replace `-` with `+` and `_` with `/`, then pad with `=` until the length is a multiple of 4.
3. Run `base64 -d` to get the plaintext. It contains 6 lines:
   1. Version
   2. Filename
   3. MIME type
   4. Compression
   5. Data
   6. Checksum
4. Take line 5 (the data), repeat the Base64URL conversion, then run:

   ```sh
   base64 -d | gunzip > output
   ```

### Security

- All processing is local.
- No data is uploaded.
- SHA-256 checksums are used.
