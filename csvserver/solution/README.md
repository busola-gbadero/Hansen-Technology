Steps
1. Navigate to the demoserver Directory
`cd csvserver/demoserver/`

2. Build the Docker Image
`docker build -t demoserver:1.0 .`

3. Pull Prometheus Docker Image 

`docker pull prom/prometheus:v2.45.2`

4. Run the Docker Container
`docker run -d demoserver:1.0` . I found the issue and proceeded to the next step.

5. Created a bash script named `gencsv.sh` , Executed the script with arguments 2 and 8 to generate inputFile with 7 entries.

6. Run `docker run -d --name demoserver -v "$(pwd)/inputFile:/csvserver/inputdata" demoserver:1.0 sh -c "chmod +x /demoserver/demoserver && /demoserver/demoserver"`
The command sets up a Docker container named demoserver with the following objectives:
It ensures that the inputFile generated on the host machine is accessible inside the container at /csvserver/inputdata, allowing the application within the container to utilize this data.

Additionally, it grants executable permissions (chmod +x) to the application binary /demoserver/demoserver within the container. enabling the application to execute successfully.

Lastly, it initiates the execution of the demoserver application within the container, ensuring the application starts and operates according to its configured behavior.

7. `docker ps`  to check container status
`docker exec -it demoserver /bin/bash` to get shell access to the container

# Inside the container shell
Run `yum install -y net-tools` to install net-tools package
`netstat -tuln` to Check the port its listening on
`exit` to exit from container shell
Stop container and delete the running container

8. # Environment Variable

Run the image with volume mounting for inputFile and setting CSVSERVER_BORDER environment variable to Orange. Map port 9300 from the container to port 9393 on the host.

`docker run -d --name demoserver -v "$(pwd)/inputFile:/csvserver/inputdata" -e CSVSERVER_BORDER=Orange -p 9393:9300 demoserver:1.0 sh -c "chmod +x /demoserver/demoserver && /demoserver/demoserver"`

7. Access the Application
Access the application at `http://localhost:9393`

