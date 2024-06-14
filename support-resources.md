# Support Resources for Openshift 

### Openshift ROSA with Private Link
#### 1. How can I assist if the customer has lost access to the OpenShift cluster via both the console and the API?

- Check the cluster with ocm backplane, if the cluster is healthy, the issue is on the customer side.
- Suggest the customer to check the following Items:
  - [ ] VPN
  - [ ] [AWS firewall prerrequisites](https://access.redhat.com/documentation/en-us/red_hat_openshift_service_on_aws/4/html/prepare_your_environment/rosa-sts-aws-prereqs#osd-aws-privatelink-firewall-prerequisites_rosa-sts-aws-prereqs)
  - [ ] [DNS forwarding](https://docs.aws.amazon.com/rosa/latest/userguide/getting-started-private-link.html#getting-started-private-link-step-4)
  - [ ] Route 53 Resolver inbound endpoint

References: 
- [Getting started with ROSA classic using AWS PrivateLink](https://docs.aws.amazon.com/rosa/latest/userguide/getting-started-private-link.html)
- [Troubleshoot ROSA cluster creation issues](https://docs.aws.amazon.com/rosa/latest/userguide/troubleshoot-rosa-cluster-provisioning.html)

#### 2. OpenShift commands - Tips

**Check nodes:**
~~~
$ oc get nodes

$ oc adm top nodes
~~~

**Check pods:**
~~~
$ oc get pods

$ oc adm top pods
~~~

Check all pods in a namespace for validation::

If you have several pods with failures, you can check the Exit code for each pod and troubleshoot.
~~~
$ oc get pods -o yaml |grep -i code
~~~
Example:

```
    - name: myapp-container
      state:
        terminated:
          exitCode: 137
          reason: OOMKilled
          startedAt: "2023-06-12T10:34:56Z"
          finishedAt: "2023-06-12T10:35:00Z"
```
When filtering with grep -i "Exit code", you would get:

```
exitCode: 1
exitCode: 0
exitCode: 137
```