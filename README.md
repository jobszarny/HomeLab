Splunk Lab 1: Log Ingestion and Parsing + Basic Search and Filtering 

Objective

The objective of this lab is to break into the well known SIEM software Splunk. The basics can never be overlooked and in this lab I will be showcasing my steps and processes for how to ingest, parse, searh, and filter new logs. There are seven different logs that were ingested that all serve different purposes but for this lab we are just going over how to set Splunk up to be used. The goal of doing this is to become comfortable with using Splunk Enterprise so I can continue to grow my knowledge and expand my abilities in labs. 

Skills Learned

Log ingestion and field extraction for custom log types
SPL proficiency in querying and transforming log data
Event filtering to isolate patterns and anomalies
Reporting on most frequent hosts, users, and errors

Tools Used

Splunk Web Interface ▸ Used for log ingestion, field extraction, and executing SPL queries.
Splunk Add Data Wizard ▸ Uploaded and indexed custom log files.
Field Extractor Tool ▸ Parsed log data to extract fields like IP, user, status code, etc.
SPL (Search Processing Language) ▸ Used commands like stats, table, top, sort, where, head.
Sample Log Files:
▸ Apache access logs
▸ NGINX logs
▸ Windows Event Logs (.evtx or text)
▸ Linux syslog files
Web Browser ▸ Accessed Splunk via http://localhost:8000.
Text Editor (e.g., Notepad++, VS Code) ▸ Opened and reviewed raw log files before ingestion.
Terminal or Command Prompt ▸ Optional: Used to inspect or tail logs before uploading.
Operating System Logs ▸ Pulled system-generated logs from Windows or Linux environments.



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


Basic Search and Filtering Step 2: 


Basic Search and Filtering Step 3: 


Basic Search and Filtering Step 4: 


Basic Search and Filtering Step 5: 


Basic Search and Filtering Step 6: 


