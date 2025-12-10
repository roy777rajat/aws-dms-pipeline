# Cost-Effective Modern Data Pipeline for Insurance Analytics

## Overview

This project implements a **cost-effective modern data pipeline** designed for insurance analytics using **AWS Database Migration Service (DMS)** and **Databricks**. The architecture leverages cloud-native services to extract, transform, and load (ETL) insurance data efficiently while maintaining optimal cost management and performance.

## Architecture

### Key Components

The data pipeline consists of the following components:

1. **Data Source** - Relational Databases
   - Insurance policy databases
   - Party/customer information databases
   - Historical transactional data

2. **AWS DMS (Database Migration Service)**
   - Continuous data replication from source databases
   - Real-time and batch data capture
   - Minimal downtime migration
   - Supports heterogeneous database sources

3. **Databricks**
   - Unified analytics platform
   - Apache Spark-based distributed processing
   - Data transformation and enrichment
   - ML capabilities for predictive analytics

4. **Data Lake**
   - Centralized data storage
   - Structured and unstructured data support
   - Cost-optimized storage tiers

### Data Flow

```
Source Databases
    ↓
AWS DMS (Replication Tasks)
    ↓
Data Lake (Bronze/Silver/Gold Layers)
    ↓
Databricks (ETL & Analytics)
    ↓
Insurance Analytics & Reports
```

## Project Structure

```
.
├── databricks/
│   ├── 01-FinancePipeLine-Party-Extract-Load.dbc
│   ├── 01-FinancePipeLine-Policy-Extract-Load.ipynb
│   └── 01-FinancePipeLine-Streaming-Party-Extract-Load.ipynb
├── init_sql/
│   └── schema.sql
├── docker-compose.yml
├── my-hand-book/
│   └── [Documentation and setup guides]
└── README.md
```

### File Descriptions

