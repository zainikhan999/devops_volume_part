
 # Docker Volumes 

This project demonstrates the use of Docker volumes to share data between multiple containers. We use `nginx` and `httpd` containers to test volume persistence, serving HTML files from a shared volume.

---

## Step 1: Create Docker Volume

**Command:**
```bash
docker volume create my_volume
```
## Step 2: Run nginx container and mount the volume
**Command:**
```bash
docker run -d --name nginx-container -p 8080:80 -v my_volume:/usr/share/nginx/html nginx
```
## Step 3: Run nginx container and mount the volume
**Command:**
```bash
http://localhost:8080
```
## Step 4: Create index.html on host
**Command:**
```bash
echo "<h1>Hello from index.html</h1>" > index.html
```
## Step 5: Copy index.html to container volume
**Command:**
```bash
docker cp index.html nginx-container:/usr/share/nginx/html/index.html
```
## Step 6: Verify new index file is served
**Command:**
http://localhost:8080

## Step 7: Stop and remove nginx container
**Command:**
```bash
docker stop nginx-container
docker rm nginx-container
```
## Step 8: Run httpd container using same volume
**Command:**
```bash
docker run -d --name httpd-container -p 8081:80 -v my_volume:/usr/local/apache2/htdocs httpd
```
## Step 9: Verify index.html via httpd
**Command:**
```bash
http://localhost:8081
```
## Step 10: Create about.html on host
**Command:**
```bash
echo "<h1>About Page</h1>" > about.html
```
## Step 11: Copy about.html to volume
**Command:**
```bash
docker cp about.html httpd-container:/usr/local/apache2/htdocs/about.html
```
## Step 12: Verify about.html is accessible
**Command:**
```bash
http://localhost:8081/about.html
```
## Step 13: Stop and remove httpd container
**Command:**
```bash
docker stop httpd-container
docker rm httpd-container
```
## Step 14: Verify both HTML files exist in volume
**Command:**
```bash
docker run --rm -v my_volume:/data alpine ls /data

## Step 15: Cleanup - Remove the volume
**Command:**
```bash
docker volume rm my_volume
```
