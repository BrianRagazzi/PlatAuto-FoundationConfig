# PlatAuto-FoundationConfig
Configuration Files for foundations deployed and maintained via Platform Automation Pipelines

These files are used to deploy foundations pks and pas to my homelab environment


# Configuring credhub clients:

1. Point UAAC at the UAA server
> uaac target https://uaa.pae.ragazzilab.com:8443 --skip-ssl-validation

2. Get admin token (retrieve secret from opsgr)
> uaac token client get admin -s <SECRET>

3. Add credhub client (in this case, named "credhub")
> uaac client add --name credhub --scope uaa.none --authorized_grant_types client_credentials --authorities "credhub.write,credhub.read"  Enter clientID and secret when prompted

4. Login to credhub as admin
> credhub login --server "https://credhub.pae.ragazzilab.com:8844" --client-name "credhub_admin_client" --client-secret <SECRET> --skip-tls-validation

5. Add permissions in credhub to new client
> credhub set-permission -a uaa-client:credhub -p /concourse/* -o read,write,delete

> credhub set-permission -a uaa-client:credhub -p /foundation/* -o read,write,delete
