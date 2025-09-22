# TLS Baseline Policy

**Version:** 1.0  
**Maintainer:** Web Admin Team (in consultation with Security)  
**Last Updated:** 2025-09-10  
**Applies To:** All IIS servers hosting ColdFusion and .NET applications  
**Scope:** Inbound (Server) and Outbound (Client) TLS settings via Schannel

## Objective

Define a clear, enforceable baseline for TLS protocols, cipher suites, and related cryptographic settings using IIS Crypto or equivalent tooling. Aligns with CIS Benchmarks and NIST 800-52r2.

## Server Protocols

### Enabled
- TLS 1.2
- TLS 1.3 (if supported by OS)

### Disabled
- SSL 2.0
- SSL 3.0
- TLS 1.0
- TLS 1.1
- PCT 1.0
- Multi-Protocol Unified Hello (disable unless explicitly required)

> **Note:** Only TLS 1.2 and 1.3 should be enabled. All legacy protocols must be disabled.

## Client Protocols

### Enabled
- TLS 1.2
- TLS 1.3 (if supported)

### Disabled
- SSL 2.0
- SSL 3.0
- TLS 1.0
- TLS 1.1
- PCT 1.0
- Multi-Protocol Unified Hello

> **Note:** TLS 1.0/1.1 may be temporarily enabled for outbound connections to legacy third-party services. Must be documented in <some file>.

## Ciphers

### Enabled
- AES 128/256 with GCM (e.g., `AES_128_GCM`, `AES_256_GCM`)

### Disabled
- RC2
- RC4
- DES
- 3DES
- NULL
- EXPORT-grade ciphers
- All CBC-mode ciphers (e.g., `AES_128_CBC`)

## Hashes

### Enabled
- SHA256
- SHA384
- SHA512

### Disabled
- MD5
- SHA1

## Key Exchanges

### Enabled
- ECDHE
- DHE (if required and securely configured)

### Disabled
- RSA key exchange (static RSA)
- Anonymous key exchanges

## Sunset Dates

| Component | Target Date |
|-----------|-------------|
| TLS 1.0 / 1.1 (client-side only) | 2025-12-31 |
| CBC-mode ciphers | 2025-10-31 |
| RC4 / 3DES | **Disabled immediately** |

## Discovery & Monitoring

- Enable Schannel logging in development environments to detect legacy clients
- Use packet capture (with Network/Server teams) to identify non-compliant clients
- App owners are responsible for remediating any breakages

## Exceptions

All exceptions must be documented and approved by DISO / Security.

## Enforcement

- **Infra owners** will enforce this policy using registry settings or IIS Crypto
- **App owners** must ensure compatibility and remediate any issues

## References

- [CIS Microsoft IIS Benchmark](https://www.cisecurity.org/benchmark/microsoft_iis)
- [NIST SP 800-52r2](https://csrc.nist.gov/publications/detail/sp/800-52/rev-2/final)
- [IANA TLS Cipher Suite Registry](https://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml)
