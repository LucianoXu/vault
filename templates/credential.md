---
type: credential
service:         # the service or account this file unlocks
kind:            # account | api-key | bank | wallet | recovery-codes | device | identity
identifiers:     # the emails, usernames or numbers used to log in
  -
last-verified:   # YYYY-MM-DD — when the values were last confirmed to work
rotate:          # true if the secret is known to be stale or over-exposed
---

# <service>

<!-- One line: what this account is for, and anything that decides whether it still matters. -->

## 凭据

<!-- The values, one per line, in the order they are entered. Never reword a secret. -->

## 说明

<!-- Only what would surprise someone using this: which region/account of several,
     what the recovery path is, what else must be present (a device, a TAN list),
     which file elsewhere in the Vault holds the rest. -->
