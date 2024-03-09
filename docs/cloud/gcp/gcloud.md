# gcloud

## cluster commands

```bash
gcloud container clusters list

gcloud container clusters get-credentials CLUSTER_NAME --region REGION --project PROJECT_ID

gcloud container node-pools list  --cluster CLUSTER_NAME --region REGION

gcloud container node-pools list  --cluster=CLUSTER_NAME --format="table(name,version,config.imageType)" --region REGION

gcloud container node-pools describe NODE-POOL_NAME --cluster=CLUSTER_NAME --region=REGION

gcloud container clusters describe CLUSTER_NAME --region=REGION
```

## storage commands

```bash title="Storage commands"
gsutil ls gs://<gcs_name>

gcloud storage cp <file/folder> gs://<gcs_name> --recursive
```

## disk commands

```bash
gcloud compute disks list --filter="-users:*"
```
