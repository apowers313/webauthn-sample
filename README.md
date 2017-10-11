# Overview
This is a quick example of how to write JavaScript to use the [WebAuthn](https://w3c.github.io/webauthn/) specification. The `navigator.credentials.create` and `navigator.credentials.get` are the primary interfaces of the WebAuthn API.

The options aren't particularily smart, and normally this code would be communicating with a back-end or validating signatures -- all of that has been removed for the sake of simplicity. See [webauthn.bin.coffee](https://webauthn.bin.coffee/) for a more complete example.

Feel free to submit any questions or comments through GitHub issues.

# Secure Context
Getting access to the `navigator.credentials` interface requires that the webpage is running in a secure context -- basically either browsing to a `https` website or to `localhost`.

## Local Access
Install python, then:

> python -m SimpleHTTPServer 8000

And browse to http://localhost:8000/sample.html

## Remote Access
Install python, then:

> python simple-https-server.py

And browse to https://localhost:8443/sample.html

If you think it's weird that this repo includes a cert / private key .pem file, you can create your own using the steps below.

## Creating a SSL self-signed cert
1. openssl genrsa -des3 -out server.key 1024
1. openssl req -new -key server.key -out server.csr
1. cp server.key server.key.org
1. openssl rsa -in server.key.org -out server.key
1. openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
1. openssl x509 -outform PEM -in server.crt -out server.crt.pem
1. cat server.crt server.key > server.pem
