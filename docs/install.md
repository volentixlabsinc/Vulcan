# Vulcan Install
The following guide you though the installation of Vulcan on your PC.

## Before You Begin

This tutorial assumes that you are running Linux on your machine and that you have some basic knowledge of git.

## Make Workspace

Create a workspace to manage the download of code and operational artifacts.

```
mkdir k3sdownloads
```

Navigate to the new directory:
```
cd k3sdownloads
```

Make sure you have the wget application:
```
which wget
```

If you do not receive the following, you will need to install it.
```
/usr/bin/wget
```

## Get K3S

[K3s](https://k3s.io/) is a very, very small version of Kubernetes. However, don't be fooled by its size. In short, K3s removes all the legacy code and not relivant code that has bloated kubernetes. For example, alpha releases are not supported. Similarily, cloud native service provider interfaces.

These limitations do not impeded Vulcan but rather empower it.

To install K3s, run the following, replacing the <VERSION> with a [valid k3s release](https://github.com/rancher/k3s/releases)
```
wget https://github.com/rancher/k3s/releases/download/<VERSION>/k3s
```

For example, to get the v0.5.0 version, you would do the following:
```
wget https://github.com/rancher/k3s/releases/download/v0.5.0/k3s
```

Make the downloaded k3s binary executable:
```
chmod +x k3s
```

Move it to the system path for programs:
```
sudo mv k3s /bin
```

Test the install using the following from the command line.
```
k3s
```

You should receive an output showing the `k3s` help documentation.

## Start The Server


Start the server and run it in the background:
```
sudo k3s server &
```
Give the server a few seconds to launch, and then test that the node has been created. If it has not, wait a few more seconds.
```
sudo k3s kubectl get node
```

Now that you know the node is up and running, you can test the infrustructure to make sure everything is running.
```
sudo k3s kubectl --all-namespaces=true get all
```

## Now What?

You can try installing VDex on your local Vulcan instance.