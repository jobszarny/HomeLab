Splunk Lab 1: Log Ingestion and Extracting + Basic Search and Filtering

Objective

The objective of this lab is to break into the well known SIEM software Splunk. The basics can never be overlooked and in this lab I will be showcasing my steps and processes for how to ingest, extract, searh, and filter new logs. There are seven different logs that were ingested that all serve different purposes but for this lab we are just going over how to set Splunk up to be used. The goal of doing this is to become comfortable with using Splunk Enterprise so I can continue to grow my knowledge and expand my abilities in labs.

Skills Learned

Log ingestion and field extraction for custom log types SPL proficiency in querying and transforming log data Event filtering to isolate patterns and anomalies Reporting on most frequent hosts, users, and errors

Tools Used

Splunk Web Interface ▸ Used for log ingestion, field extraction, and executing SPL queries.
Splunk Add Data Wizard ▸ Uploaded and indexed custom log files.
Field Extractor Tool ▸ Parsed log data to extract fields like IP, user, status code, etc.
SPL (Search Processing Language) ▸ Used commands like stats, table, top, sort, where, head.
Sample Log Files:
Apache access logs
NGINX logs
Windows Event Logs (.evtx or text)
Linux syslog files
Web Browser ▸ Accessed Splunk via http://localhost:8000.
Ingestion + Extract Step 1:

<img width="1465" height="819" alt="add1" src="https://github.com/user-attachments/assets/70d25d83-36fc-47f7-b828-64b78d728a88" />

Go to Settings and find Add Data on the left of the drop menu
Ingestion + Extract Step 2:

<img width="1427" height="820" alt="add2" src="https://github.com/user-attachments/assets/60ef9499-fab9-43c0-b649-6402264c0413" />

After clicking on Add Data, select Upload on the bottom left of the page
Ingestion + Extract Step 3:

<img width="1454" height="808" alt="add3" src="https://github.com/user-attachments/assets/bc457805-d978-4376-941c-8849265505d5" />

Select the source you want to add with the logs, check the preview before adding to ensure it's the correct file, then upload.
Ingestion + Extract Step 4:

<img width="1458" height="830" alt="add4" src="https://github.com/user-attachments/assets/b3f2ae00-3d4a-47a3-9ee5-f0943050885c" />

Now you must select the source type as this will ensure your logs are correctly parsed, my source was Apache Logs so I must select "access_combined" as this works with my log type.
Ingestion + Extract Step 5:

<img width="1467" height="808" alt="add5" src="https://github.com/user-attachments/assets/03e8b8b4-bceb-4f40-957a-2a47bc79e527" />

Input Settings is next and I left mine on constant value while making sure the host is correct and attaching the index I wish for the file to used within.
Ingestion + Extract Step 6:

<img width="1464" height="367" alt="add6" src="https://github.com/user-attachments/assets/05cb781a-4311-486d-8d4b-290ede90bc77" />

Review the details of adding your data before you submit, this page shows all the major details and you must submit when finished.
Ingestion + Extract Step 7:

<img width="1466" height="524" alt="add7" src="https://github.com/user-attachments/assets/d732fe5d-1d67-4ba7-8e6d-771acc671cd7" />

After submitting, there's options to start searching within your logs, extract them, add more data, download apps to have more options with the data, or you can build a dashboard. In this case we will be selecting, 'Extract Fields'
Ingestion + Extract Step 8:

<img width="1463" height="912" alt="extract 1" src="https://github.com/user-attachments/assets/9ac2bcfd-5e0d-45e2-9571-92639e13c368" />

We selected our event from "access_combined" sourcetype to build our extraction rule from.
Ingestion + Extract Step 9:

<img width="1396" height="463" alt="extract 2" src="https://github.com/user-attachments/assets/a00943d7-0755-44a3-8baf-7d3831671311" />

Then it prompts you to choose the method which will determine how Splunk should extract the field as we choose Regular Expression since it works well with Apache logs.
Ingestion + Extract Step 10:

<img width="1436" height="633" alt="extract3" src="https://github.com/user-attachments/assets/0ce360c6-37d9-45c1-a98d-14c8a2961a67" />

We are selecting the IP ' 10.0.0.2 ' in the Apache log as our field. Splunk has made the decision to preview other logs with IP's as it follows the similarity of the first IP. I basically just trained it on what an IP looks like in our logs.
Ingestion + Extract Step 11:

<img width="1455" height="604" alt="extract4" src="https://github.com/user-attachments/assets/b8044335-75c6-440d-884f-a10037b213cc" />

This step is basically testing out our new field extraction to see if it works, in this case it does because Splunk successfully captured the other IP's from our ingested Apache logs.
Next: Basic Search and Filtering

Basic Search and Filtering Step 1:

<img width="1434" height="827" alt="1" src="https://github.com/user-attachments/assets/70b8dc0e-d2ae-4246-8800-83c9ccad32d4" />

Select the Apps tab at the top left to get to Search & Reporting where we will be conducting our SPL.
Basic Search and Filtering Step 2:

<img width="1464" height="819" alt="2" src="https://github.com/user-attachments/assets/3dda6c6f-9c76-4559-ba33-bfb94a42edfb" />

Under "New Search" is the search panel where we write different queries, as the one completed represents the index I created where our previous logs were added. Under "Time Range" is a selection of various time frames to search within the logs, but currently selected is "All time".
Basic Search and Filtering Step 3:

<img width="1434" height="647" alt="3" src="https://github.com/user-attachments/assets/6143f27b-d8b4-43aa-bf34-a740ced41cce" />

Within this query we're searching within the declared index for a certain IP Address and sourcetype. In our case, sourcetype = "access_combined" is looking for Apache logs with ' IP="10.0.0.2" ' as part of the criteria for our outcome.
Outcome: We found an Apache log with our desired details and more! It includes the desired IP, user is 'mary', request is 'GET /index.html HTTP/1.1', and status code: 200 (successful request).
Fields Used: host, source, sourcetype
Basic Search and Filtering Step 4:

<img width="469" height="284" alt="4" src="https://github.com/user-attachments/assets/0c0845b2-f495-48d8-a1cd-3a5f83a9cb56" />

Now we're incorporating a stats command in a new query. This query is telling Splunk to count for logs that contain a certain IP Address within the desired index.
Outcome: The search came back with a count of '1' for our requested search which means only one log within the index contained the requested IP Address.
Used: 'stats count' to count how many matching events were found
Basic Search and Filtering Step 5:

<img width="1466" height="679" alt="5" src="https://github.com/user-attachments/assets/f02cf938-8626-48ae-a799-9fdc5a7ac1db" />

This search is asking for a frequency count of the most common sourcetypes in lab1_index.
Outcome: Shows 10 different sourcetypes for logs within lab1_index.
Used: ' top ' will list the most frequently found outcomes based on the criteria, in numerical order.
Basic Search and Filtering Step 6:

<img width="1465" height="419" alt="6" src="https://github.com/user-attachments/assets/16017af6-6e52-4345-82d1-6fc371e043c4" />

This query is asking for the top host that has more than 5 events. The query is counting events by 'host' as it only filters those with '>5' events. Additionally, it is sorting in descending order but since we asked for 'head 1' we are limiting the results to only the top spot.
Outcome: The top host is 'Jacks-MacBook-Air.local' with 27 events.
Used: Aggregation ' stats count by host ', filtering ' where count > 5 ', sorting ' sort - count ', result limiting ' head 1 '.
