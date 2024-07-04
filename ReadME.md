# File Transfer from On-Premises Server to Google Cloud

This guide provides a detailed process for securely migrating files from an on-premises server to Google Cloud. The migration script includes configuration settings, batch script files for password or PPK-based authentication, and the necessary tools.

## Prerequisites

Before you start, ensure you have the following:
- Access to the on-premises server where the files are located.
- Google Cloud storage setup and SFTP credentials.
- A zip file containing the migration script.

## Step-by-Step Process

### 1. Extract the Migration Script

1. Download the zip file containing the migration script to your on-premises server.
2. Extract the contents of the zip file. It should contain:
    - `config.ini` (configuration file)
    - `file_transfer_pwd.bat` (batch script for password-based authentication)
    - `file_transfer_ppk.bat` (batch script for PPK-based authentication)
    - `psftp.exe` (PSFTP application for file transfer)

### 2. Configure `config.ini`

Open the `config.ini` file in a text editor and provide the necessary details:
sftp_ip = <your_sftp_server_ip>
user = <your_username>
password = <your_password_if_using_password_auth>
ppk_path = <path_to_your_ppk_file_if_using_ppk_auth>
source_dir = <path_to_your_data_files_folder>
hotel_name = <your_hotel_name>
file_type = <file_format_e.g._csv,zip,txt>

### 3. Running the Batch Script

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