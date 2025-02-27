---
title: Windows.OSQuery.Generic
hidden: true
tags: [Client Artifact]
---

OSQuery is an excellent tool for querying system state across the
three supported Velociraptor platform (Windows/Linux/MacOS).

You can read more about OSQuery on https://osquery.io/


```yaml
name: Windows.OSQuery.Generic
description: |
  OSQuery is an excellent tool for querying system state across the
  three supported Velociraptor platform (Windows/Linux/MacOS).

  You can read more about OSQuery on https://osquery.io/

reference:
  - https://osquery.io/
  - https://github.com/osquery/osquery

# I am not actually sure if OSQuery allows arbitrary command execution via SQL?
required_permissions:
  - EXECVE

precondition: SELECT OS From info() where OS = 'windows'

tools:
  - name: OSQueryWindows
    github_project: Velocidex/OSQuery-Releases
    github_asset_regex: windows-amd64.exe

parameters:
  - name: Query
    default: "SELECT * FROM osquery_info"

sources:
  - query: |
      LET binary <= SELECT FullPath
      FROM Artifact.Generic.Utils.FetchBinary(ToolName="OSQueryWindows")

      LET result = SELECT * FROM execve(
         argv=[binary[0].FullPath, "--json", Query],
         length=1000000)

      SELECT * FROM foreach(row=result,
      query={
         SELECT * FROM parse_json_array(data=Stdout)
      })

```
