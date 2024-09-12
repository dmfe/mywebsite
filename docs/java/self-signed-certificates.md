---
tags:
    - java
    - ssl
    - security
    - certificate
---

# Self-Signed Certificates

## Example of generating Self-Singned Certificate for localhost

```bash title="Generate root certificate with private key"
$ openssl req -x509 -sha256 -days 3653 -newkey rsa:2048 -keyout root_ca.key -out root_ca.crt
```

Output:
```bash
.....................+..+......+.+...+............+......+...+..+...+.........+...+......
.....+.............+..+.............+......+.....+++++++++++++++++++++++++++++++++++++++
Enter PEM pass phrase:
Verifying - Enter PEM pass phrase:
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:RU
State or Province Name (full name) [Some-State]:Nizhegorodskaya Oblast                          
Locality Name (eg, city) []:Nizhniy Novgorod
Organization Name (eg, company) [Internet Widgits Pty Ltd]:dmfe.net 
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:ROOT CA
Email Address []:
```

```bash title="Generate private key for application"
$ openssl genrsa -out localhost.key 2048
```

```bash title="Cerate request for certicifate signing for previosly generated application private key"
$ openssl req -key localhost.key -new -out localhost.csr
```

Output:
```
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:RU
State or Province Name (full name) [Some-State]:Nizhegorodskaya Oblast
Locality Name (eg, city) []:Nizhniy Novgorod
Organization Name (eg, company) [Internet Widgits Pty Ltd]:dmfe.net
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:localhost
Email Address []:

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
```

Creating new file with extensions:
```text title="localhost.ext"
authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
subjectAltName=@alt_names
[alt_names]
DNS.1=localhost
IP.1=127.0.0.1
```

```bash title="Sign application certificate with root certificate"
$ openssl x509 -req \
    -CA root_ca.crt \
    -CAkey root_ca.key \
    -in localhost.csr \
    -out localhost.crt \
    -days 365 \
    -CAcreateserial \
    -extfile localhost.ext
```

```bash title="Create chain of certificates"
$ cat localhost.crt root_ca.crt > localhost_full.crt
```

```bash title="Export certificate and private key to pkcs12 keystore"
$  openssl pkcs12 -export \
    -in localhost_full.crt \
    -inkey localhost.key \
    -name localhost \
    -out localhost.p12
```

Here is a simple spring boot app, which is using http2 and demonstrate working with self-signed certificate: [sandbox-spring-boot](https://github.com/dmfe/sandbox-spring-boot)

