# TODO Application GitOps

## Overall architecture

![Architecture of Pipeline and GitOps](cicd.png "Architecture of Pipeline and GitOps")


## Prerequisites

- All projects are stored in GitHub repository
  - TODO application (Java)
    > Fork from this project: https://github.com/secangkirkopipanas/todo-application
  - TODO application (.NET)
    > Fork from this project: https://github.com/secangkirkopipanas/todo-dotnet-application
  - TODO application infrastructure configuration
    > Fork from this project: https://github.com/secangkirkopipanas/todo-application-infra
- [Openshift Pipeline](https://www.redhat.com/en/technologies/cloud-computing/openshift/pipelines) operator is installed
- [Openshift GitOps](https://www.redhat.com/en/technologies/cloud-computing/openshift/gitops) operator is installed
- [ACS](https://www.redhat.com/en/technologies/cloud-computing/openshift/advanced-cluster-security-kubernetes) operator is installed and configured
- [Quay](https://www.redhat.com/en/technologies/cloud-computing/quay) operator is installed
- [Sealed Secret operator (Bitnami)](https://github.com/bitnami-labs/sealed-secrets) is installed
- Required namespaces:
  - For pipeline and deployment to Dev:
    - todo-dev
  - For deployment to SIT and Prod:
    - todo-sit
    - todo-prod


## Notes for the implementation

### Check role for openshift-gitops namespace

```
$ oc patch cm/argocd-rbac-cm -n openshift-gitops --type=merge -p '{"data": { "policy.default": "role:admin" } }'
```

### Command to generate sealed secrets from secrets YAML

```
$ kubeseal --format yaml < [source-secrets.yaml] > [target-sealed-secrets].yaml
```
