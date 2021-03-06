# Download 
To download this script, download the latest version [here](https://github.com/dpaulson45/ExchangeLogCollector/releases)

# ExchangeLogCollector
This script is intended to collect the Exchange default logging data from the server in a consistent manner to make it easier to troubleshoot an issue when large amounts of data is needed to be collected. You can specify what logs you want to collect by the switches that are available, then the script has logic built in to determine how to collect the data. 

# How to Run 
The script MUST be run as Administrator in Exchange Management Shell on an Exchange Server that you would like to collect the data from. This script is mainly built around Exchange 2013 and greater, but it should be able to collect data in Exchange 2010 still just fine. This script is great to collect a set of data for an issue without needing to collect a lot of data that isn't needed for an issue. 

Within the version 2.1 or greater, we are now able to do remote collections if the target machine is on Windows Server 2012 or greater to use Invoke-Command. If Invoke-Command works remotely, then we will allow you to attempt to collect the data. You can still utilize the script to collect locally as it used to be able to, if the target OS doesn't allow this. 

Prior to collecting the data, we check to make sure that there is at least 15GB of free space at the location of where we are trying to save the data of the target server. You have the option to use the Disk Override switch but use at your own discretion. 

Examples: 

This cmdlet will collect all default logs of the local Exchange Server and store them in the default location of "C:\MS_Logs_Collection" 

*.\ExchangeLogCollector.ps1 -AllPossibleLogs*

This cmdlet will collect all relevant data regarding database failovers from server EXCH1 and EXCH2 and store them at Z:\Data\Logs. Note: at the end of the collection, the script will copy over the data to the local host execution server to make data collection even easier. 

*.\ExchangeLogCollector.ps1 -DatabaseFailoverIssue -Servers EXCH1,EXCH2 -FilePath Z:\Data\Logs*

This cmdlet will collect all relevant data regarding IIS Logs (within the last 3 days by default) and all RPC type logs from the servers EXCH1 and EXCH2 and store them at the default location of "C:\MS_Logs_Collection"

*.\ExchangeLogCollector.ps1 -Servers EXCH1,EXCH2 -IISLogs -RPCLogs*


# Parameters 

FilePath - The Location of where you would like the data to be copied over to. This location must be the same and accessible on all servers if you use the Servers parameter. 

Servers - An array of servers that you would like to collect data from. 

EWSLogs - Collects the EWS Logs from the Exchange Server. 

IISLogs - Collects the IIS Logs from the Exchange Server, this will also collect the Httperr logs from the server as well. On Exchange 2010, we collect it only from the default IIS log location. 

DailyPerformanceLogs - Collects the daily performance logs.

ManagedAvailability - Collects Managed Availability (MA) Logs.

Experfwiz - Collects Experfwiz data from the server. It will only be able to do this if we can find the path from logman. 

RPCLogs - Collects the RPC Logs from the Server. 

EASLogs - Collects the Exchange Active Sync Logs. 

ECPLogs - Collects the ECP Logs from the Server. 

AutoDLogs - Collects the AutoD Logs from the Server. 

OWALogs - Collects the OWA Logs from the Server. 

ADDriverLogs - Collects the AD Driver Logs from the Server. 

SearchLogs - Collects the Search Logs from the Server. 

HighAvailabilityLogs - Collects the High Availability Logs from the Server.

MapiLogs - Collects the Mapi Logs from the Server. 

MessageTrackingLogs - Collects the Message Tracking Logs from the Server. 

HubProtocolLogs - Collects the Hub Protocol Logs from the Server. 

HubConnectivityLogs - Collects the Hub Connectivity Logs from the Server. 

FrontEndConnectivityLogs - Collects the Front End Connectivity Logs from the Server. 

FrontEndProtocolLogs - Collects the Front End Protocol Logs from the Server. 

MailboxConnectivityLogs - Collects the Mailbox Connectivity Logs from the Server. 

MailboxProtocolLogs - Collects the Mailbox Protocol Logs from the Server. 

QueueInformationThisServer - Collects the Queue Information from the Server. 

ReceiveConnectors - Collects the Receive Connector Information from the Server. 

SendConnectors - Collects the Send Connector Information from the ORG. 

DAGInformation - Collects DAG Information from the Server. 

GetVdirs - Collects the Virtual Directories of the environment. 

OrganizationConfig - Collects the Organization Configuraiton from the environment.

TransportConfig - Collects the Transport Configuration from the Server. 

DefaultTransportLogging - Collects the default logging enabled on an out of the box Exchange Server. 

Exmon - Collects Exmon information from the Server. 

ServerInfo - Collects general server information from the server. 

ExchangeServerInfo - Used to collect Exchange Server data (Get-ExchangeServer, Get-MailboxServer...). Enabled whenever ServerInfo is used as well.

CollectAllLogsBasedOnDaysWorth - Collects all the logs based off DaysWorth instead of just the default logs of IIS and Daily Performance due to their size by default. 

AppSysLogs - Collects the Application, System, and MSExchange Management. 

AllPossibleLogs - Enables the collection of all default logging collection on the Server. 

SkipEndCopyOver - If the Servers parameter is used, by default we will attempt to collect all the data back over to the local server after all the data was collected on each server. 

DaysWorth - The number of days to go back from today for log collection. 

DatabaseFailoverIssue - Enables Daily Performance Logs, High Availability Logs, Managed Availability logs, and DAG Information collections. 

Experfwiz_LogmanName - Sets the name of how to collect Experfwiz data from logman. Use only if a different log collection name is used within the experfwiz script. 

Exmon_LogmanName - Sets the name of how to collect Exmon data from logman. Use only if a different log collection name is used within the experfwiz script. 

AcceptEULA - Bypass the disclaimer for using the script.
