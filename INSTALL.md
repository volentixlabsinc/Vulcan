helm init --service-account tiller --history-max 200

helm install --name my-release stable/bitcoind

# NOTES BitcoinD:
bitcoind RPC can be accessed via port 8332 on the following DNS name from within your cluster:
my-release-bitcoind.default.svc.cluster.local

To connect to bitcoind RPC:

1. Forward the port for the node:

  $ kubectl port-forward --namespace default $(kubectl get pods --namespace default -l "app=bitcoind,release=my-release" -o jsonpath="{ .items[0].metadata.name }") 8332

2. Test connection with user and password provided in configuration file:

  $ curl --user rpcuser:rpcpassword -k http://127.0.0.1:8332 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getinfo", "params": [] }' -H 'content-type: text/plain;'


# Notes: Installing k3s

Reference: https://dzone.com/articles/lightweight-kubernetes-k3s-installation-and-spring

## Get K3s

cd ~
mkdir k3sdownload
cd k3sdownload

Make sure you have get
```
which wget
```

should put
```
/usr/bin/wget
```

## Get K3S

You will need to replace <VERSION> with a valid K3s version from their release repository. You can get this information from the [the K3s release repository](https://github.com/rancher/k3s/releases)

```
wget https://github.com/rancher/k3s/releases/download/<VERSION>/k3s
```
For example, to get the v0.5.0 version, you would do the following:
```
wget https://github.com/rancher/k3s/releases/download/v0.5.0/k3s
```

Change the executable
```
chmod +x k3s
sudo mv k3s /bin
```

## Starting The Server


You will need to start the server with the following arguments:
```
sudo k3s server &
```
Test node:
```
sudo k3s kubectl get node
```

Test the instulation:
```
sudo k3s kubectl --all-namespaces=true get all
```