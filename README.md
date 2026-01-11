# Bank Microservices Configuration Repository

This repository serves as the **Centralized Configuration Storage** for the Bank Platform Microservices ecosystem. It follows the **Externalized Configuration** pattern to decouple environment-specific parameters from the application source code.

---

## 📂 Repository Structure

The configuration files are organized using the Spring Cloud Config naming convention: `{application-name}-{profile}.yml`.

| Service | Default Config | QA Environment | Production Environment |
| :--- | :--- | :--- | :--- |
| **Accounts** | `accounts.yml` | `accounts-qa.yml` | `accounts-prod.yml` |
| **Cards** | `cards.yml` | `cards-qa.yml` | `cards-prod.yml` |
| **Loans** | `loans.yml` | `loans-qa.yml` | `loans-prod.yml` |

## 🚀 Architectural Role



1. **Source of Truth:** All configurations are version-controlled in this Git repository.
2. **Config Server:** Acts as a centralized resource server that fetches YAML/Properties files and serves them via REST API.
3. **Microservices (Clients):** On startup, each service requests its specific configuration based on its `spring.application.name` and active `spring.profiles.active`.

---

## 🛠 Integration Guide

To connect your **Spring Cloud Config Server** to this repository, add the following configuration to your server's `application.yml`:

```yaml
spring:
  cloud:
    config:
      server:
        git:
          uri: [https://github.com/your-username/bankmicroservicesconfig.git](https://github.com/your-username/bankmicroservicesconfig.git)
          default-label: main
          clone-on-start: true
          force-pull: true
