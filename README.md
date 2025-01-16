# AzureFileTransfer
This repository is to explore the Azure File transfer as a managed file transfer solution

Moving files from one storage account to another storage account within the same tenant, and across subscriptions.

Requirements:
1) Ability to move files from one Storage Account to Another
2) Files should only be read by this process, only after it is completely committed
3) Files of larger sizes than 1GB should be supported
4) Should be a extensible soution
5) Files of larger sizes
6) Easily implemetable solution across the portfolio teams
7) File should not be read prematurely, only after it is completely written.

Solution
Use Azure Event Grid, on the back of the Microsoft.Storage.BlobCreated event being created. This event is only triggered when the block blob is completely committed
Can use Logic Apps Azure Event grid trigger to get the event of this message, after which you can go and get the file from storage account
Then it will create a file in the destination storage container, with the contents of the file.
There is a lease lock applied on the storage container - so that there are no concurrency issues
Files upto 1GB are supported through this process

Additional considerations
Can use Service Bus to pool all the blobcreated events - and can use Logic App from Service Bus. 
Using App Configuration for config related data
Using Alternative solution when the size is more than 1GB - AzCopy???
