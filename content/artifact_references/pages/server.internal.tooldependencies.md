---
title: Server.Internal.ToolDependencies
hidden: true
tags: [Client Artifact]
---

An internal artifact that defines some tool
depenencies. Velociraptor releases for offline collector


```yaml
name: Server.Internal.ToolDependencies
description: |
  An internal artifact that defines some tool
  depenencies. Velociraptor releases for offline collector

tools:
  - name: VelociraptorWindows
    url: https://github.com/Velocidex/velociraptor/releases/download/v0.6.9/velociraptor-v0.6.9-windows-amd64.exe
    serve_locally: true
    version: 0.6.9

  - name: VelociraptorWindows_x86
    url: https://github.com/Velocidex/velociraptor/releases/download/v0.6.9/velociraptor-v0.6.9-windows-386.exe
    serve_locally: true
    version: 0.6.9

  - name: VelociraptorLinux
    url: https://github.com/Velocidex/velociraptor/releases/download/v0.6.9/velociraptor-v0.6.9-linux-amd64-musl
    serve_locally: true
    version: 0.6.9

  - name: VelociraptorDarwin
    url: https://github.com/Velocidex/velociraptor/releases/download/v0.6.9/velociraptor-v0.6.9-darwin-amd64
    serve_locally: true
    version: 0.6.9

  - name: VelociraptorWindowsMSI
    url: https://github.com/Velocidex/velociraptor/releases/download/v0.6.9/velociraptor-v0.6.9-windows-amd64.msi
    serve_locally: true
    version: 0.6.9

  - name: VelociraptorWindows_x86MSI
    url: https://github.com/Velocidex/velociraptor/releases/download/v0.6.9/velociraptor-v0.6.9-windows-386.msi
    serve_locally: true
    version: 0.6.9

```
