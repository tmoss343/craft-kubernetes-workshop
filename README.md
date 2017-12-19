# Augemented Craft Kubernetes Workshop for EngTech's uses

In this workshop you will learn how to:

* Connect to a kubernetes instance and interact with it using kubectl
* Deploy and manage Docker containers using kubectl

Kubernetes Version: 1.6.6

## Access

### Clone this Repository

```
git clone https://github.com/tmoss343/craft-kubernetes-workshop.git
```

### Entering the cluster

You can either [install the azure cli](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest) or you can run the cli from a container, if you choose the container route your volumes will need to be set up correctly.
```
docker run -it -p 81:8080 -v C:/dockervolumes/azure:/root/.ssh -v C:/Repo/craft-kubernetes-workshop:/workshop-files azuresdk/azure-cli-python bash
```

After you have gotten your cli running login to azure
```
az login
az account show
az account set --subscription {subscription-id}
```

You will want to connect to the Kubernetes instance after this. You will need to have your ssh keys set up to access the instance. In lastpass there will be an entry for Kubernetes-playground ssh keys that will give you access to the keys. If you are running in a container then you can see from the example command above how we mount the ssh keys to the ssh directory so you have access to the cluster. For windows machines connection to the kube instance you will want to put the ssh keys in your `%USERPROFILE%/.ssh` directory.

```
az acs kubernetes install-cli
az acs kubernetes get-credentials --resource-group=kubernetes-playground --name=kubernetes-playground
```

At this point you should be able to run `kubectl get all --all-namespaces` and you should see a buch of resources returned and bam you are in. If you have any trouble connecting check you ssh keys are correct and that you have the right version of python installed on your machine.

## Managing Applications with Kubernetes

Kubernetes is all about applications and in this section you will utilize the Kubernetes API to deploy, manage, and upgrade applications. In this part of the workshop you will use an example application called "app" to complete the labs.

[App](https://github.com/kelseyhightower/app) is hosted on GitHub and provides an example 12 Factor application. During this workshop you will be working with the following Docker images:

* [kelseyhightower/monolith](https://hub.docker.com/r/kelseyhightower/monolith) - Monolith includes auth and hello services.
* [kelseyhightower/auth](https://hub.docker.com/r/kelseyhightower/auth) - Auth microservice. Generates JWT tokens for authenticated users.
* [kelseyhightower/hello](https://hub.docker.com/r/kelseyhightower/hello) - Hello microservice. Greets authenticated users.
* [ngnix](https://hub.docker.com/_/nginx) - Frontend to the auth and hello services.

#### Labs

  * [Creating and managing pods](labs/creating-and-managing-pods.md)
  * [Monitoring and health checks](labs/monitoring-and-health-checks.md)
  * [Managing application configurations and secrets](labs/managing-application-configurations-and-secrets.md)
  * [Creating and managing services](labs/creating-and-managing-services.md)
  * [Creating and managing deployments](labs/creating-and-managing-deployments.md)
  * [Rolling out updates](labs/rolling-out-updates.md)

## Further tutorials

  * [Published by Kubernetes themselves](https://kubernetes.io/docs/tutorials/)
  * [Examples included in the Kubernetes source](https://github.com/kubernetes/examples)
  * [For the adventurer Kelsey Hightower publishes a ton of tutorials to poke around in, most are really really good (this is one of them just augmented a bit!!)](https://github.com/kelseyhightower)

## Links

  * [Kubernetes](http://googlecloudplatform.github.io/kubernetes)
  * [azure cli Tool Guide](https://docs.microsoft.com/en-us/cli/azure/overview?view=azure-cli-latest)
  * [Docker](https://docs.docker.com)
  * [etcd](https://coreos.com/docs/distributed-configuration/getting-started-with-etcd)
  * [nginx](http://nginx.org)
