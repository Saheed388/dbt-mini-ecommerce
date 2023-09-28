###  DBT Setup
1. Setup venv and activate venv
2. Install Requirements
3. Install extensions :Add to GIT Ignore, YAML, Better Jinja

**DBT-for-bigquery-set-up**
1. Set up dbt via command line: from https://docs.getdbt.com/docs/core/connect-data-platform/bigquery-setup#local-oauth-gcloud-setup
2. gcloud cli ..
2. Authenticate Big-Query - Run this line:
3.
For Mac or Linux
```
gcloud auth application-default login \
  --scopes=https://www.googleapis.com/auth/bigquery,\
https://www.googleapis.com/auth/drive.readonly,\
https://www.googleapis.com/auth/iam.test

```
For Windows:
```
gcloud auth application-default login --scopes=https://www.googleapis.com/auth/bigquery,https://www.googleapis.com/auth/drive.readonly,https://www.googleapis.com/auth/iam.test
```


**CREATING A NEW DBT PROJECT**
1. Get into a new project
2. Run: "dbt init" to create a project : input a name
name: your-project-name
chose database: [1] BigQuery
chose authentication: [1] oauth
enter GCP Project name OR ID:
enter dataset name
thread: 60
select;  US

# NOTE: Always ensure you are inside the folder that has your dbt virtual environment and that your virtual environment is activated

3. Run:
```
dbt debug --config-dir
```

4. open the profiles.yaml :  >> copy the dev profiles and create a productions profile : change the schema

create new branch by clicking on main: switch to the branch >> stage the changes and commit

**Install dbt power user extension:**
1. Search for dbt power user: install
2. Run " command shift p "
3. In the tab tha shows up search for user settings.json : open it and copy the below into the json file:
Add this to the file
```

    // Associated the right file types with the right VSCode extensions
    "files.associations": {
        "*.sql": "jinja-sql"
    },

    // CRUCIAL - you need to change this to terminal.integrated.env.[osx|windows|linux] depending on your system
    // and point it to the folder where your profiles directory is stored!
    "terminal.integrated.env.osx": {
        "DBT_PROFILES_DIR": "fill-this-with-the-path-to-the-folder-containing-your-profiles.yaml-file-on-your-local-file",
		"BIGQUERY_PROJECT": "fill-this-with-your-gcp-pproject-name"
   },

```
Above
 a. if you are on a mac you can add this  ```~/.dbt``` as ```DBT_PROFILES_DIR```
 b. add ```GCP-PROJECT-ID``` as  BIGQUERY_PROJECT NAME
 c. In the  ```terminal.integrated.env.osx``` tag replace "osx" with  either ```windows or linux``` depending on your system's OS

4. run "dbt clean && dbt deps"
5. Restart the vs code or run "command shift p" >> select reload window >> choose the correct python interpreter
6. check the models folder to see if the models have the dbt icon (it works successfully if it does)