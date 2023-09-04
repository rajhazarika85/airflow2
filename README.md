# Airflow 2.x
Implementation of Airflow 2.x

# Apache Airflow 2.x Setup Guide for macOS

This guide provides step-by-step instructions on how to set up Apache Airflow 2.x on macOS using docker compose. 
Apache Airflow is a platform for programmatically authoring, scheduling, and monitoring workflows.

## Prerequisites
Before you begin, make sure you have the following prerequisites installed on your Mac:

- Python 3.x
- Pip

## Step 1: Install Homebrew
If you don't have Homebrew installed, you can do so by running the following command in your Terminal:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```


## Step 2: Install Dependencies
```
brew install python@3.9
```
You can use a different Python version if you prefer, but Python 3.9 is recommended for Apache Airflow 2.x.

## Step 3: Run postgresql in Docker using docker compose
- This configuration includes the PostgreSQL service and exposes the default PostgreSQL port (5432) for external connections.
- Open a terminal in the same directory as the docker-compose.yml file.
- Run the following command to start the PostgreSQL container:
```
docker-compose up -d
```
- This will launch the PostgreSQL container in the background. You can now connect to your PostgreSQL database using the specified credentials and hostname (usually "localhost" since it's running on the same machine) and port 5432.


## Step 4: Install Apache Airflow
Install Apache Airflow and its extras package via pip:
This command installs Apache Airflow along with several extras that provide additional features and integrations.

```
pip install "apache-airflow[postgres,async,cncf.kubernetes,crypto,http,ldap,password,redis]"
```

## Step 5: Initialize Airflow Database
Initialize the Airflow database using the provided command-line tool:
```
airflow db init
```
## Step 6: Start the Webserver and Scheduler
```
airflow webserver --port 8080
airflow scheduler
```
The web server will be available at http://localhost:8080/. You can access the Airflow UI from your web browser.
- username: admin
- password: admin

There is no default username and password created if you are just using python wheel.

Run the following to create a user:

For Airflow >=2.0.0:
```
airflow users  create --role Admin --username admin --email admin --firstname admin --lastname admin --password admin
```
OR

For Airflow <1.10.14:
```
airflow create_user -r Admin -u admin -e admin@example.com -f admin -l user -p admin
```

## Step 7: Optional Configuration
- If you want to use a different database backend, update the database connection string in the airflow.cfg file.

- Install additional dependencies for specific use cases as needed.

## Additional Resources
- https://airflow.apache.org/docs/apache-airflow/stable/start/index.html
- That's it! You now have Apache Airflow 2.x set up on your Mac. You can start creating and managing your workflows using the Airflow web UI or the command-line interface.


## Github setup
- Set Your Git Username:
```
git config --global user.name "Your Name"
```
- Set Your Git Email:
```
git config --global user.email your.email@example.com
```
- Verify Your Git Configuration:
```
git config --global --get user.name
git config --global --get user.email
```
- To push the current branch and set the remote as upstream, use
```
git push --set-upstream origin airflow-setup
```