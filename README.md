## Run Jenkins

```
docker run -it --rm -p 8080:8080 -v /var/run/docker.sock:/var/run/docker.sock --name jenkins-curso docker.io/mguazzardo/pipe-seg
```

Go to to: ```http://localhost:808/```

Login with:
```admin / admin```


## Run Nexus (Repository of builds)


```
docker run -d -p 8081:8081 -p 8082:8082 -p 8083:8083 --name nexus -v nexus-data:/nexus-data sonatype/nexus3
```

### After minutes, get the admin password 
```
docker exec -it nexus cat /nexus-data/admin.password ; echo
```

Go to: ```http://localhost:8081/```

Login with: 
```
user: admin
password: <FROM /nexus-data/admin.password>
```
and change password to `Password1234.`