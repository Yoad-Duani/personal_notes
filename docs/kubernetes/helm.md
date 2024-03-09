# Helm

## Helm repos

```bash title="Add repo"
helm repo add MY_REPO_NAME REPO_URL
```

```bash title="List repos"
helm repo list
```

```bash title="Search chart"
helm search repo REPO_NAME -l
```

```bash title="Pull chart"
helm pull repo REPO_NAME/CHART_NAME --version VERSION
```
