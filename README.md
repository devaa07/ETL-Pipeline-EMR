# ETL-Pipeline-EMR
Automate EMR ETL Jobs with Airflow

![Screen Shot 2024-01-02 at 10 58 40 PM](https://github.com/devaa07/ETL-Pipeline-EMR-/assets/126756574/49c6e41a-1441-4dae-a111-da2b49152c43)


# Step 1: Create an EC2 instance along with Key-pair and security group. Also, enable the port 8080 with HTTP for airflow

# Step 2: Install the following dependencies with superuser(use sudo)
          python3 --version
          sudo apt update
          sudo apt install python3-pip
          sudo apt install python3.10-venv
          python3 -m venv redfin_venv
          source redfin_venv/bin/activate
          pip install boto3
          pip install --upgrade awscli
          aws configure
          pip install apache-airflow
          pip install apache-airflow-providers-amazon

# Step 3:  Configure the aws cli with access key, secret key, region using aws configure command

# Step 4: create the s3 bucket and create the below foldes showing in the picture

<img width="1192" alt="Screen Shot 2024-01-02 at 11 04 53 PM" src="https://github.com/devaa07/ETL-Pipeline-EMR-/assets/126756574/d87dc69c-1095-495d-8a44-754d25168fe5">

# Step 5: Establish remote connection in VSCode and create the dag file: airflow/dags/redfin_analytics.py and start writing the dag code.
          redfin_analytics.py

# Step 6: Create the aws emr default role using below command
          aws emr create-default-roles

# Step 7: Now list the role using the below command
          aws iam list-roles | grep 'EMR_DefaultRole\|EMR_EC2_DefaultRole'

![Screen Shot 2024-01-02 at 11 10 26 PM](https://github.com/devaa07/ETL-Pipeline-EMR-/assets/126756574/99c00b30-3a4b-4588-b5ec-fd8790959ca5)

# Step 8: Create the VPC for the EMR 

<img width="904" alt="Screen Shot 2024-01-02 at 11 11 21 PM" src="https://github.com/devaa07/ETL-Pipeline-EMR-/assets/126756574/18365903-7553-4a62-8e16-6ac4328e0d8c">

# Step 9: Create the ingest.sh file with the below command to download the file and copy to s3 bucket. make sure this file is available in s3 bucket inside scripts folder
          wget -O - https://redfin-public-data.s3.us-west-2.amazonaws.com/redfin_market_tracker/city_market_tracker.tsv000.gz | aws s3 cp - s3://redfin-data-project-yml/store-raw-data-yml/city_market_tracker.tsv000.gz

# Step 10: Finaly update the code in the DAG file and trigger the DAG.

![Screen Shot 2024-01-02 at 11 16 44 PM](https://github.com/devaa07/ETL-Pipeline-EMR-/assets/126756574/7b2ca771-610b-4567-9d57-b7d016e58e90)

See the Snow pipe steps in other code repo.
