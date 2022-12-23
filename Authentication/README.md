# Authentication



**Key ve CSR **
```
$ openssl genrsa -out cagatayakk.key 2048 

$ openssl req -new -key cagatayakk.key -out cagatayakk.csr -subj "/CN=cagatay@cagatayakk.net/O=DevTeam"
```

**CertificateSigningRequest **

```
$ cat <<EOF | kubectl apply -f -
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: cagatayakk
spec:
  groups:
  - system:authenticated
  request: $(cat cagatayakk.csr | base64 | tr -d "\n")
  signerName: kubernetes.io/kube-apiserver-client
  usages:
  - client auth
EOF
```

**CSR  ve crt**

```
$ kubectl get csr

$ kubectl certificate approve cagatayakk

$ kubectl get csr cagatayakk -o jsonpath='{.status.certificate}' | base64 -d >> cagatayakk.crt 
```

**kubectl config **

```
$ kubectl config set-credentials cagatay@cagatayakk.net --client-certificate=cagatayakk.crt --client-key=cagatayakk.key

$ kubectl config set-context cagatayakk-context --cluster=minikube --user=cagatay@cagatayakk.net

$ kubectl config use-context cagatayakk-context
```