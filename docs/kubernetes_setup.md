Setup 4CeeD on Kubernetes Cluster 
====

*Disclaimer*: This is the recommended way to setup 4CeeD. This setup requires advanced users with Linux and cluster setup experience.

## Setup your own Kubernetes cluster

We have tested successfully with Kubernetes v1.6.6 on a cluster running Ubuntu 16.04 LTS. Please refer to [our official instructions](k8s_setup_ubuntu.md) to how to setup Kubernetes on your Ubuntu 16.04 LTS cluster.

To setup Kubernetes on other operating systems, pick your own Kubernetes deployment solution [here](https://kubernetes.io/docs/setup/pick-right-solution/). 

## Configure 4CeeD

Next, update configuration in `custom.conf` according to your Kubernetes setup:

* `KUBECTL`: Path to `kubectl` command
* `CURATOR_ADDR`: Addresses of the Curator and Uploader 
* `SMTP_SERVER`: Address of your SMTP server. Comment out or leave empty if email verification is not required
* `ADMIN_EMAIL`: Email address of 4CeeD's admin

Then, run `./reconf.sh` to refresh configuration information.

## Deploy 4CeeD on Kubernetes cluster

### Start 4CeeD 

Start all 4CeeD services by running the following command:
```
./startup.sh all
```

Wait until all 4CeeD services start (this process can take a while since it will require downloading a bunch of Docker images from Docker Hub). To check the status of all services, use the following command and make sure that all pods have status `Running`:

```
kubectl get pods --namespace=4ceed
```

### Access 4CeeD
When all servies have started, we can access 4CeeD at `$CURATOR_ADDR` as configured in `custom.conf`.

Please note that the first user that can sign-up to the system has to be the user with email in `ADMIN_EMAIL`.

### Stop 4CeeD
To stop all services, run the following command:
```
./shutdown.sh all
```

