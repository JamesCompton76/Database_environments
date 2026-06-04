Overview

This repository serves as a centralized hub for Infrastructure as Code (IaC) configurations, utilizing YAML and Docker to systematically deploy, manage, and scale isolated database and distributed compute environments.

It provides a reproducible framework for spinning up complex, multi-container data architectures—ensuring exact parity across local development, testing, and staging environments without the overhead of manual configuration.
🏗️ Architectural Philosophy

In modern enterprise data engineering, environment consistency is critical. This project eliminates "it works on my machine" issues by fully containerizing both the transactional database layer and the analytical compute layer. Every environment is defined by declarative code, allowing for rapid deployment, stateless testing, and immediate teardown.
Tech Stack

    Containerization Engine: Docker

    Orchestration: Docker Compose

    Configuration: YAML

    Core Systems: Microsoft SQL Server (Replication Topology), PostgreSQL, Oracle, MongoDB, Apache Spark (Delta Lake), MinIO (S3-Compatible Storage)

    Host Environment: WSL2 / Linux

📦 Container Architecture & Service Registry

Executing the core compose configuration provisions a secure, interconnected bridge network (lab-net) containing the following isolated services:

    mssql (SQL Server Publisher): Primary SQL Server 2022 instance configured for Transactional Replication. Exposed on port 1433.

    mssql-secondary (SQL Server Subscriber): Secondary SQL Server 2022 instance acting as the replication target. Exposed on port 1434.

    postgres (PostgreSQL): Standard relational PostgreSQL database. Exposed on port 5433.

    oracle (Oracle Free 23c): Lightweight Oracle database environment. Exposed on port 1521.

    mongo (MongoDB): NoSQL document store. Exposed on port 27017.

    spark (Spark Master): Apache Spark master node configured with Delta Lake extensions. Exposes the Spark UI on 8080 and internal cluster communication on 7077.

    spark-worker (Spark Worker): Compute node bound directly to the Spark Master to execute distributed transformations. Shares a local ./delta_warehouse volume.

    minio (MinIO): S3-compatible object storage server for local data lake simulation. Exposes the API on 9000 and the Web Console on 9001.

Key Capabilities

    Rapid Provisioning: Spin up fully functional, isolated database servers and compute clusters in seconds using optimized docker-compose configurations.

    Network Isolation: Custom Docker bridge networks ensure secure, explicit communication between containerized services without exposing internal traffic.

    Volume Management: Configured persistent storage mapping (e.g., replica-data, minio-data, and local bind mounts) to ensure data survives container recreation.

    Resource Constraint Tuning: Memory and CPU limits defined at the container level to mimic production hardware constraints on local hardware.

Security & Configuration

All sensitive configurations, such as SA_PASSWORD, default user credentials, and specific port mappings, are stripped from the repository and handled via local .env files.

When cloning this repository, you must create an .env file in the root directory of the target environment utilizing the provided .env.example template.
