## This repo for deploying [DevOps-Challenge app](https://github.com/tradebyte/DevOps-Challenge) in minikube cluster using helm##
After download helm go to this repo location in in your local machine write\
`helm install release1 .` to start the app and its environment \
then check your `minikube ip` and write it in the browser followed by `:30002`\
![This is an image](/myapp/images/python_run.png))\
## use Jenkins using helm ##
- get the repo 

 ```
 helm repo add jenkins https://charts.jenkins.io\
 helm repo update
 ```

- install chart \
`helm install jenkins-helm jenkins/jenkins`
\
after installation check the jenkins-helm service `kubectl get svc` if exist follow this instructions
- Edit jenkins-helm service expose jenkins with `NodePort` on the minikube cluster. \
`kubectl edit svc myjenkins` \
change `type` to `NodePort` and add `nodePort: 30010` in containers port section  

- get the minikube ip by using this command `minikube ip`.
- go to the browser and write this url `minikube-ip:30010` jenkins login page will appear
![This is an image](/myapp/images/jenkins_login.png) 

- get admin password by type \
`echo $(kubectl get secret --namespace default myjenkins -o jsonpath="{.data.jenkins-admin-password}" | base64 --decode)` 
- in the login page put this pasword and put username `admin`
