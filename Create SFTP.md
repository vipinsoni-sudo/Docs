I'll help you rewrite this AWS SFTP Server setup guide with correct grammar and improved clarity.

***

## AWS SFTP Server Setup Guide

### Create SFTP Server

1. Search for **AWS Transfer Family** in the AWS console search bar and click on it
2. Click **Create server**
3. Select **SFTP (SSH File Transfer Protocol)** - File Transfer over Secure Shell, then click **Next**
4. Select **Service managed** and click **Next**
5. Keep the default options as they are and click **Next**
6. Select **Amazon S3** as the storage option and click **Next**
7. Leave the default options and click **Next**
8. Review the final configuration before clicking **Create SFTP Server**

### Create IAM Policy

1. Search for **IAM** in the search bar and navigate to the IAM console
2. Click on **Policies** in the left-hand menu, then click **Create policy**
3. Select **S3** in the "Select a service" option
4. Under "Actions allowed", select **List**, **Read** (full), and **Write** permissions
5. Select **bucket** and **object** in the Resources section, then click **Next**
6. Enter a policy name in the "Policy name" input field and click **Create policy**

### Create IAM Role

1. Click on **Roles** in the left-hand menu, then click **Create role**
2. Select **AWS service** and choose **Transfer** in the "Use case" section, then click **Next**
3. Search for your policy name in the "Add permissions" section and select it, then click **Next**
4. Enter a role name in the "Role name" input field and click **Create role**

### Create SFTP User

1. Search for **AWS Transfer Family** and navigate to the AWS Transfer Family console
2. Click on your created server and select **Add user** in the Users section
3. Enter a username in the "Username" input field
4. Choose the IAM role you created and select **Auto-generate policy based on home folder**
5. Select your S3 bucket in the "Home directory" section and enter the folder name you want to access via SFTP
6. Paste your SSH public key in the provided field

### Generate SSH Public Key for SFTP User

1. Open your terminal or command prompt and enter: `ssh-keygen -m PEM -f "Name_of_the_key_file"`, then press Enter
2. Enter a passphrase when prompted and press Enter to confirm

### Test SFTP Server - Upload & Download Files

1. Navigate to the **AWS Transfer Family** console, click on your server name, and copy the **Endpoint URL** from the Endpoint Details section
2. Open PowerShell on Windows and enter: `sftp -i "private_key_file_name" username@sftp_endpoint`
3. Enter the passphrase you created when generating the public key

**If connected successfully, use these commands:**

**Upload a file:**
```
put "file_path_with_full_path"
```

**Download a file:**
```
get "file_name"
```

**List all files:**
```
ls
```

***

**Note:** The correct SFTP connection command should be `sftp -i "private_key_file" username@endpoint` (with a hyphen before the `i` flag and including the username with @ symbol before the endpoint).