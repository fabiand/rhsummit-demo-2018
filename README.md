# Container-native Virtualization (CNV) Red Hat Summit Demo 2018

This repository contains a setup which is pretty close to the demo seen at Red
Hat Summit 2018.

This includes the eventually modified components:

- KubeVirt
- Client tools
- VM Template
- OpenShift Web Console

This does not include:

- CDI - Due to issues to deploy it robust in a generic setup
  [This script](https://github.com/aglitke/oc-kubevirt-up) also sets up the CDI, but is not as robust.
- Metrics - Unstable to deploy

# Requirements

- [OpenShift Client Tool v3.9.0](https://github.com/openshift/origin/releases/tag/v3.9.0) installed
- [`oc cluster up` configured](https://github.com/openshift/origin/blob/master/docs/cluster_up_down.md)
- [`virtctl` v0.4.1](https://github.com/kubevirt/kubevirt/releases/tag/v0.4.1)
  installed

# Usage

> **Note:** Take a look at the `.logs` file in case of an error or use
> `tail -f .logs` during deployment to view the status.

The `oc-kubevirt` script does all necessary steps:

```bash
$ ./oc-kubevirt
INFO Setting up the CNV Demo
INFO Setting up 'oc cluster up'
INFO Waiting for OpenShift to be fully up
INFO Deploying KubeVirt
INFO Deploying examples
INFO Granting additional permissions
INFO Using demo OpenShift Web Console image
INFO Done, connection details:
Logged into "https://127.0.0.1:8443" as "system:admin" using existing credentials.

You have access to the following projects and can switch between them with 'oc project <projectname>':

    default
    kube-public
    kube-service-catalog
    kube-system
  * myproject
    openshift
    openshift-infra
    openshift-node
    openshift-template-service-broker
    openshift-web-console

Using project "myproject".
OpenShift server started.

The server is accessible via web console at:
    https://127.0.0.1:8443

You are logged in as:
    User:     developer
    Password: <any value>

To login as administrator:
    oc login -u system:admin

INFO For CNV: Log into the web console as 'developer' and go to https://127.0.0.1:8443/console/project/myproject/overview
$
```

> **Note:** The virtual machines and templates are accessible in the project
> [_My Project_](https://127.0.0.1:8443/console/project/myproject/overview)

## User Guide

Once started, thre is the [KubeVirt user guide](http://docs.kubevirt.io/) to
work with the new entities.

## Cleanup

> **Note:** This will remove all `oc cluster` related data.

The setup can be cleaned using:

```bash
$ ./oc-cluster clean
```
