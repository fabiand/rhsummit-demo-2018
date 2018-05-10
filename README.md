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

> **Note:** The required setup time is heavily depending on the speed of your
> internet connection.

The `oc-cnv` script does all necessary steps, you can pass the `-v` flag
to see all the relevant calls done to perform the setup.

```bash
$ ./oc-cnv
INFO Setting up the CNV Demo (this can take a few minutes)
INFO Setting up 'oc cluster'
INFO Waiting for OpenShift to be fully up
INFO Deploying KubeVirt
INFO Deploying examples
INFO Granting additional permissions
INFO Switching to the OpenShift Web Console demo image
INFO Done, connection details:

> Logged into "https://127.0.0.1:8443" as "system:admin" using existing credentials.
> 
...
> 
> Using project "myproject".
> OpenShift server started.
> 
> The server is accessible via web console at:
>     https://127.0.0.1:8443
> 
> You are logged in as:
>     User:     developer
>     Password: <any value>
> 
> To login as administrator:
>     oc login -u system:admin

INFO For CNV: Log into the web console as 'developer' and go to https://127.0.0.1:8443/console/project/myproject/overview
$
```

> **Note:** Once setup, the virtual machines and templates are accessible in
> the project
> [_My Project_](https://127.0.0.1:8443/console/project/myproject/overview)

## virtctl

In order to start, stop, and connect to a virtual machine console you can use
the `virtctl` tool:

```bash
$ ./virtctl-v0.4.1-linux-amd64 start testvm
$ ./virtctl-v0.4.1-linux-amd64 vnc testvm
$ ./virtctl-v0.4.1-linux-amd64 stop testvm
```

## CLI

The provided template can also be used to instantiate a new virtual machine from
the CLI using:

```bash
$ oc login -u developer
Logged into "https://127.0.0.1:8443" as "developer" using existing credentials.
...
Using project "myproject".

$ oc new-app --template cirros-vm-template -p NAME=second
--> Deploying template "myproject/cirros-vm-template" to project myproject

     CirrOS Virtual Machine
     ---------
     OCP KubeVirt CirrOS VM template

     * With parameters:
        * NAME=second
        * MEMORY=512Mi
        * CPU_CORES=2

--> Creating resources ...
    offlinevirtualmachine "second" created
--> Success
    Run 'oc status' to view your app.

$
```

## User Guide

Once started, thre is the [KubeVirt user guide](http://docs.kubevirt.io/) to
work with the new entities.

## Cleanup

> **Note:** This will remove all `oc cluster` related data.

The setup can be cleaned using:

```bash
$ ./oc-cnv clean
```
