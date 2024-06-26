# TLS SSL certificates
2 files are expected here
* `ca.key` - the private key
* `ca.crt` - the public certificate

## How to generate the certificates
See this [StackOverflow article](https://stackoverflow.com/questions/10175812/how-to-generate-a-self-signed-ssl-certificate-using-openssl)

### Inspect the signed certificate
```bash
openssl x509 -noout -text -in ca.crt
```

### Examine the private key
```bash
cat ca.key
```
