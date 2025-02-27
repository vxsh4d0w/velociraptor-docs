---
title: Windows.EventLogs.Cleared
hidden: true
tags: [Client Artifact]
---

Extract Event Logs related to EventLog clearing
- Security Log  - EventID 1102
- System Log - EventID 104


```yaml
name: Windows.EventLogs.Cleared
author: Matt Green - @mgreen27

description: |
  Extract Event Logs related to EventLog clearing
  - Security Log  - EventID 1102
  - System Log - EventID 104

reference:
  - https://attack.mitre.org/versions/v6/techniques/T1070/

type: CLIENT

parameters:
  - name: TargetGlob
    default: C:\Windows\System32\Winevt\Logs\{System,Security}.evtx
  - name: DateAfter
    type: timestamp
    description: "search for events after this date. YYYY-MM-DDTmm:hh:ssZ"
  - name: DateBefore
    type: timestamp
    description: "search for events before this date. YYYY-MM-DDTmm:hh:ssZ"
  - name: SearchVSS
    description: "Add VSS into query."
    type: bool

sources:
  - query: |
      SELECT
        EventTime,
        if(condition= EventID = 1102,
                then= Channel,
                else= UserData.LogFileCleared.Channel
            ) as ClearedLog,
        Message,
        UserData.LogFileCleared.SubjectDomainName + "\\" + UserData.LogFileCleared.SubjectUserName as Username,
        if(condition= EventID = 104,
                then= UserSID,
                else= UserData.LogFileCleared.SubjectUserSid
            ) as UserSID,
        dict(
            EventTime=EventTime,
            Computer=Computer,
            Channel=Channel,
            EventID=EventID,
            EventRecordID=EventRecordID,
            FullPath=FullPath,
            UserData=UserData
        ) as EventData
      FROM Artifact.Windows.EventLogs.EvtxHunter(EvtxGlob=TargetGlob,
            ChannelRegex='^(Security|System)$',
            IdRegex='^(1102|104)',
            IocRegex='clear|cleared',
            DateAfter=DateAfter,
            DateBefore=DateBefore,
            SearchVSS=SearchVSS)

```
