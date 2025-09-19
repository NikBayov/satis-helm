# Install satis-server by helm for kubernetes(k8s,k3s)

### 1. Create namespace 
```
kubectl create ns satis
```
### 2. Move to the project folder
```
cd satis-helm
```
### 3. Edit ConfigMap
You need to add your composer packages in [ConfigMap](./templates/configmap-satis.yaml)

### 4. Install satis
```
helm upgrade --install satis . -n satis -f values.yaml
```

### 5. Build and download packages(I did manual)
```
kubectl create job --from=cronjob/satis-build satis-manual-$(date +%s) -n satis
```
### Awaiting completion of the job and checking the result
![Alt text](https://github.com/NikBayov/Administration/blob/main/cache/picture/satis.png)
