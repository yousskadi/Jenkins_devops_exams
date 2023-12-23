# DATASCIENTEST JENKINS EXAM
# python-microservice-fastapi
Learn to build your own microservice using Python and FastAPI
Youssef KADI
## How to run??
 - Make sure you have installed `docker` and `docker-compose`
 - Run `docker-compose up -d`
 - Head over to http://localhost:8080/api/v1/movies/docs for movie service docs 
   and http://localhost:8080/api/v1/casts/docs for cast service docs


## Create Certificat
    1.  Install cert-manager


• kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.13.1/cert-manager.yaml

À partir de l’adresse <https://cert-manager.io/docs/installation/kubectl/> 

Installing cert-manager
	• It can be installed with a YAML manifest, or with Helm
	• Let's install the cert-manager Helm chart with this one-liner:

helm install cert-manager cert-manager \
--repo https://charts.jetstack.io \
--create-namespace --namespace cert-manager \
--set installCRDs=true
	
	• If you prefer to install with a single YAML file, that's fine too!

    2. Create a ClusterIssuer to obtain certificates with Let's Encrypt

        # ClusterIssuer manifest

          apiVersion: cert-manager.io/v1
          kind: ClusterIssuer
          metadata:
            name: letsencrypt-prod
          spec:
            acme:
          # Remember to update this if you use this manifest to obtain real certificates :
              email: ykadi.ykadi@gmail.com
          # server:https://acme-staging-v02.api.letsencrypt.org/directory
          # To use the production environment, use the following line instead:
              server: https://acme-v02.api.letsencrypt.org/directory
              privateKeySecretRef:
                name:  issuer-letsencrypt-prod
              solvers:
              - http01:
                  ingress:
                    class: nginx

      # Add to ingress resources:

          metadata:
             annotations:
                cert-manager.io/cluster-issuer: letsencrypt-prod

    and

          spec:
            tls:
            - hosts:
                - www.devops-youss.cloudns.ph
              secretName: letsencrypt-prod

          


