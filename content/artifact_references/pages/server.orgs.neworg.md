---
title: Server.Orgs.NewOrg
hidden: true
tags: [Server Artifact]
---

This server artifact will create a new org and assign the current
user as an admin to it.

NOTE: This artifact is only available to users with the ORG_ADMIN
permission, normally only given to users with the administrator role
while using the root org (You might need to switch to the root org
in the GUI before collecting this artifact).

After collecting this artifact, collect the `Server.Orgs.ListOrgs`
artifact and select to upload client config files. Use this org's
config to create new client MSIs for deployment.


```yaml
name: Server.Orgs.NewOrg
description: |
  This server artifact will create a new org and assign the current
  user as an admin to it.

  NOTE: This artifact is only available to users with the ORG_ADMIN
  permission, normally only given to users with the administrator role
  while using the root org (You might need to switch to the root org
  in the GUI before collecting this artifact).

  After collecting this artifact, collect the `Server.Orgs.ListOrgs`
  artifact and select to upload client config files. Use this org's
  config to create new client MSIs for deployment.

type: SERVER

parameters:
- name: OrgName

sources:
- query: |
    LET org_record <= org_create(name=OrgName)

    SELECT org_record.name as Name, org_record.id AS OrgId,
           user_create(orgs=org_record.id,
                       roles=["administrator", "org_admin"],
                       user=whoami()) AS AdminUser
    FROM scope()

```
