# Maven Pipeline

The following repo contains the Tekton Pipeline which executes the following jobs:

- Clone the repo using `git-clone` Task.
- Executes the following maven goals using `maven` Task:
  - mvn-clean-compile
  - mvn-test
  - mvn-package
- Create image and deploy on openshift using `openshift-client` Task.

> Note: The following Pipeline is equivalent to the Jenkinsfile present [here](https://github.com/rupalibehera/jboss-eap-quickstarts/blob/7.1.x-develop/helloworld/Jenkinsfile).

## Install

1. [`git-clone`](https://hub.tekton.dev/tekton/task/git-clone)
2. [`maven`](https://hub.tekton.dev/tekton/task/maven)
3. [`openshift-client`](https://hub.tekton.dev/tekton/task/openshift-client)

4. Create the secret which contains the kubeconfig of openshift.

```sh
kubectl create secret generic kubeconfig --from-file="<path/to>/kubeconfig"
```

5. `Maven Pipeline`

```sh
kubectl apply --filename maven-pipeline.yaml
```

6. Create the PipelineRun

```sh
kubectl apply --filename maven-pipeline-run.yaml
```
