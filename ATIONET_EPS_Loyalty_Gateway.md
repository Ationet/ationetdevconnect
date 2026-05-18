# ATIONET EPS Loyalty Gateway

## Overview
<img width="890" height="520" alt="image" src="https://github.com/user-attachments/assets/de840534-ae16-4423-8ba6-995092218e79" />

**EPS** (Electronic Payment System) is the middleware component that manages communication between the POS and external loyalty host systems.

**ATIONET EPS Loyalty Gateway** integrates with the EPS and acts as an intermediary layer that translates EPS loyalty messages into the format required by the Loyalty Host.

It enables communication with a Loyalty Host through its Native API, abstracting protocol and message format differences between EPS and the host system.

It can also identify the origin of the operation and redirect it to a different Loyalty Host based on its information.


## Verifone Commander Integration
- [Commander Configuration (ATIONET Host)](Commander_Config_ATIONET_Host.md)
- [Commander Configuration (External Host)](Commander_Config_External_Host.md)
- [Operation Flow](Commander_Operations.md)
