---
title: "[WEYI-897] V2M - Report of Data Points Included on Customer Invoice Reports"
source: "https://cloudbreak.atlassian.net/browse/WEYI-897?focusedCommentId=92314&sourceType=mention&page=com.atlassian.jira.plugin.system.issuetabpanels%3Acomment-tabpanel&xpis=eyJicmlkZ2UiOiJub3RpZmljYXRpb25EcmF3ZXIiLCJpZCI6IjE3OTE1ODM3Mzk1ODIiLCJzb3VyY2UiOiJqaXJhIn0%3D#comment-92314"
author:
published:
created: 2026-10-09
description:
tags:
  - "clippings"
---
### Description:

Create a report showing **all data points included on each customer’s invoice**. The report should provide a clear view of invoice data requirements by customer.

### Acceptance Criteria:

- One row per customer
- Include customer name/ID
- List all data points included on that customer’s invoice
- Deliver in an exportable format such as Excel or CSV

##### Xiang Xu

`sp_InvoiceRpt_Hospital_Secure` In this stored procedure, take a look at each specific condition with CompanyCode and summarize what action we did for each customized customer.  
