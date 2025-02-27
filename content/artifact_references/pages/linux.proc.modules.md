---
title: Linux.Proc.Modules
hidden: true
tags: [Client Artifact]
---

Module listing via /proc/modules.

```yaml
name: Linux.Proc.Modules
description: Module listing via /proc/modules.
parameters:
  - name: ProcModules
    default: /proc/modules

sources:
  - precondition: |
      SELECT OS From info() where OS = 'linux'

    query: |
        SELECT Name,
          atoi(string=Size) As Size,
          atoi(string=UseCount) As UseCount,
          parse_string_with_regex(regex='''(?P<UsedBy>.*),''', string=UsedBy).UsedBy AS UsedBy,
          Status, 
          Address
        FROM split_records(
           filenames=ProcModules,
           regex='\\s+',
           columns=['Name', 'Size', 'UseCount', 'UsedBy', 'Status', 'Address'])

```
