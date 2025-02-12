# Configuring-and-Deploying-a-Relational-Database-RDS-
Amazon Relational Database Service (RDS) allows you to deploy, manage, and scale a relational database in the AWS cloud without handling infrastructure maintenance. 

Step 1: Create an RDS Database Instance

-Log in to AWS Management Console
-Go to Services → Search for RDS → Click on it
-Click "Create Database"

![Screenshot 2025-02-10 204910](https://github.com/user-attachments/assets/013c61da-f77f-4d1f-8bea-a9ec3f26bcd2)

-Choose Database Engine
-Select "Standard Create"

![Screenshot 2025-02-10 204927](https://github.com/user-attachments/assets/1941bbbc-1c45-48b7-a1c8-a2d0ad01fa43)

-Choose Database Engine → MySQL 

![Screenshot 2025-02-10 204945](https://github.com/user-attachments/assets/714cdb84-d081-42d1-bf65-550893b2286d)

-Choose Deployment Type
-Select"Free tier"

![Screenshot 2025-02-10 205000](https://github.com/user-attachments/assets/2774d935-0c2b-4edb-a975-014b7e910414)

DB Instance Identifier: myrdsinstance

![Screenshot 2025-02-10 205026](https://github.com/user-attachments/assets/f74a7fea-f37d-40cc-b3aa-4d4a90cf8af9)

-Configure Credentials
-Master Username: admin
-Master Password: Set a strong password
-Click "Show Master Password" → Save it for later

![Screenshot 2025-02-10 205304](https://github.com/user-attachments/assets/a8fa8e61-2751-4cd5-ad2c-8261148bbb0f)

-Instance Size & Storage
-Instance Class: Choose db.t3.micro (for Free Tier)

![Screenshot 2025-02-10 205350](https://github.com/user-attachments/assets/df41c8c3-13ae-4bca-8f93-cafee3e1ce2b)

-Storage Type: Select General Purpose (SSD)
-Allocated Storage: Keep default (20 GB)

![Screenshot 2025-02-10 205415](https://github.com/user-attachments/assets/1c50620b-601b-42bf-8966-27004343dbdc)

Connectivity Settings

![Screenshot 2025-02-10 205641](https://github.com/user-attachments/assets/14a05bda-a07f-4b7b-9051-66d8af24444d)

VPC: Choose "Default VPC" (or create a new one)

![Screenshot 2025-02-10 205700](https://github.com/user-attachments/assets/564d8fea-e6ab-4801-acfd-4565a7a3bc5f)

We are creating new one named as "myrds"

![Screenshot 2025-02-10 205908](https://github.com/user-attachments/assets/8d478b9b-cf28-49bd-b6e2-1bced80ae011)

Configure Additional Settings
Initial Database Name: mydatabase

![Screenshot 2025-02-10 205941](https://github.com/user-attachments/assets/8a09545c-b30f-4344-94a1-7bfcfe65b064)

![Screenshot 2025-02-10 210041](https://github.com/user-attachments/assets/f6e2a98d-867a-4c7c-9a0a-d4987a789e59)

Click "Create Database"

Step 2: Configure Security Group for RDS

Go to Services → EC2 → Security Groups
Find the security group assigned to your RDS instance

![Screenshot 2025-02-10 210452](https://github.com/user-attachments/assets/cf4689fc-6687-44bf-94a4-b53c9198bacc)

Click Inbound Rules → Edit Inbound Rules

![Screenshot 2025-02-10 210519](https://github.com/user-attachments/assets/ef93fb99-3161-4e34-ba28-9ba95791703b)

![Screenshot 2025-02-10 210710](https://github.com/user-attachments/assets/627bad9d-0ce3-46cf-a9f4-e7a22e5b3200)

![Screenshot 2025-02-10 210732](https://github.com/user-attachments/assets/22fde271-a509-4f43-a286-790634c5b68e)

An error pops up
![Screenshot 2025-02-10 211239](https://github.com/user-attachments/assets/cf3a23b4-c2ba-493e-b452-f31e8cb5fd58)

Fix: Add Subnets to Your VPC
![Screenshot 2025-02-10 211400](https://github.com/user-attachments/assets/d9b8298b-7db8-4991-abdb-a600ecda3b32)

Create 2 subnets for both az

Subnet 1:
Name: rds-subnet-1
Availability Zone: Choose any (e.g., us-east-1a)
CIDR Block: 172.31.128.0/17
![Screenshot 2025-02-10 212519](https://github.com/user-attachments/assets/6bca3a74-7a49-4372-821f-6abec4681e58)

Subnet 2:
Name: rds-subnet-2
Availability Zone: Choose another (e.g., us-east-1b)
CIDR Block: 172.31.0.0/17
![Screenshot 2025-02-10 212534](https://github.com/user-attachments/assets/2964cec3-c2d1-4067-b478-029ced5320c9)

your VPC has subnets!
![Screenshot 2025-02-10 212550](https://github.com/user-attachments/assets/0757534f-65ce-4f5c-adc8-4b5479607785)

Create a DB Subnet Group
![Screenshot 2025-02-10 212704](https://github.com/user-attachments/assets/7f2585ca-008c-4bc2-8320-8b939064dd40)
![Screenshot 2025-02-10 213207](https://github.com/user-attachments/assets/e271ee47-6dbd-4a50-a3fd-a1904e2d0d68)

Step 3: Connect to RDS from Local Machine
Click on your database → Copy the Endpoint
![Screenshot 2025-02-10 213740](https://github.com/user-attachments/assets/417d1cad-365a-4949-8905-8d5d58231b73)

Connect via MySQL Workbench
![Screenshot 2025-02-10 214917](https://github.com/user-attachments/assets/292d6957-4847-4ac1-9025-cad61f4c7791)

Launch MySQL Workbench
Click "Database" → "Manage Connections"
![Screenshot 2025-02-10 215458](https://github.com/user-attachments/assets/2053883d-714f-4ee5-b257-75693d8c8828)
![Screenshot 2025-02-10 215514](https://github.com/user-attachments/assets/c3c6b5bc-ff08-43c2-9671-073da67f618a)

Enter your endpoints and User name + password
![Screenshot 2025-02-10 215748](https://github.com/user-attachments/assets/ec39eb4f-0e94-40fd-9fbe-49f991df89ec)

Click "New"
![Screenshot 2025-02-10 223400](https://github.com/user-attachments/assets/5602db03-1e4e-4017-a483-270c5edc3ebc)

Run a test query:SHOW DATABASES;
![Screenshot 2025-02-10 224312](https://github.com/user-attachments/assets/6312f2f7-95aa-48de-91b6-e405e27e00a4)
![Screenshot 2025-02-10 231008](https://github.com/user-attachments/assets/94f0d06f-0191-4a66-9942-88b9339da71a)
![Screenshot 2025-02-10 230529](https://github.com/user-attachments/assets/5e4ee90a-372c-4537-9e13-5df449930bcb)


