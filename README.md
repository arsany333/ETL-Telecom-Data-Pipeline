# Telecom_ETL_Project Using (SSIS)
ETL Case Study Project for Telecom Company using SQL Server Integration Services (SSIS)

# Description 
A telecommunications company has approached an ETL developer to carry out a data warehousing project. 
The company generates a CSV files everyday, containing key data related to customer activities over a given period of time.
Below is a table showing the information stored in these CSV files.

![1](https://github.com/user-attachments/assets/145d1252-5dd5-484b-bd08-1c69655f0bbc)

# The Required Processing for the data in the files

![2](https://github.com/user-attachments/assets/fe37b41f-9520-44f2-9c17-e0c9f356c762)

# Control Flow of the program

![control flow](https://github.com/user-attachments/assets/ce1ff3af-82a2-40c5-8f96-35ba91e813e3)

## Steps of Control Flow 

1. **Get Batch ID**: 
   - For each run of the package, generate a new batch_id based on the last batch_id in the audit_dim.
2. **Getting file name**:
   - Iterate through the directory of the files and get the names of it.
3. **Audit Record Insertion**:
   - Insert a new record into the dim_audit, which includes the batch_id, package name, and file name.
4. **Executing Data Flow**:
   - Run the data flow task to import the file data into the database.
   - Record necessary audit information, including rejected rows, inserted rows, and total rows processed.
5. **Audit Record Maintenance**:
   - Update the audit log with details on the number of processed, rejected, and inserted rows.
6. **File Management**:
   - Move the processed files to a different location for further management.

# Data Flow of the program

![data flow](https://github.com/user-attachments/assets/351b050c-d128-4439-b2b7-97e604ed0819)

## Steps of Data flow 

1. **Data Validation Check**: 
   - For each csv file any rejected data record will move to table err_source_output
2. **Adding audit_id column and counting records**:
   - taking audit_id record from insert statment into a variable at which used here, after that count the extracted processed rows beside of the extracted error records.
3. **Making some operations to specific columns**:
   - by getting subscriber_id at which imsi is matched and operations as showded above
4. **Derived Columns Creation**:
   - Create necessary derived columns, such as `tac` and `snr`, from the `imei` column.
5. **loading prcessed data to fact_transaction**:
   - after making processing of the data it uploaded to the DWH as shown below in the schema.

## Schema

![schema2](https://github.com/user-attachments/assets/305f3263-4d1a-4014-93e9-2b2fa7ab7ed4)
  
