### Vault Webhook Testing

**Deploy vault-webhook**

```
kubectl apply -f webhook/
```

**Deploy cert-manager**


```
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v0.16.0/cert-manager.yaml
```

**Create certificate and issuer**

```
kubectl apply -f issuer.yml -f certificate.yml
```

**Example**


* create serviceaccount

```
kubectl create sa myserviceaccount
```

* label the namespace

```
kubectl label namespace default vault-webhook=enabled
```

* create the `DatabaseCredentialBinding` CR

```
kubectl apply -f binding.yaml
```

* deploy the application

```
kubectl apply -f deployment.yml
```

* manually trigger cert-renewal

```
 kubectl cert-manager renew vault-webhook -n kube-system
 ```