# Helm charts for Qstack

Subset of [Kubernetes Helm Charts](https://github.com/kubernetes/charts) as a default set for
Application Orchestration in [Qstack](https://qstack.com).


# How to update charts

Install and configure [Helm](https://github.com/kubernetes/helm])

## Configure repositories

```bash
helm repo add kubernetes-charts http://storage.googleapis.com/kubernetes-charts
```

## Clean previous charts

```bash 
rm -f ./charts/*
```

## Download all the charts in `charts.txt`

```bash 
for c in `cat charts.txt` ; do
    helm fetch --destination ./charts $c
done
```

## Create `index.yaml`

Note: You need to provide the url to the final location of the downloadable artifacts.

```bash 
helm repo index --url https://git.greenqloud.com/sverrir/qstack-helm/raw/master/charts/ ./charts
```
