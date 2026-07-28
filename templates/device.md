---
codename:
type:            # server | laptop | desktop | mobile | storage | cloud-service
status:          # active | idle | retired
os:
owner:           # self-hosted | rented | institutional | third-party
root-access:     # true | false
vault-replica:   # true | false — whether a Syncthing copy of this Vault lives here
hosts:           # reachable addresses (private name / public IP / jump host)
  -
last-verified:   # YYYY-MM-DD
---

# <codename>

<!-- One line: what this device is and why it exists. -->

## Access

<!-- SSH config block, jump host, 2FA requirements.
     Credentials may be inlined here: this file is never tracked by Git. -->

## Hardware

<!-- CPU / GPU / memory / disk. Delete this section if not applicable. -->

## Services

<!-- One row per deployed service. Delete this section if the device runs none.
     "Managed by" is the systemd unit name or the docker compose file path. -->

| Service | Purpose | Endpoint | Managed by | Notes |
|---|---|---|---|---|
|  |  |  |  |  |

## Hosted Assets

<!-- Assets the Vault *records* (rather than owns) on this device.
     Link back to the corresponding entries under assets/. -->

## Maintenance Log

<!-- Changes, pitfalls, renewal deadlines. -->
