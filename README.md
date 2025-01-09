## Two-Tier-Application using Dockerfile

- First create a docker image from Dockerfile
```bash
docker build -t flaskapp .
```

- Now, make sure that you have created a network using following command
```bash
docker network create mynetwork
```

- Attach both the containers in the same network, so that they can communicate with each other

i) MySQL container 
```bash
docker run -d --name mysql --network mynetwork -p 3306:3306 -e MYSQL_ROOT_PASSWORD=Pass@123 -e MYSQL_DATABASE=mydb mysql:5.7

```
ii) Backend container
```bash
docker run -d --name flaskapp --network mynetwork -p 5000:5000 -e MYSQL_HOST=mysql -e MYSQL_USER=root -e MYSQL_PASSWORD=Pass@123 -e MYSQL_DB=mydb flaskapp:latest
```

## Notes

- Make sure to replace placeholders (e.g., `your_username`, `your_password`, `your_database`) with your actual MySQL configuration.
