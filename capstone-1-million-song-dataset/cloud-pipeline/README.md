# 3 - Cloud Pipeline with AWS and Azure

## - 3.1 Purpose of the Cloud Pipeline
The purpose of this pipeline was to create a similar structure as the <em>Local Pipeline</em>, but using an Azure database as the destination.
There are a few major differences with this approach:
1. The source dataset comes from AWS
2. An Azure Virtual Machine (VM) is required to run the Python SQLAlchemy script
3. Azure SQL Database (which is SQL Server) is used instead of MySQL

## 3.2 - Database Design
The ERD for the Azure SQL Database is the same as the MySQL database in the <em>Local Pipeline</em>. Here it is again for reference:
![image did not render](architecture/msd-erd.png "msd-erd.png")

## 3.3 - Pipeline Design