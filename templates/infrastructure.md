---
codename:
type:            # server | laptop | desktop | mobile | storage
                 # | cloud-service | domain | account
status:          # active | idle | retired
os:              # omit for entries that are not machines
owner:           # self-hosted | rented | institutional | third-party
root-access:     # true | false
vault-replica:   # true | false — whether a Syncthing copy of this Vault lives here
hosts:           # reachable addresses (private name / public IP / jump host / domain)
  -
last-verified:   # YYYY-MM-DD
---

# <codename>

<!-- One line: what this entry is and why the Vault holds it. -->

## Access

<!-- SSH config block, jump host, 2FA requirements, control panel URL.
     Credentials may be inlined here: this file is never tracked by Git. -->

## Hardware

<!-- CPU / GPU / memory / disk. Delete this section if not applicable. -->

## Services

<!-- One row per deployed service, or per DNS record for a domain.
     "Managed by" is the systemd unit name or the docker compose file path.
     Delete this section if the entry runs none. -->

| Service | Purpose | Endpoint | Managed by | Notes |
|---|---|---|---|---|
|  |  |  |  |  |

## Hosted Assets

<!-- Assets the Vault *records* (rather than owns) here.
     Link back to the corresponding entries under assets/.
     Delete this section for entries that cannot hold content. -->

## Maintenance Log

<!-- Changes, pitfalls, renewal and billing deadlines. -->
