# File Transfer from On-Premises Server to Google Cloud

This document provides a guideline for securely migrating files from an on-premises server to SFTP Location. The migration script includes configuration settings, batch script files for password or PPK-based authentication, and the necessary tools.

## Prerequisites

Before you start, ensure you have the following:
- Access to the on-premises server where the files are located.
- SFTP credentials.
- A zip file containing the migration script.

## Step-by-Step Process

### 1. Extract the Migration Script

1. Download the zip file containing the migration script to your on-premises server.
2. Extract the contents of the zip file. It should contain:
    - `config.ini` (configuration file)
    - `file_transfer_pwd.bat` (batch script for password-based authentication)
    - `file_transfer_ppk.bat` (batch script for PPK-based authentication)


### 2. Download PSFTP Client

You need to download the `psftp.exe`(an SFTP client, i.e., general file transfer sessions much like FTP) depending upon your processor type:

- 32-bit: [psftp.exe (via FTP)](https://puttygen.com/download.php?val=22)
- 64-bit: [psftp.exe (via FTP)](https://puttygen.com/download.php?val=25)

Copy the `psftp.exe` to the above extracted folder.

### 3. Configure `config.ini`

Open the `config.ini` file in a text editor and provide the necessary details:
```cmd
sftp_ip = <your_sftp_server_ip>
user = <your_username>
password = <your password if using password auth>
ppk_path = <path to your ppk file if using ppk auth>(Either password or PPK should be provided)
source_dir = <path to your data files folder>
hotel_name = <your hotel name>
file_type = <file format e.g. csv,zip,txt>
```

### 4. Running the Batch Script

### Add How to do using Schedular
- Look for Task Schedular in your windows machine.
![step1](https://github.com/parthpaliwal-49/testing/assets/146166132/86b21c8a-9027-4f32-9590-b3328b2da5fe)



Once Task Schedular is opened click on Create Task option to create a new task.
![step2](https://github.com/parthpaliwal-49/testing/assets/146166132/675d0e39-562b-4c7d-ac9a-2705d347f13a)



Once you create a task in general configuration  give name to the task.
![step3](https://github.com/parthpaliwal-49/testing/assets/146166132/37ac0b88-324b-4f88-bafe-a6eaa5750bb4)



After giving name also select user login settings and OS version for the task accordingly.
![step4](https://github.com/parthpaliwal-49/testing/assets/146166132/f7358350-651b-4f57-a15e-21df7253c43f)



Now select Triggers configuration and click on New.
![step5](https://github.com/parthpaliwal-49/testing/assets/146166132/293d2222-aa1c-4487-920b-a5400f1961f8)



Choose when do you you want to run the task and do not forget to click on Enabled on bottom is not selected already.
![step6](https://github.com/parthpaliwal-49/testing/assets/146166132/c9067412-7b39-4c37-8a2b-2ef07b49706c)



Select Actions configuration section and click on New.
![step7](https://github.com/parthpaliwal-49/testing/assets/146166132/077cabc2-2d16-4227-94fd-72e9e1a6c522)



In Action select Start a program and give the path to the batch script of your choice in Program/Script option.
Also do not forget to add the path to the Script folder in "Start in(Optional) configuration"
![step8](https://github.com/parthpaliwal-49/testing/assets/146166132/c45bc9be-d40c-496b-be53-dfb9c8ee1958)



Click OK for Task Configuration and also for the Task.
Now your task is scheduled for the provided time and you can see it in Active Tasks
![step9](https://github.com/parthpaliwal-49/testing/assets/146166132/c5bf5cee-221e-421c-a18a-f019a4e900de)






Based on your authentication method (password or PPK), run the appropriate batch script:

#### Password-Based Authentication

1. Open Command Prompt.
2. Navigate to the directory where you extracted the migration script.
3. Run the following command:
    ```cmd
    file_transfer_pwd.bat
    ```

#### PPK-Based Authentication

1. Open Command Prompt.
2. Navigate to the directory where you extracted the migration script.
3. Run the following command:
    ```cmd
    file_transfer_ppk.bat
    ```

### Additional Information

- **Directory Structure:** The script will create a directory structure on the remote server based on the file names and dates.
- **Log File:** The script generates a log file (`logfile.log`) to track the progress and any errors encountered during the transfer.


### Script Overview

#### `file_transfer_pwd.bat`

This batch script is used for password-based authentication. It reads the configuration from `config.ini` and uses `psftp.exe` to transfer files.

#### `file_transfer_ppk.bat`

This batch script is used for PPK-based authentication. It also reads the configuration from `config.ini` and uses `psftp.exe` to transfer files.

### Troubleshooting

- **Invalid Credentials:** Ensure your SFTP credentials are correct in the `config.ini` file.
- **Network Issues:** Verify that the on-premises server can connect to the Google Cloud SFTP server.
- **File Permissions:** Ensure you have the necessary permissions to read files from the local directory and write to the remote directory.
