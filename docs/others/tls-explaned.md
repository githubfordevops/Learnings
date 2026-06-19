# Understanding TLS Certificates: CA Certificate, Server Certificate, and Client Certificate

TLS can seem complicated because there are **three different certificates** often involved:

1. **CA Certificate (cacert)** – "Who do I trust?"
2. **Server Certificate (servercert)** – "I am the server."
3. **Client Certificate (clientcert)** – "I am the client."

Let's build it from first principles.

---

# 1. Why do we need certificates?

Imagine you're opening your bank's website.

How do you know:

* The website is really the bank?
* Not an attacker pretending to be the bank?

TLS solves this using certificates.

---

# 2. Certificate Authority (CA)

A **CA** is a trusted third party that signs certificates.

Examples:

* DigiCert
* Let's Encrypt
* GlobalSign

Think of the CA as a government office issuing passports.

---

## CA creates:

### Private Key

```text
ca.key
```

### CA Certificate

```text
ca.crt
```

The CA certificate contains:

```text
CA Public Key
CA Name
Signature
```

---

# 3. Server Certificate

Suppose your server is:

```text
api.company.com
```

The server generates:

```text
server.key
```

(private key)

and a certificate request.

The CA signs it and produces:

```text
server.crt
```

Now the server has:

```text
server.key
server.crt
```

---

# 4. What does the client have?

The client needs:

```text
ca.crt
```

only.

Because the client trusts the CA.

---

# 5. One-way TLS (most common)

This is what happens when you open HTTPS websites.

```text
Client -------> Server
```

The client authenticates the server.

The server does NOT authenticate the client.

---

## Handshake

### Step 1

Client connects

```text
Hello Server
```

---

### Step 2

Server sends:

```text
server.crt
```

---

### Step 3

Client checks:

```text
Was this certificate signed by a CA I trust?
```

Using:

```text
ca.crt
```

---

### Step 4

If validation succeeds:

```text
This is really api.company.com
```

The client proceeds.

---

### Diagram

```text
Client
  |
  | trusts
  v
ca.crt
  ^
  |
signed
  |
server.crt ---- server.key
       |
       |
     Server
```

---

# 6. What is Mutual TLS (mTLS)?

Sometimes the server also wants to know:

```text
Who is this client?
```

Examples:

* Microservices
* 5G NFs
* Service Mesh
* Envoy ↔ xDS
* NRF ↔ UDM

Then both sides authenticate each other.

---

### Diagram

```text
Client <------> Server
```

Both exchange certificates.

---

# 7. Client Certificate

The client generates:

```text
client.key
```

CA signs it:

```text
client.crt
```

Now the client has:

```text
client.key
client.crt
```

---

# 8. mTLS Handshake

### Client → Server

```text
Client Hello
```

---

### Server → Client

```text
server.crt
```

---

### Client validates server

Using:

```text
ca.crt
```

---

### Server asks:

```text
Show me your certificate
```

---

### Client sends:

```text
client.crt
```

---

### Server validates client

Using:

```text
ca.crt
```

---

### Connection established

Both trust each other.

---

### Diagram

```text
             CA
             |
      signs  |  signs
             |
      +------+------+
      |             |
server.crt    client.crt
server.key    client.key
      |             |
      +------+------+
             |
           TLS
```

---

# 9. Why are private keys important?

Certificates are public.

Anyone can see:

```text
server.crt
```

The secret is:

```text
server.key
```

During the handshake, the server proves:

```text
I possess the private key
```

without revealing it.

If someone steals:

```text
server.key
```

they can impersonate the server.

---

# 10. Typical file mapping

| File       | Purpose                |
| ---------- | ---------------------- |
| ca.crt     | Trusted CA certificate |
| ca.key     | CA private key         |
| server.crt | Server certificate     |
| server.key | Server private key     |
| client.crt | Client certificate     |
| client.key | Client private key     |

---

# 11. In Kubernetes / Service Mesh

A pod running Envoy might have:

```text
/etc/certs/
   ca.crt
   tls.crt
   tls.key
```

where:

```text
ca.crt  -> CA certificate
tls.crt -> server/client certificate
tls.key -> private key
```

Envoy uses:

```yaml
validation_context:
  trusted_ca:
    filename: /etc/certs/ca.crt
```

to validate peers.

---

# 12. Real-world analogy

Think of an airport.

### CA

Government passport office.

### Server Certificate

Server's passport.

### Client Certificate

Client's passport.

### Private Key

Secret biometric information proving the passport belongs to that holder.

### TLS

Airport officer checks the passport.

### mTLS

Both parties check each other's passports.

---

# Quick Summary

## One-way TLS

```text
Client trusts CA
CA signs Server Cert

Client --> verifies Server
```

### Files involved

```text
Client:
   ca.crt

Server:
   server.crt
   server.key
```

---

## Mutual TLS (mTLS)

```text
Client trusts CA
Server trusts CA

CA signs both certificates

Client verifies Server
Server verifies Client
```

### Files involved

```text
Client:
   client.crt
   client.key
   ca.crt

Server:
   server.crt
   server.key
   ca.crt
```

This mTLS model is exactly what you'll commonly see between 5G core network functions such as UDM, NRF, and service-mesh components like Envoy.
