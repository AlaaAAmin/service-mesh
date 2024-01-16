# First steps with Istio

## Deploying Istio in Kubernetes
Steps:
1. Have kubernetes (this could be any variant of kubernetes).
2. Download istioctl to be to install Istio and interact with it.
3. Download Istio distribution from the Istio release page at https://github.com/istio/istio/releases and download the distribution for your operating system.  
Alternatively, you can run this handy script: `curl -L https://istio.io/downloadIstio | ISTIO_VERSION=1.13.0 sh -`
4. Run `istioctl version` to verify that everything is working as expected.
5. let’s verify that any prerequisites have been met in our Kubernetes cluster (such as the version) and identify any issues we may have before we begin the installation. through the command `istioctl x precheck` 
At this point, we’ve downloaded the distribution files and verified that the istioctl CLI tools are a fit for our operating system and Kubernetes cluster.  
Next, let’s do a basic installation of Istio to get hands-on with its concepts.  
  
In the distribution you just downloaded and unpacked, the manifests directory contains a collection of charts and resource files for installing Istio into the platform of your choice.  
  
The official method for any real installation of Istio is to use istioctl, istio-operator, or Helm.  

6. `$ istioctl install --set profile=demo -y`
✔ Istio core installed  
✔ Istiod installed  
✔ Ingress gateways installed  
✔ Egress gateways installed  
✔ Installation complete