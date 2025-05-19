# 📡 Telecom ETL Project Using SSIS

An **ETL Case Study** project for a telecom company using **SQL Server Integration Services (SSIS)**.

---

## 📘 Project Description

A telecommunications company has hired an ETL developer to build a data warehousing pipeline. The company generates **daily CSV files** containing key customer activity data. The goal is to build a robust SSIS pipeline to extract, transform, validate, and load this data into a structured data warehouse while maintaining data integrity and audit logs.

---

## 📂 Source Data Format

Each CSV file contains information such as:

![CSV Data](https://github.com/user-attachments/assets/145d1252-5dd5-484b-bd08-1c69655f0bbc)

---

## 🔄 Required Data Processing

The SSIS package must perform the following operations on each file:

![Processing Steps](https://github.com/user-attachments/assets/fe37b41f-9520-44f2-9c17-e0c9f356c762)

---

## 🔁 Control Flow Overview

The control flow manages the overall execution of the ETL pipeline.

![Control Flow](https://github.com/user-attachments/assets/ce1ff3af-82a2-40c5-8f96-35ba91e813e3)

### ✅ Control Flow Steps:

1. **Generate Batch ID**
   - Generate a new `batch_id` for the current package run based on the latest value in `audit_dim`.

2. **Fetch File Name**
   - Iterate through the directory to retrieve all CSV file names.

3. **Insert Audit Record**
   - Insert a record into `dim_audit` for tracking, including batch ID, file name, and package name.

4. **Execute Data Flow**
   - Load and process the data from CSV into the database.
   - Log the number of total, inserted, and rejected records.

5. **Update Audit Log**
   - Record the results (inserted, rejected, processed counts) in the audit log.

6. **Manage Files**
   - Move the processed files to an archive or backup location.

---

## 🔄 Data Flow Overview

The data flow is responsible for validating, transforming, and loading the data.

![Data Flow](https://github.com/user-attachments/assets/351b050c-d128-4439-b2b7-97e604ed0819)

### ✅ Data Flow Steps:

1. **Data Validation**
   - Records failing validation rules are redirected to the `err_source_output` table.

2. **Audit ID & Row Count**
   - Retrieve the `audit_id` from the insert step and use it in downstream tasks.
   - Count processed and rejected rows.

3. **Column Operations**
   - Perform necessary transformations, including matching `imsi` with `subscriber_id`.

4. **Derived Columns**
   - Derive columns like `tac` and `snr` from the `imei` field.

5. **Load to Data Warehouse**
   - Load cleaned and processed records into the `fact_transaction` table.

---

## 🗂️ Schema

The final structure of the Data Warehouse includes:

![Schema](https://github.com/user-attachments/assets/305f3263-4d1a-4014-93e9-2b2fa7ab7ed4)
