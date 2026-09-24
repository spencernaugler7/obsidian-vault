---
title: "[WEYI-285] Title: Ensure Client Updates in Core System Use UTC Timestamps"
source: "https://cloudbreak.atlassian.net/browse/WEYI-285"
author:
published:
created: 2026-09-23
description:
tags:
  - "clippings"
---
### **Description**

Client updates in the Core system are currently using **Eastern Time (EST)** for the LastUpdated timestamp. This caused a recent issue where a client update was **not applied in VIP**, because the LastUpdated time appeared **earlier than the CreateTime**, which is stored in **UTC**.  

### **Background Example**
- Original client name: Threshold
- Client renamed to: Thresholds – Crisis Response
- VIP filters out clients with names identical to the company name — so the rename should have made the client visible.
- However, since LastUpdated was in **EST** and CreateTime was in **UTC**, the update was rejected.
- Manual re-push by Xiang resolved this specific case.  
    this issue is in WEYI-221

### **Acceptance Criteria**
- Update the Core system to use **UTC timestamps** for LastUpdated and other relevant fields
- Add validation or logging to flag future cases where LastUpdated < CreateTime.
- Create Client then update client name, the updates should be able to push VIP