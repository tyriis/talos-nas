# talos setup

## generate secrets

```console
talhelper gensecret > talsecret.sops.yaml
```

## crypt secret

```console
sops -e -i talsecret.sops.yaml
```

## generate config

```console
talhelper genconfig
```

## install

```console
talosctl apply-config --nodes 192.168.1.57 \
          --file infra/talos/clusterconfig/kube-nas-kube-nas.yaml --insecure
```

## bootstrap

```console
talosctl bootstrap --nodes 192.168.1.57
```

## create kubeconfig

```console
talosctl kubeconfig \
          --talosconfig=infra/talos/clusterconfig/talosconfig \
          --nodes 192.168.1.57 \
          --endpoints 192.168.1.57 \
          --force
```

## install metrics server

```console
kubectl kustomize --enable-helm infra/talos/metrics-server | kubectl apply -f -
```

## install kubelet-csr-approver

```console
kubectl kustomize --enable-helm infra/talos/kubelet-csr-approver | kubectl apply -f -
```
