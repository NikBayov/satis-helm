# Install satis-server by helm for kubernetes(k8s,k3s)

### 1. Create namespace 
```
kubectl create ns satis
```
### 2. Download project
```
https://github.com/NikBayov/satis-helm.git && cd satis-helm
```
### 3. Edit values.yaml
You need to replace your values in [values.yaml](./values.yaml)

### 4. Edit ConfigMap
You need to add your composer packages in [ConfigMap](./templates/configmap-satis.yaml)

### 5. Install satis
```
helm upgrade --install satis . -n satis -f values.yaml
```

### 6. Build and download packages(I did manual)
```
kubectl create job --from=cronjob/satis-build satis-manual-$(date +%s) -n satis
```
### 7. Awaiting completion of the job and checking the result
![Alt text](https://github.com/NikBayov/Administration/blob/main/cache/picture/satis.png)

## Notes
To add new packages, you need to add them to the [ConfigMap](./templates/configmap-satis.yaml) and run:
```
user@server:/satis-helm# helm upgrade satis . -n satis -f values.yaml && kubectl create job --from=cronjob/satis-build satis-manual-$(date +%s) -n satis
```
