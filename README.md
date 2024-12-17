# Novade Project Progress Report

*Update as of December 16, 2024*

---

## Introduction

This report presents the current status of the Novade project, which aims to migrate our technical infrastructure to a new architecture. The main goal is to centralize and process data from various sources such as Salesforce, Drift, and the tracking plan, to improve data storage and analysis in a Databricks/Azure/Amplitude environment.

### Key Points and KPIs

- **Project Duration**: To date, 16 workdays have been dedicated out of the planned 24 days, which is 80% of the allocated time.
- **Progress Made**: The majority of migration and integration scripts are in place, with ongoing tests to ensure stability and performance.
- **Major Challenges**: Adapting Databricks workflows for complex automations, and managing permissions with Amplitude, Azure, and Salesforce.
- **Envisioned Solutions**: Migration to more flexible solutions like Azure Blob Storage and Synapse Analytics for better data management.

This document is designed to provide a clear and accessible overview of the progress made, challenges encountered, and solutions considered. We remain committed to working closely with all stakeholders to ensure the success of this migration.

---

## 📊 Project Overview

The Novade project involves migrating from a proven solution (n8n/Segment/BigQuery) to a new architecture (Databricks/Azure/Amplitude). This transition aims to centralize and process data from various sources (Salesforce, Drift, tracking plan) to enhance data storage and analysis.

### Main Objectives
- **Complete infrastructure migration**
- **Data centralization in Databricks**
- **Implementation of automations**
- **Maintenance of service continuity**
- **Performance optimization**

---

## 📅 Project History

### Timeline of Meetings and Progress

#### Sprint 1: Weekly - November 12
- **Work Done**: Preparation of the first scripts on Databricks.
- **Encountered Issues**:
  - Problem creating Amplitude destination.
  - Authorization issue on GitHub.
- **Found Solutions**: No definitive solution at this stage.
- **Work Time**: 3 days.

#### Sprint 2: Weekly - November 18
- **Work Done**: Setup of the Amplitude connector to Databricks and testing.
- **Encountered Issues**:
  - Cost for about 1000 data points: €400.
  - Salesforce authorization problem for application creation.
- **Found Solutions**: No definitive solution at this stage.
- **Work Time**: 3 days.

#### Sprint 3: Weekly - November 26
- **Work Done**: Salesforce migration script creation and testing.
- **Encountered Issues**:
  - Data older than 1 month not importing into Databricks.
  - Data not being sent correctly.
- **Found Solutions**: Implementation of a double import to ensure all necessary data is transferred.
- **Cost**: About €50 for 200 events sent.
- **Work Time**: 3 days.

#### Sprint 4 and 5: Weekly - December 10
- **Work Done**: Creation of a local environment, deployment on Databricks or Azure when access to logs is available. Making scripts compatible for a dual environment.
- **Encountered Issues**:
  - Heavy architecture due to the triple environment.
  - Making scripts compatible for Azure/local and Databricks/local.
- **Found Solutions**: Creation of a local environment for testing.
- **Work Time**: 7 days.

#### Sprint 6: Weekly - December 17
- **Work Done**: Adjustments to make Spark and Salesforce libraries compatible.
- **Encountered Issues**:
  - Unstable Databricks clusters, frequent restarts.
- **Found Solutions**: Searching for a solution for a stable cluster.
- **Work Time**: 3 days.

---

## 🚨 Major Identified Issues

1. **Authorization Issues**: Limited access to necessary resources on Amplitude, Azure, and Salesforce.
2. **Development Environment**: Incompatibilities between local environments and Databricks, leading to instabilities.
3. **Data Management**: Difficulties in validating and integrating data from different sources.
4. **Limitations of Databricks Workflows**: Databricks workflows, mainly designed for data analysis and small periodic automations, do not effectively meet the requirements of our large-scale project that requires complex and continuous automations.

---

## 💡 Identified Solutions

The Databricks automation solutions imposed on me are far too costly and restrictive. Databricks is primarily dedicated to creating notebooks for data analysis or small automations. The creation of connectors also burdens the project.

### Proposed Solution

Amplitude has just created a new native Azure Blob Storage data destination. Here's how we can proceed:

1. **Amplitude → Azure Blob Storage**:
   - Export data from Amplitude (merged events, users) directly into Azure Blob Storage through native integration. Files are typically in JSON, CSV, or Parquet format.

2. **Azure Blob Storage → Azure Synapse Analytics**:
   - Load data into Synapse via:
     - **PolyBase**: Direct queries on Blob files without duplication.
     - **COPY INTO**: Importing files into internal tables for faster analysis.
   - **Automation**: Use Synapse Pipelines to schedule and orchestrate data flows between Blob Storage and Synapse.

### Automation Choices

For automation, you will need to choose between two options:

- **n8n**: If you opt for n8n, it will allow easy integration through already completed scripts. n8n is ideal for visual workflows and simple automations.
  
- **Python hosted on Azure Functions**: This option offers more flexibility and control over data processing but requires more technical management. This may be more suitable if complex processing is necessary.

### Revised Time Estimation

| Step                                         | Estimated Duration |
|----------------------------------------------|--------------------|
| Amplitude Export to Blob Storage             | 4 hours            |
| Blob Storage Loading to Synapse              | 5 hours            |
| Automation with Synapse Pipelines            | 6 hours            |
| Verifications and documentation              | 6 hours            |
| Installation of n8n on Azure                 | 4 hours            |
| Configuration of Python and automation framework | 4 hours          |
| Final tests and adjustments                  | 3 hours            |
| **Total Estimated**                          | **32 hours**       |

### Details of Revisions

- **Export and Loading**: An additional hour for each step to account for potential adjustments and performance testing.
- **Automation with Synapse Pipelines**: An extra hour to allow for more detailed configuration and integration testing.
- **Installation of n8n on Azure**: Two additional hours to include time for troubleshooting configuration and security issues.
- **Configuration of Python and automation framework**: An extra hour to ensure a complete installation of dependencies and initial tests.
- **Final tests and adjustments**: Three hours to test the entire system, adjust workflows, and ensure everything is functioning as expected.

These adjustments provide a buffer to manage unforeseen issues and ensure that the project stays on track while minimizing the risk of delays.

---

## ⚠️ Points of Caution

- **Authorization Monitoring**: Continue to monitor access to critical resources to prevent future blockages.
- **Stability of Environments**: Ensure that development and production environments remain synchronized and stable.
- **Documentation**: Maintain up-to-date documentation to facilitate communication between teams and ensure operational continuity.

---

This report aims to provide a clear and concise overview of the state of the Novade project, focusing on challenges and solutions. We remain committed to working closely with all stakeholders to ensure the success of this migration.
