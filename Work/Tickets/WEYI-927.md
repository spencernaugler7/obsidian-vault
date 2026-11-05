---
summary:
created: 2026-10-30
source: https://cloudbreak.atlassian.net/browse/WEYI-927
---
# Voyce Core Data into Kafka

## Description

Create a new task in the Voyce Core system to publish CDC events directly to Kafka. Each source table should have its own dedicated Kafka topic, with one message per changed row.

The new Kafka task must run in parallel with the existing SQS publishing task. The existing Databricks workspaces used by VIP still depend on SQS, so this flow must continue without interruption.

The SQS publishing task should only be decommissioned after VIP has fully migrated to the new Databricks workspaces and no longer depends on the existing SQS flow.

## Requirements

## Acceptance Criteria

- A new task publishes Voyce Core CDC events directly to Kafka.
- Each source table publishes events to its own dedicated topic.
- Each message represents a single row change, supporting insert, update, and delete events.
- CDC events continue to be published to SQS while the Kafka task runs.
- Kafka event delivery is verified without disrupting the existing VIP data flow.
- The SQS task remains active until VIP migration is complete and its dependencies on SQS are removed.

## Notes

- Testing Notes
	- A new task publishes Voyce Core CDC events directly to Kafka.
	- Each source table publishes events to its own dedicated topic.
	- Each message represents a single row change, supporting insert, update, and delete events.
	- CDC events continue to be published to SQS while the Kafka task runs.
	- Kafka event delivery is verified without disrupting the existing VIP data flow.
	- The SQS task remains active until VIP migration is complete and its dependencies on SQS are removed.

## Questions

1. What is a CDC event?
	1. change data capture
2. what does vip use databricks for?
	1. single reporting source
3. what is databricks?
4. we already use a push notification service. Via firebase cloud messaging. Why do we also have an sqs message queue?
5. 

## Todo

1. new column on TableLiveUpdate1-15 SyncedCDC
2. new service
	1. get top 300 records from non-cdcsynced records

## Processes

TableTrigger
1. is insert or update 
2. exec `sp_TableLiveUpdateInsert` with `DatabaseName`, `TableName` and `PrimaryKey`
3. `sp_TableLiveUpdateInsert` if statement for each table. here is the mapping from source table to the result table.

| **Source Table**                         | **Insertion Table** | **Notes**                                                                  |
| ---------------------------------------- | ------------------- | -------------------------------------------------------------------------- |
| Request                                  | TableLiveUpdate     |                                                                            |
| Client                                   | TableLiveUpdate2    |                                                                            |
| ClientUser                               | TableLiveUpdate2    |                                                                            |
| ClientUserIVRPinInfo                     | TableLiveUpdate2    |                                                                            |
| CompanyProperty                          | TableLiveUpdate2    |                                                                            |
| AppUser                                  | TableLiveUpdate3    |                                                                            |
| BillClientProduct                        | TableLiveUpdate3    |                                                                            |
| BillCompanyClientProductIVRPinInfo       | TableLiveUpdate3    |                                                                            |
| BillCompanyProduct                       | TableLiveUpdate3    |                                                                            |
| BillCompanyProductOption                 | TableLiveUpdate3    |                                                                            |
| Company                                  | TableLiveUpdate3    |                                                                            |
| CompanyTimeZone                          | TableLiveUpdate3    |                                                                            |
| InvoiceSetup                             | TableLiveUpdate3    |                                                                            |
| InvoiceSetupDetail                       | TableLiveUpdate3    |                                                                            |
| InvoiceSetupDetailBillingItemParameter   | TableLiveUpdate3    |                                                                            |
| KanjiDevice                              | TableLiveUpdate3    |                                                                            |
| KanjiDevicePerson                        | TableLiveUpdate3    |                                                                            |
| LSPProvider                              | TableLiveUpdate3    |                                                                            |
| CompanyDataInputScheme                   | TableLiveUpdate3    |                                                                            |
| CodeList                                 | TableLiveUpdate4    |                                                                            |
| Language                                 | TableLiveUpdate4    |                                                                            |
| Person                                   | TableLiveUpdate4    |                                                                            |
| PersonSessionProperty                    | TableLiveUpdate5    |                                                                            |
| Provider                                 | TableLiveUpdate5    |                                                                            |
| ProviderOnLineStatus                     | TableLiveUpdate5    |                                                                            |
| ProviderService                          | TableLiveUpdate5    |                                                                            |
| RequestEval                              | TableLiveUpdate6    |                                                                            |
| RequestFeedback                          | TableLiveUpdate6    |                                                                            |
| RequestPersonSession                     | TableLiveUpdate6    |                                                                            |
| RequestProvider                          | TableLiveUpdate6    |                                                                            |
| ServiceItemDataInput                     | TableLiveUpdate7    |                                                                            |
| VOSPhoneRequestProperty                  | TableLiveUpdate8    |                                                                            |
| ServiceItemDetail                        | TableLiveUpdate9    | live update table 9 for records with an even id value. 18 for an odd value |
| ServiceItemMaster                        | TableLiveUpdate10   | 10 for even value id records. 20 for odd valued                            |
| InvoiceMaster                            | TableLiveUpdate11   |                                                                            |
| InvoiceDetail                            | TableLiveUpdate11   |                                                                            |
| InvoiceMasterQuickbook                   | TableLiveUpdate11   |                                                                            |
| YClientInfoNM2                           | TableLiveUpdate11   |                                                                            |
| RequestEPICInformation                   | TableLiveUpdate11   |                                                                            |
| RequestConference                        | TableLiveUpdate12   |                                                                            |
| RequestConferenceSession                 | TableLiveUpdate12   |                                                                            |
| RequestConferenceSessionProperty         | TableLiveUpdate12   |                                                                            |
| RequestConferenceSessionVideoParticipant | TableLiveUpdate13   |                                                                            |
| RequestConferenceSessionAudioParticipant | TableLiveUpdate14   |                                                                            |
| VOSPhoneRequest                          | TableLiveUpdate15   |                                                                            |
| VOSPhoneNumber                           | TableLiveUpdate15   |                                                                            |
| InvoiceBillingItem                       | TableLiveUpdate16   |                                                                            |
| InvoiceBillingItemParameter              | TableLiveUpdate16   |                                                                            |
| ClientMarttiMap                          | TableLiveUpdate16   |                                                                            |
| RequestProperty                          | TableLiveUpdate17   |                                                                            |
| TableLiveDeleteAction                    | TableLiveUpdate18   |                                                                            |
| RequestException                         | TableLiveUpdate19   |                                                                            |
| RequestExceptionBackupCall               | TableLiveUpdate19   |                                                                            |
| ProviderDedicatedSchedule                | TableLiveUpdate20   |                                                                            |
| ProviderDedicatedSchedule7Days           | TableLiveUpdate20   |                                                                            |

Data sync process
1. Service `WEYIReportLiveDataAction` maintains all triggers 
2. for each numbered timer the previous service starts it runs `WEYIReportLib.ReportLiveData.PushTableLiveUpdateProcess(int index)` where index corresponds to the number of the timer that triggered.
3. each `PushTableLiveUpdateProcess` 
	1. runs `sp_TableLiveUpdateNeedToPush` initially, 
	2. creates a json object for each and then runs 
	3. **pushes the json object into sqs**
	4. runs `sp_TableLiveUpdatePushFinish` to complete the process.

Backup process
1. tables that should be synced have a particular trigger: `tiud_<TableName>`. This trigger execs `sp_TableLiveUpdateInsert` on insertion of a record or an update of a record.
2. `sp_TableLiveUpdateInsert` takes new record data

