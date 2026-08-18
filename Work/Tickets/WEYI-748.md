---
created: 2026-08-17
summary: Add language id and client id to the outsource request, defaulted to ASL and Voyce's client id
---
# Description
Enhance the Outsource API request model to include `LanguageId` and `ClientId` fields. These fields should be automatically populated with default values to ensure all outsource interactions are associated with the correct language and client.


# Questions
1. What is voyces client id? None of the scripts I have insert it into that table.
2. Why do we default to ASL?