# conformity-migration-tool
Migrates your visiblity information in cloudconformity.com to cloudone.trendmicro.com

## **⚠ WARNING: This tool will overwrite your Cloud One Conformity**

## Requirements
1. Python v3.7+
2. API Keys for both Legacy Conformity and CloudOne Conformity
   - **Note:** Both API Keys must have admin privileges

## How to use this tool

1) Create or choose an empty folder where you would like to install and run the tool.

2) Start a shell/terminal on the folder you just created or chosen.

3) Create a python3 virtual environment (minimum: python v3.7)
    ```
    python3 -m venv .venv
    ```

4) Activate the virtual environment
   ```
   source .venv/bin/activate
   ```

5) Install the tool
    ```
    pip install conformity-migration-tool
    ```

6) Configure the tool
    ```
    conformity-migration configure
    ```

7) If you have AWS accounts, you have the option to use this CLI for updating your `ExternalId`:
   ```
   conformity-migration-aws generate-csv <CSV_FILE>
   ```
   Update your CSV file with your AWS credentials. Then use the updated csv to run the command below:
   ```
   conformity-migration-aws update-stack --csv-file <CSV_FILE>
   ```
   You can also run this CLI to update an invidual account's stack, which is useful if you want to
   wrap it in your own script that will iterate through all your accounts. To find those options,
   please run this command:
   ```
   conformity-migration-aws update-stack --help
   ```

8)  Run the migration
    ```
    conformity-migration run
    ```
    If you already updated your AWS accounts' `ExternalId` beforehand as in step 8, then you can add this
    option below so it will stop prompting you to update your ExternalId manually:
    ```
    conformity-migration run --skip-aws-prompt
    ```


## Migration support
### Cloud Types
- [X] AWS account
  - **Note:** To grant access to CloudOne Conformity, user has to update the `ExternalId` parameter of CloudConformity stack of his/her AWS account. This can be done either manually or using the CLI `conformity-migration-aws` which is part of the conformity-migration-tool package.

- [X] Azure account
  - **Note:** User needs to specify App Registration Key so the tool can add the Active Directory to Conformity
- [ ] GCP account

### Organisation-Level Configurations
- [X] Users
  - **Note**: The tool will display other users that needs to be invited by the admin to CloudOne Conformity.
- [X] Groups
- [X] Communication channel settings
- [X] Profiles
- [X] Report Configs

### Group-Level Configurations
- [X] Report Configs

### Account-Level Configurations
- [X] Account tags
- [X] Conformity Bot settings
- [X] Account Rule settings
  - **Limitation:** The API only allows writing a single note to the rule so the tool won't be able to preserve the history of notes. The tool will instead combine history of notes into a single note before writing it.
- [X] Communication channel settings
- [X] Checks
  - **Limitation:** The API only allows writing a single note to the check so the tool won't be able to preserve the history of notes. In addition to that, API only allows a maximum of 200 characters of note. The tool will only get the most recent note and truncate it to 200 characters before writing it.
- [X] Report Configs
