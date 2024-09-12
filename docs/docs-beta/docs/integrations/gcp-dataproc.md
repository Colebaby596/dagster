---
layout: Integration
status: published
name: GCP Dataproc
title: Dagster & GCP Dataproc
sidebar_label: GCP Dataproc
excerpt: Integrate with GCP Dataproc.
date: 2022-11-07
apireflink: https://docs.dagster.io/_apidocs/libraries/dagster-gcp
docslink: 
partnerlink: 
logo: /integrations/gcp-dataproc.svg
categories:
  - Compute
enabledBy:
enables:
---

### About this integration

Using this integration, you can manage and interact with Google Cloud Platform's Dataproc service directly from Dagster. This integration allows you to create, manage, and delete Dataproc clusters, and submit and monitor jobs on these clusters.

### Installation

```bash
pip install dagster-gcp
```

### Examples

```python
from dagster import asset, Definitions
from dagster_gcp.dataproc import DataprocResource


dataproc_resource = DataprocResource(
    project_id="your-gcp-project-id",
    region="your-gcp-region",
    cluster_name="your-cluster-name",
    cluster_config_yaml_path="path/to/your/cluster/config.yaml",
)


@asset
def my_dataproc_asset(dataproc: DataprocResource):
    with dataproc.get_client() as client:
        job_details = {
            "job": {
                "placement": {"clusterName": dataproc.cluster_name},
            }
        }
        client.submit_job(job_details)


defs = Definitions(
    assets=[my_dataproc_asset], resources={"dataproc": dataproc_resource}
)
```

### About Google Cloud Platform Dataproc

Google Cloud Platform's **Dataproc** is a fully managed and highly scalable service for running Apache Spark, Apache Hadoop, and other open source data processing frameworks. Dataproc simplifies the process of setting up and managing clusters, allowing you to focus on your data processing tasks without worrying about the underlying infrastructure. With Dataproc, you can quickly create clusters, submit jobs, and monitor their progress, all while benefiting from the scalability and reliability of Google Cloud Platform.