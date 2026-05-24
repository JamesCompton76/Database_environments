Overview

This repository serves as a centralized hub for Infrastructure as Code (IaC) configurations, utilizing YAML and Docker to systematically deploy, manage, and scale isolated database environments.

It provides a reproducible framework for spinning up complex, multi-container data architectures—ensuring exact parity across local development, testing, and staging environments without the overhead of manual configuration.
🏗️ Architectural Philosophy

In modern enterprise data engineering, environment consistency is critical. This project eliminates "it works on my machine" issues by fully containerizing the database layer. Every environment is defined by declarative code, allowing for rapid deployment, stateless testing, and immediate teardown.
Tech Stack

    Containerization Engine: Docker

    Orchestration: Docker Compose

    Configuration: YAML

    Core Systems: Microsoft SQL Server, PostgreSQL, Custom Networking (adjust list as needed)

    Host Environment: WSL2 / Linux

Key Capabilities

    Rapid Provisioning: Spin up fully functional, isolated database servers in seconds using optimized docker-compose configurations.

    Network Isolation: Custom Docker bridge networks to ensure secure, explicit communication between containerized services.

    Volume Management: Configured persistent storage mapping to ensure data survives container recreation.

    Resource Constraint Tuning: Memory and CPU limits defined at the container level to mimic production hardware constraints on local hardware.


Security & Configuration

All sensitive configurations, such as SA_PASSWORD and specific port mappings, are stripped from the repository and handled via local .env files.

When cloning this repository, you must create an .env file in the root directory of the target environment utilizing the provided .env.example template.
