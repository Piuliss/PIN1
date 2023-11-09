# Getting Started

```
docker compose up

```

## Run Jenkins
Go to to: ```http://localhost:8080/```

Login with:
```admin / admin``


## Run Nexus (Repository of builds)
### After minutes, get the admin password 
```
docker exec -it pin1-nexus-1 cat /nexus-data/admin.password ; echo
```

Go to: ```http://localhost:8081/```

Login with: 
```
user: admin
password: <FROM /nexus-data/admin.password>
```
and change password to `Password1234.`


## PIN1
Evidencias de deploy a Nexus con docker-compose 
![image](https://github.com/tercemundo/PIN1/assets/1384962/da0c5890-a5b0-4aeb-bcb5-d374417826fe)