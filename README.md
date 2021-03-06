# kind-codefresh-demo

A Codefresh step for creating an ephemeral [kind cluster](https://kind.sigs.k8s.io/) (Kubernetes in Docker). This is great if you need to quickly spin up a Kubernetes cluster for testing within a CI/CD pipeline, and then delete it.

### Background

Builds on the excellent work done by Jie Yu and Steven Chung to solve the problem of running kind within Kubernetes (as opposed to Docker Desktop). The step uses Docker images published in the "jieyu" Docker Hub account.

References:
- https://d2iq.com/blog/running-kind-inside-a-kubernetes-cluster-for-continuous-integration
- https://github.com/jieyu/docker-images/tree/master/dind

### How to install this step in your Codefresh account

Prerequisites:
- Codefresh account: https://codefresh.io/docs/docs/getting-started/create-a-codefresh-account/
- Codefresh Runner installed in your K8s cluster: https://codefresh.io/docs/docs/administration/codefresh-runner/
- Codefresh CLI installed: https://codefresh-io.github.io/cli/installation/
- yq 4+ installed: https://github.com/mikefarah/yq

```
# Look up the name of your Codefresh account.
codefresh auth get-contexts

# Update the name of the step so that it is namespaced with your account.
# Be sure to change "your-account-name" before running these commands!
CF_ACCOUNT=your-account-name
STEP=$CF_ACCOUNT/kind yq eval '.metadata.name = env(STEP)' -i step.yaml

# Install the step
codefresh create step-type -f step.yaml
```

### Now what?

After installing the step, you'll then be able to see it from the Codefresh IDE by clicking the **Steps** tab, then the **My Steps** tab.

This repo includes 2 example pipelines to illustrate how to use the step.
- `pipeline-examples/kind-with-typed-step.yaml` - this is the main example that shows the typical usage.
- `pipeline-examples/kind-with-freestyle-steps.yaml` - this exposes the step's underlying code as Freestyle steps, so that you can easily experiment with changes and additions.
