- MigrationRequestMonitor
	- keeps track of table column changes.


So we have three tables `Request`, `ServiceItemMaster`, and `ServiceItemDetail`. `ServiceItemMaster` has a `RequestId` and `ServiceItemDetail` also has a `RequestId`. It seems odd that `ServiceItemDetail` needs a `RequestId` column. Is there a scenario where have have some `ServiceItemDetail` records that don't have the same `RequestId` as their parent `ServiceItemMaster` record?

Yes, master means a set of requests, the requestId is the first request in the whole call sequence while the requestId is for different call segments, for example, if a call starts with an operator but ends up with a language, we will have 2 detail records and 1 master records.