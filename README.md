# Fetch Rewards #
## Data Engineering Take Home: ETL off a SQS Qeueue ##

This project is the solution for the Data Engineering assignment given in the below link:
https://bitbucket.org/fetchrewards/data-engineering-take-home/src/master/

## To run the code
1. Clone this repo.
```bash
git clone https://github.com/prasadashu/data-engineering-fetch-rewards.git
```

2. Go into the cloned repo.
```bash
cd data-engineering-fetch-rewards
```

3. Run `make` command to install dependencies.
```bash
make pip-install
```

4. Run `make` command to configure aws shell.
```bash
make aws-configure
```

5. Pull and start docker containers.
```bash
make start
```

6. Run Python code to perform ETL process.
```bash
make perform-etl
```

## Checking messages loaded in Postgres
- To validate the messages loaded in Postgres
```bash
psql -d postgres -U postgres -p 5432 -h localhost -W
```
- Credentials and database information
    - **username**=`postgres`
    - **password**=`postgres`
    - **database**=`postgres`

- If `psql` binary is not installed on Ubuntu based distros, install it using the below command.
```bash
apt install postgresql-client
```

## Decrypting masked PIIs
- The `ip` and `device_id` fields are masked using base64 encryption.
- To recover the encrypted fields, we can use the below command.
```bash
echo -n "<sample_base64_encrypted_string>" | base64 --decrypt
```


## :eyes: Assumptions: 

1. The SQS Queue contains JSON data with a consistent structure, containing fields like `user_id`, `device_type`, `ip`, `device_id`, `locale`, `app_version`, and `create_date`.
2. The PII data (IP and device_id) can be masked using a one-way hashing algorithm (e.g., SHA-256) to preserve uniqueness while ensuring that the original data cannot be easily recovered.
3. The PostgreSQL database is set up with the correct table schema to store the processed records.
4. The provided Docker Compose file sets up the local development environment, and no additional configuration is required for local testing.
5. The ETL pipeline is designed to be executed as a standalone script and does not include advanced features like scheduling or error handling.

## :runner:Next Steps: 

1. Add error handling and retries for reading from SQS and writing to PostgreSQL.
2. Implement logging and monitoring to track the application's performance and detect issues.
3. Develop a scheduling mechanism or run the ETL pipeline as a service to process new data periodically.
4. Optimize the data processing, for example, by processing messages in batches to improve performance.
5. Implement more comprehensive tests, including integration and end-to-end tests.

### :raising_hand: Deployment in Production: 

To deploy this application in production, we could use a managed container orchestration service like AWS Fargate or Kubernetes -- it would allow us to easily manage, scale, and monitor the application in a production environment.:grin:

### :speech_balloon: Production-Ready Components:

In order to make this application production-ready, we could add the following components:

1. Centralized logging with services like AWS CloudWatch or ELK Stack (Elasticsearch, Logstash, Kibana) for easy log management and analysis.
2. Monitoring and alerting with tools like Grafana, Prometheus, or Datadog to track the performance and health of the application.
3. CI/CD pipeline for automated building, testing, and deployment of the application.

### :muscle: Scaling with a Growing Dataset:

Finally, to scale this application with a growing dataset, we could take the following approaches depending on our dev environment:

1. Implement ---> horizontal scaling by adding more instances of the ETL application, allowing it to process data concurrently.
2. Optimize database performance with proper indexing, partitioning, and sharding strategies.
3. Use a message broker like Apache Kafka or Amazon Kinesis to handle high throughput and enable data streaming.


