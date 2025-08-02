Splunk Lab 1: Log Ingestion and Parsing + Basic Search and Filtering 

Objective

The objective of this lab is to break into the well known SIEM software Splunk. The basics can never be overlooked and in this lab I will be showcasing my steps and processes for how to ingest, parse, searh, and filter new logs. There are seven different logs that were ingested that all serve different purposes but for this lab we are just going over how to set Splunk up to be used. The goal of doing this is to become comfortable with using Splunk Enterprise so I can continue to grow my knowledge and expand my abilities in labs. 

Skills Learned

Log ingestion and field extraction for custom log types
SPL proficiency in querying and transforming log data
Event filtering to isolate patterns and anomalies
Reporting on most frequent hosts, users, and errors

Tools Used

- Splunk Web Interface ▸ Used for log ingestion, field extraction, and executing SPL queries.
- Splunk Add Data Wizard ▸ Uploaded and indexed custom log files.
- Field Extractor Tool ▸ Parsed log data to extract fields like IP, user, status code, etc.
- SPL (Search Processing Language) ▸ Used commands like stats, table, top, sort, where, head.
- Sample Log Files:
   - Apache access logs
   - NGINX logs
   - Windows Event Logs (.evtx or text)
   - Linux syslog files
- Web Browser ▸ Accessed Splunk via http://localhost:8000.
- Text Editor (e.g., Notepad++, VS Code) ▸ Opened and reviewed raw log files before ingestion.
- Terminal or Command Prompt ▸ Optional: Used to inspect or tail logs before uploading.
- Operating System Logs ▸ Pulled system-generated logs from Windows or Linux environments.



Ingestion + Parse Step 1: 

<img width="1465" height="819" alt="add1" src="https://github.com/user-attachments/assets/cc512bcd-d5b7-4dd2-b706-cae14f888d33" />

- Go to Settings and find Add Data on the left of the drop menu

Ingestion + Parse Step 2:

<img width="1427" height="820" alt="add2" src="https://github.com/user-attachments/assets/ac1fd1f6-be55-417b-a62d-8c3826198585" />

- After clicking on Add Data, select Upload on the bottom left of the page

Ingestion + Parse Step 3: 

<img width="1454" height="808" alt="add3" src="https://github.com/user-attachments/assets/b259a789-1c5e-46ce-8a74-e43b92faccaa" />

- Select the source you want to add with the logs, check the preview before adding to ensure it's the correct file, then upload. 

Ingestion + Parse Step 4: 

<img width="1458" height="830" alt="add4" src="https://github.com/user-attachments/assets/736488cb-103f-40b4-ba1e-6a5df6106843" />

- Now you must select the source type as this will ensure your logs are correctly parsed, my source was Apache Logs so I must select "access_combined" as this works with my log type. 

Ingestion + Parse Step 5: 

<img width="1467" height="808" alt="add5" src="https://github.com/user-attachments/assets/cfb839a8-d457-4671-acfa-12c5b8c283c3" />

- Input Settings is next and I left mine on constant value while making sure the host is correct and attaching the index I wish for the file to used within. 

Ingestion + Parse Step 6: 

<img width="1464" height="367" alt="add6" src="https://github.com/user-attachments/assets/dbb8b927-fc93-4dd6-bd40-327054238dcd" />

- Review the details of adding your data before you submit, this page shows all the major details and you must submit when finished.

Ingestion + Parse Step 7: 

<img width="1466" height="524" alt="add7" src="https://github.com/user-attachments/assets/79d83688-ca88-435a-84e1-7978b78a2775" />

- After submitting, there's options to start searching within your logs, extract them, add more data, download apps to have more options with the data, or you can build a dashboard.




Next: Basic Search and Filtering 


Basic Search and Filtering Step 1: 

<img width="1434" height="827" alt="1" src="https://github.com/user-attachments/assets/1ca433e7-5a34-43e8-afb3-0b3c74f35e4a" />

- Select the Apps tab at the top left to get to Search & Reporting where we will be conducting our SPL.
 
Basic Search and Filtering Step 2: 

<img width="1464" height="819" alt="2" src="https://github.com/user-attachments/assets/10d67a43-8fad-410b-9a14-b1f07001e2f5" />

- Under "New Search" is the search panel where we write different queries, as the one completed represents the index I created where our previous logs were added. Under "Time Range" is a selection of various time frames to search within the logs, but currently selected is "All time". 

Basic Search and Filtering Step 3: 

<img width="1434" height="647" alt="3" src="https://github.com/user-attachments/assets/c72d41dc-6fba-47a1-8bbb-61cd4fb33030" />

- Within this query we're searching within the declared index for a certain IP Address and sourcetype. In our case, sourcetype = "access_combined" is looking for Apache logs with ' IP="10.0.0.2" ' as part of the criteria for our outcome.
- Outcome: We found an Apache log with our desired details and more! It includes the desired IP, user is 'mary', request is 'GET /index.html HTTP/1.1', and status code: 200 (successful request).
- Fields Used: host, source, sourcetype

Basic Search and Filtering Step 4: 

<img width="469" height="284" alt="4" src="https://github.com/user-attachments/assets/9cc36ef2-b38c-4514-8417-ab581e094936" />

- Now we're incorporating a stats command in a new query. This query is telling Splunk to count for logs that contain a certain IP Address within the desired index.
- Outcome: The search came back with a count of '1' for our requested search which means only one log within the index contained the requested IP Address.
- Used: 'stats count' to count how many matching events were found

Basic Search and Filtering Step 5: 

<img width="1466" height="679" alt="5" src="https://github.com/user-attachments/assets/26e7ee94-2b6e-4d37-b247-160d89b6fe9a" />

- This search is asking for a frequency count of the most common sourcetypes in lab1_index.
- Outcome: Shows 10 different sourcetypes for logs within lab1_index.
- Used: ' top ' will list the most frequently found outcomes based on the criteria, in numerical order.


Basic Search and Filtering Step 6: 

<img width="1465" height="419" alt="6" src="https://github.com/user-attachments/assets/caaf42b2-eafd-46d9-ba7d-9b647cdc45ed" />

- This query is asking for the top host that has more than 5 events. The query is counting events by 'host' as it only filters those with '>5' events. Additionally, it is sorting in descending order but since we asked for 'head 1' we are limiting the results to only the top spot. 
- Outcome: The top host is 'Jacks-MacBook-Air.local' with 27 events.
- Used: Aggregation ' stats count by host ', filtering ' where count > 5 ', sorting ' sort - count ', result limiting ' head 1 '. 

