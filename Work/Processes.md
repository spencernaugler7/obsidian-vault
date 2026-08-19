# Outsource request process.
1. Voyce -> Martti   VoyceGateway v1/outsource
2. Martti -> Voyce   `v1/outsource/accept`  
3. Martti -> Voyce   `v1/outsource/finish` 
4. Voyce -> Martti VoyceGateway delete `v1/outsource/{id}` (only if it already exists)

>[!note]
>[[WEYI-748]] is updating this process to use v2 endpoints (`v2/outsource/{id}`).