- **databricks/**: Contains Databricks notebooks for ETL operations
  - **Party Extract Load**: Handles party/customer data extraction and loading
  - **Policy Extract Load**: Processes insurance policy data
  - **Streaming Party Extract Load**: Real-time streaming operations for party data

- **init_sql/**: Database initialization scripts
  - **schema.sql**: Creates required database schema and tables

- **docker-compose.yml**: Docker configuration for local development and testing

- **my-hand-book/**: Setup guides and documentation
  - Docker setup instructions
  - SSH tunneling configuration for EC2 instances
  - Database and table architecture documentation

## Features

### 1. **Cost Efficiency**
- Leverages AWS DMS for efficient data migration
- Optimized Databricks cluster configuration
- Pay-as-you-go pricing model
- Reduced infrastructure management overhead

### 2. **Real-time Data Processing**
- Continuous data replication from source systems
- Streaming ingestion capabilities
- Near real-time analytics and insights

### 3. **Scalability**
- Handles growing data volumes seamlessly
- Distributed processing with Apache Spark
- Elastic resource allocation on Databricks

### 4. **Data Quality & Governance**
- Medallion Architecture (Bronze/Silver/Gold layers)
- Data validation and cleansing pipelines
- Audit trails and data lineage

### 5. **Insurance-Specific Analytics**
- Policy management and tracking
- Party/customer segmentation
- Risk assessment and pricing analytics
- Claims analysis and fraud detection capabilities

## Technology Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| Data Migration | AWS DMS | Source database replication |
| Analytics Engine | Databricks (Apache Spark) | Data processing and transformation |
| Data Storage | S3 / DBFS | Data lake storage |
| Orchestration | Databricks Workflows | Pipeline automation |
| Infrastructure | Docker, AWS | Containerization and cloud services |
| Notebooks | Databricks Notebooks | ETL development and testing |

## Prerequisites

- AWS Account with DMS and appropriate permissions
- Databricks Workspace
- Docker and Docker Compose (for local development)
- Source insurance database (PostgreSQL, MySQL, or Oracle)
- Python 3.7+

## Setup Instructions

### 1. Local Development Setup

```powershell
# Clone the repository
git clone https://github.com/roy777rajat/aws-dms-pipeline.git
cd finance-pipeline

# Start Docker services
docker-compose up -d

# Initialize database schema
docker-compose exec postgres psql -U postgres -f /init_sql/schema.sql
```

### 2. AWS DMS Configuration

1. Create a DMS replication instance
2. Configure source and target endpoints
3. Create replication task with continuous replication enabled
4. Monitor task status and data validation

### 3. Databricks Setup

1. Import notebooks into Databricks workspace
2. Configure cluster with appropriate compute resources
3. Set up mount points to S3 data lake
4. Configure secrets for database credentials
5. Execute ETL notebooks in sequence

### 4. SSH Tunneling for EC2

For secure remote access to databases:
- Refer to `my-hand-book/Setup Laptop to Ec2 SSH Tunneling.docx`
- Configure SSH key pairs
- Set up port forwarding

## Usage

### Running ETL Pipelines

1. **Party Data Pipeline**
   ```
   Run: 01-FinancePipeLine-Party-Extract-Load.dbc
   ```

2. **Policy Data Pipeline**
   ```
   Run: 01-FinancePipeLine-Policy-Extract-Load.ipynb
   ```

3. **Streaming Operations**
   ```
   Run: 01-FinancePipeLine-Streaming-Party-Extract-Load.ipynb
   ```

### Monitoring

- Monitor DMS replication tasks in AWS Console
- View Databricks job runs and logs
- Check data quality metrics in bronze/silver/gold layers

## Data Transformation Pipeline

### Bronze Layer
- Raw data from DMS replication
- Minimal transformations
- Maintains data lineage

### Silver Layer
- Data cleansing and validation
- Type conversions and standardization
- Deduplication and enrichment

### Gold Layer
- Business-ready analytics tables
- Aggregated and summarized data
- Optimized for reporting and ML

## Performance Optimization

1. **Partition Strategy**
   - Partition data by date and policy_type
   - Optimize query performance

2. **Clustering**
   - Cluster by frequently joined columns
   - Improve join performance

3. **Caching**
   - Cache intermediate DataFrames
   - Reduce redundant computations

4. **Resource Optimization**
   - Right-size Databricks clusters
   - Use spot instances for cost savings

## Cost Optimization Tips

- Use DMS for efficient migration with minimal downtime
- Leverage Databricks job clusters instead of all-purpose clusters
- Implement data retention policies for archived data
- Use S3 storage classes (Standard, IA, Glacier)
- Schedule jobs during off-peak hours
- Monitor and optimize cluster usage

## Troubleshooting

### Common Issues

1. **DMS Task Failures**
   - Check network connectivity to source database
   - Verify source endpoint credentials
   - Review DMS logs for detailed error messages

2. **Databricks Cluster Issues**
   - Verify IAM role permissions
   - Check cluster configuration
   - Review Spark job logs

3. **Data Quality Issues**
   - Validate source data format
   - Check schema compatibility
   - Review transformation logic in notebooks

## Security Best Practices

- Use AWS Secrets Manager for credential management
- Enable encryption for data in transit and at rest
- Implement network isolation with VPCs
- Use IAM roles for service authentication
- Enable audit logging and monitoring
- Implement least privilege access controls

## Contributing

Contributions are welcome! Please follow these guidelines:
1. Create a feature branch
2. Make your changes
3. Test thoroughly
4. Submit a pull request

## Documentation References

- [AWS DMS Documentation](https://docs.aws.amazon.com/dms/)
- [Databricks Documentation](https://docs.databricks.com/)
- [Apache Spark Documentation](https://spark.apache.org/docs/)
- [Insurance Analytics Best Practices](https://www.databricks.com/solutions/industries/insurance)

## Support

For issues, questions, or suggestions:
- Open an issue on GitHub
- Contact the development team

## License

This project is licensed under the MIT License - see LICENSE file for details.

## Authors

- **Rajat Roy** - Initial architecture and implementation
- Contributors welcome!

## Changelog

### Version 1.0.0 (December 2025)
- Initial release
- Party and Policy data pipelines
- Real-time streaming capabilities
- Docker-based local development setup

## Future Roadmap

- [ ] Implement advanced ML models for risk prediction
- [ ] Add real-time anomaly detection
- [ ] Expand to multi-source data federation
- [ ] Implement advanced data governance
- [ ] Create automated reporting dashboards
- [ ] Add data quality monitoring

## Acknowledgments

This project demonstrates industry best practices for building scalable, cost-effective data pipelines in the insurance sector using modern cloud technologies.

---

**Last Updated**: December 2025
