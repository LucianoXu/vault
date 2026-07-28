---
type: record
title:
kind:            # directory | file | repository | dataset | service-data | physical
device:          # codename of the entry in devices/ (plain text, not a wikilink:
                 # devices/ lies outside the Obsidian root)
path:            # absolute path or locator on that device
size:            # approximate, e.g. 12G
access:          # how to reach it, e.g. ssh, mounted volume, https endpoint
remote:          # upstream URL if the asset is a clone or mirror; omit otherwise
backed-up:       # true | false | unknown
last-verified:   # YYYY-MM-DD — when the path was last confirmed to exist
---

# <title>

<!-- One line: what this asset is and why the Vault records it. -->

## Contents

<!-- Enough detail to decide whether the asset is worth retrieving, without retrieving it. -->

## Retrieval

<!-- The exact commands or steps to obtain or mount the asset. -->

## Notes

<!-- Anything that would surprise someone retrieving it:
     licence, size caveats, dependencies, expiry. -->
