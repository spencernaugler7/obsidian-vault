---
summary:
created: 2026-11-24
source: https://cloudbreak.atlassian.net/browse/WEYI-901
---
# Voyce API: Expose Transaction Transfer and Routing History

## Description

Request a Voyce API endpoint that provides the **transfer and routing history for a transaction**.

Today, when investigating a transaction, we need visibility into how the transaction moved through the Voyce platform, including its routing path and any transfers that occurred. This information should be available programmatically using the transaction identifier.

Table related for routing:
`RequestProvider`

Table related for transfer:
`RequestTransfer` (Video and Anymeeting), `RequestRerouteRequest` (OPI and Video)

Basically, you need to implement two APIs: one for Routing History and one for the Transfer Request Chain.
1. Routing History
	The routing history should include the following fields:
	- RequestId
	- ProviderId
	- ProviderName
	- ProviderEmail
	- ProviderCompanyName
	- RequestSentTime
	- AcceptedTime
	- ConfirmedTime
2. Transfer Request Chain
	This API should return the complete transfer history for a request.
	For example, if a request goes through the following transfer chain:
	2 → 3 → 4 → 5
	If any RequestId in this chain is provided, the API should return all related requests in the chain, along with the corresponding request times.
 

## Notes



## Questions

1. 

	## Todo