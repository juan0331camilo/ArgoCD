DESPLIGUE DE APP USANDO KUBERNETES , DOCKER Y ARGO CD 

PASOS PARA EL DESPLIEGUE 

1 Clonar el repositorio 
https://github.com/juan0331camilo/ArgoCD.git

 2 Iniciar Minikube
 $ minikube start
$ minikube dashboard

3 Instalar e iniciar Argo CD:

Instalación del Chart

$ kubectl create ns argo-cd
$ helm repo add argo https://argoproj.github.io/argo-helm
$ helm install argocd argo/argo-cd -n argo-cd

para acceder a la interfaz se debe enviar la siguiente URL http://localhost:8080  

Después de acceder a la interfaz de usuario por primera vez, puede iniciar sesión con el nombre de 
usuario: admin y la contraseña aleatoria generada durante la instalación. Puede encontrar la contraseña ejecutando:
$ kubectl -n argo-cd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

4.Aplicar el archivo de ArgoCD: Aplica el archivo de ArgoCD para desplegar la aplicación en Kubernetes. Este archivo referencia la carpeta /dev 

$ kubectl apply -f application.yaml

# ArgoCD
![ARGO_CD01](https://github.com/juan0331camilo/ArgoCD/assets/54645813/e4402e34-b00c-4660-b6c7-192b5f95d0f9)

![argo_cd02](https://github.com/juan0331camilo/ArgoCD/assets/54645813/bd93e91c-56f3-4857-ac4f-e9c380b11660)

5. Obtener la URL del servicio: Obtén la URL para acceder a la aplicación a través de Minikube.

$ kubectl port-forward service/dockerapp-service -n dockerapp-namespace 8081:8080

6 Acceder a la aplicación http://localhost:8081/swagger 
![despliegueAPI](https://github.com/juan0331camilo/ArgoCD/assets/54645813/363cba9b-3f9d-4111-bdfd-b16010d92ff2)




