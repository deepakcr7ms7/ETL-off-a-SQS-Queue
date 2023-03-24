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


#

### Quesstions:

### 1)Deployment in Production: 

First , we need to set up the production environment. This may involve creating a virtual machine or a container orchestration platform such as Kubernetes or Amazon ECS.

Then we can deploy the Docker image to the production environment. This can be done using a container orchestration platform such as Kubernetes or Amazon ECS, which can automatically manage the deployment, scaling, and monitoring of your containers.

### 2) Production-Ready Components:

In order to make this application production-ready, we could add the following components:

Centralized logging: Using tools like ELK Stack, Splunk, or AWS CloudWatch to collect and analyze logs from different parts of the application can help identify and debug issues quickly.

Monitoring and alerting: Tools like Prometheus, Grafana, or New Relic can provide visibility into application performance, resource utilization, and other key metrics. Alerting can be set up to notify the team when metrics exceed predefined thresholds.

CI/CD pipeline: Automating the building, testing, and deployment of the application using tools like Jenkins, Travis CI, or GitLab CI/CD can help reduce manual errors and improve deployment speed.

Scalability: Implementing horizontal scaling using load balancers like HAProxy, Nginx, or Amazon ELB can help ensure high availability and handle spikes in traffic.


Security: Implementing security measures like encryption, role-based access control, and web application firewalls can help protect against threats like data breaches and DDoS attacks.

Disaster recovery: Implementing backup and recovery processes, including data replication and automated failover, can help ensure business continuity in the event of a disaster.

Performance optimization: Regular performance testing and optimization, including database tuning and resource allocation, can help ensure the application is performing efficiently.

Compliance: Ensuring the application is compliant with relevant regulations and standards, such as HIPAA, PCI DSS, and GDPR, can help mitigate legal and financial risks.

Documentation and training: Providing documentation and training for support and maintenance teams can help ensure the application is well-understood and properly managed over time.

### 3)Scaling with a Growing Dataset:

Finally, to scale this application with a growing dataset, we could take the following approaches depending on our dev environment:

Increase the number of ETL worker instances: As the size of the dataset grows, you may need to increase the number of worker instances that are processing messages from the SQS Queue. This can be achieved by either launching additional EC2 instances or scaling out the containers running the ETL workers in a containerized environment.

Use Autoscaling: Autoscaling can be used to automatically adjust the number of worker instances based on the size of the queue. When the number of messages in the queue grows, additional worker instances can be launched to handle the increased load. When the queue size decreases, the number of worker instances can be scaled down.

Implement a distributed ETL process: A distributed ETL process can be implemented to divide the processing load across multiple worker instances. This can be achieved using technologies like Apache Spark or Apache Flink, which can distribute the processing of data across a cluster of worker nodes.

Optimize the ETL process: The ETL process should be optimized to handle large amounts of data efficiently. This can involve optimizing queries, reducing the number of database or API calls, and using caching mechanisms to reduce the amount of data that needs to be processed.

Use a Data Pipeline service: Use a managed data pipeline service like AWS Glue or Azure Data Factory to automate and manage the ETL process. These services can automatically scale and optimize the processing of data based on the size of the queue.

### 4) assumptions I made :

The data in the SQS Queue is in a consistent format.

The SQS Queue can handle the volume of data.

The ETL process can handle duplicates, missing data nad delayed messages.

The ETL process can handle errors and failures

