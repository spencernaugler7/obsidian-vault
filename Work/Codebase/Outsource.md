# Outsource request overview.
1. Voyce -> Martti   VoyceGateway v1/outsource
2. Martti -> Voyce   `v1/outsource/accept`  
3. Martti -> Voyce   `v1/outsource/finish` 
4. Voyce -> Martti VoyceGateway delete `v1/outsource/{id}` (only if it already exists)

>[!note]
>[[WEYI-748]] is updating this process to use v2 endpoints (`v2/outsource/{id}`).

# Accept process
1. fetch the request record using the outsource id.
2. set the request property "ExternalInterpreterId" to the "InterpeterId" we provided via the "accept" endpoint
3. generate the interpreter for outsource id with the asl language.
	1. upsert the provider
		1. tables affected
			1. Provider
			2. LSPProvider
			3. AppUser
			4. ProviderProperty
	2. update last name of the provider
	3. update 