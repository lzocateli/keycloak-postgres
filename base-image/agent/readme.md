```powershell
podman build -t nuuve.jfrog.io/nuuve-docker/keycloak:postgresql-1.0.0 .
```
- Upload your image to your container registry:

```powershell
podman push nuuve.jfrog.io/nuuve-docker/keycloak:postgresql-1.0.0
```

##### Where:
- `nuuver` = Your docker registry   
- `keycloak` = Your path in docker registry   
- `postgresql-1.0.0` = Your image tag name    
