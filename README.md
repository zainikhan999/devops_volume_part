
 # Docker Volumes 

This project demonstrates the use of Docker volumes to share data between multiple containers. We use `nginx` and `httpd` containers to test volume persistence, serving HTML files from a shared volume.

---

## Step 1: Create Docker Volume

**Command:**
```bash
docker volume create my_volume
```
![image](https://github.com/user-attachments/assets/fdeede13-930a-4285-bcfb-de42f556b6e4)

## Step 2: Run nginx container and mount the volume
**Command:**
```bash
docker run -d --name nginx-container -p 8080:80 -v my_volume:/usr/share/nginx/html nginx
```
![image](https://github.com/user-attachments/assets/79c16b47-8d63-4987-b395-b44fed196cbb)

## Step 3: Verify Negix default page
**Command:**
```bash
http://localhost:8080
```
![image](https://github.com/user-attachments/assets/c0365945-dca1-4695-a513-88083fba897e)

## Step 4: Create index.html on host
**Command:**
```bash
echo "<h1>Hello from index.html</h1>" > index.html
```
![image](https://github.com/user-attachments/assets/9a971512-6b97-49a7-82ea-48679cfa4304)


## Step 5: Copy index.html to container volume
**Command:**
```bash
docker cp index.html nginx-container:/usr/share/nginx/html/index.html
```
![image](https://github.com/user-attachments/assets/198e3659-a84f-4263-920e-9fd2aa59d602)

## Step 6: Verify new index file is served
**Command:**
http://localhost:8080

## Step 7: Stop and remove nginx container
**Command:**
```bash
docker stop nginx-container
docker rm nginx-container
```
![image](https://github.com/user-attachments/assets/281b0490-b985-42ce-9355-376a83717c8b)

## Step 8: Run httpd container using same volume
**Command:**
```bash
docker run -d --name httpd-container -p 8081:80 -v my_volume:/usr/local/apache2/htdocs httpd
```
![image](https://github.com/user-attachments/assets/3af95316-1512-425e-b792-a292f409058e)

## Step 9: Verify index.html via httpd
**Command:**
```bash
http://localhost:8081
```
![image](https://github.com/user-attachments/assets/b008670a-1d15-49ee-9690-b3c3312b7a3c)

## Step 10: Create about.html on host
**Command:**
```bash
echo "<h1>About Page</h1>" > about.html
```
![image](https://github.com/user-attachments/assets/2d8aee29-6079-485c-a84c-eead7a700e79)

## Step 11: Copy about.html to volume
**Command:**
```bash
docker cp about.html httpd-container:/usr/local/apache2/htdocs/about.html
```
![image](https://github.com/user-attachments/assets/729aa7f9-5655-48f4-85d8-9e2ec6eac5ce)

## Step 12: Verify about.html is accessible
**Command:**
```bash
http://localhost:8081/about.html
```
![image](https://github.com/user-attachments/assets/83019e22-ff3d-4b0b-a3e0-65548fc2fe70)

## Step 13: Stop and remove httpd container
**Command:**
```bash
docker stop httpd-container
docker rm httpd-container
```
![image](https://github.com/user-attachments/assets/6916fcaa-1fd1-4c5e-a63f-de5ea709dd9e)

## Step 14: Verify both HTML files exist in volume
**Command:**
```bash
docker run --rm -v my_volume:/data alpine ls /data
```
![image](https://github.com/user-attachments/assets/b1afa582-48b1-4cca-8b5e-4ba9deb2d733)


## Step 15: Cleanup - Remove the volume
**Command:**
```bash
docker volume rm my_volume
```
![image](https://github.com/user-attachments/assets/04cf4295-2625-48f9-8118-6aedbda9a7ae)

