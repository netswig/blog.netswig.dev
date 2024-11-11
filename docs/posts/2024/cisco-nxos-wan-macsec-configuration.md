---
date:
  created: 2024-11-12
categories:
    - Cisco NXOS
tags: 
- CiscoNXOS
draft: true
---

# Cisco NXOS - WAN MacSec Configuration

<!-- more -->

## Configuration Example

```cisco title="WAN MacSec Configuration Example"
nx-sw-01:

feature macsec

key chain dci-02-key-01 macsec
key 01
key-octet-string [OMMITED] cryptographic-algorithm AES_128_CMAC

macsec policy dci-02-policy-01
  cipher-suite GCM-AES-XPN-128
  key-server-priority 10
  security-policy must-secure
  sak-expiry-time 3600
  
interface Ethernet1/47
  eapol mac-address broadcast-address ethertype 0x876f

nx-sw-01:

feature macsec

key chain dci-02-key-01 macsec
key 01
key-octet-string [OMMITED] cryptographic-algorithm AES_128_CMAC

macsec policy dci-02-policy-01
  cipher-suite GCM-AES-XPN-128
  key-server-priority 20
  security-policy must-secure
  sak-expiry-time 3600
  
interface Ethernet1/47
  eapol mac-address broadcast-address ethertype 0x876f
```

```cisco title="X"
x
```

## Verification


```cisco title="x"
x
```

## Summary

