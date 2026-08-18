---
created: 2026-08-17
summary: Add language id and client id to the outsource request, defaulted to ASL and Voyce's client id
source: https://cloudbreak.atlassian.net/browse/WEYI-748?referrer=quick-find&search_id=98cc1de2-cb55-4fcf-a63c-00c99cf02d01
---
# Description
Enhance the Outsource API request model to include `LanguageId` and `ClientId` fields. These fields should be automatically populated with default values to ensure all outsource interactions are associated with the correct language and client.

# Requirements
#### 1. Update Outsource Request Model
Add the following fields to the outsource request:
- LanguageId
- ClientId
#### 2. Default Values
If these fields are not provided by the caller:
- LanguageId defaults to **ASL**.
- ClientId defaults to **Voyce's client ID**.
#### 3. Interaction Creation
When creating the outsource interaction:
- Use the resolved `LanguageId` and `ClientId`.
- Persist these values with the interaction so downstream services use the correct context.
# Acceptance Criteria
- The Outsource API request supports LanguageId and ClientId.
- Requests without these fields continue to work without modification.
- LanguageId defaults to **ASL** when omitted.
- ClientId defaults to **Voyce's client ID** when omitted.
- The resolved values are stored with the created outsource interaction.
- Existing integrations remain backward compatible.
# Questions
1. What is voyces client id? None of the scripts I have insert it into that table.
	1. You have to fetch it using a person id.
```sql
select d.Id as VoyceClientId, 
	d.ClientName as VoyceClientName, 
	a.Name as VoyceClientUserName, 
	b.Id as VoyceClientUserId  
from WEYI.dbo.Person a  
inner join WEYIMgr.dbo.ClientUser b on a.Id = b.PersonId  
inner join WEYIMgr.dbo.Appuser c on 
	b.Id = c.SourceId and c.UserType = 'ClientUser'  
inner join WEYIMgr.dbo.Client d on c.ClientId = d.Id  
where a.Id = @pPersonId
```
1. Why do we default to ASL?