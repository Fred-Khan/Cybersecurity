### Steps to Install OWASP Juice Shop on Amazon Linux 2 Using Docker

Below are the detailed steps to install Docker, pull the Juice Shop image, and run it on  fresh Amazon Linux 2 EC2 instance. These assume you're logged in as the default `ec2-user` with sudo privileges. Run all commands in the terminal.

1. **Update the System Packages**  
   This ensures your instance has the latest security patches and dependencies.  
   ```
   sudo yum update -y
   ```

2. **Install Docker**  
   Amazon Linux 2 uses yum as the package manager. Install Docker directly from the repositories.  
   ```
   sudo yum install docker -y
   ```

3. **Start and Enable the Docker Service**  
   Start Docker and enable it to run on boot.  
   ```
   sudo systemctl start docker
   sudo systemctl enable docker
   ```

4. **Add Your User to the Docker Group**  
   This allows you to run Docker commands without sudo (recommended for ease of use). Replace `ec2-user` if you're using a different username.  
   ```
   sudo usermod -a -G docker ec2-user
   ```  
   After this, log out and log back into your SSH session for the group change to take effect. You can verify with `groups` (you should see `docker` in the list).

5. **Verify Docker Installation**  
   Check that Docker is running correctly.  
   ```
   docker --version
   ```  
   And run a test container:  
   ```
   docker run hello-world
   ```  
   If it works, you'll see a "Hello from Docker!" message.

6. **Pull the OWASP Juice Shop Docker Image**  
   The official image is hosted on Docker Hub.  
   ```
   docker pull bkimminich/juice-shop
   ```

7. **Run the Juice Shop Container**  
   This command runs the container in detached mode (-d), maps port 80 on  EC2 instance to port 3000 inside the container (-p 80:3000), and gives it a name for easy reference.  
   ```
   docker run -d -p 80:3000 --name juice-shop bkimminich/juice-shop
   ```  
   - After running, access Juice Shop by visiting `http://<-ec2-public-ip>` in a web browser.  
   - Note: Ensure  EC2 security group allows inbound traffic on port 80 (HTTP) from  IP or 0.0.0.0/0 (for public access, but be cautious as this exposes the vulnerable app).  
   - If port 80 is already in use (e.g., by httpd), stop the conflicting service with `sudo service httpd stop` or choose a different host port.
   - You can add `--restart=always` to the run command so it auto-starts the container on reboots.

8. **Verify the Container is Running**  
   Check the status:  
   ```
   docker ps
   ```  
   You should see the `juice-shop` container listed with ports mapped as `0.0.0.0:80->3000/tcp`.

If something goes wrong, check logs with `docker logs juice-shop` or restart the container with `docker restart juice-shop`.

---

### Docker Images vs. Containers: Key Differences

Before diving into commands, it's essential to understand the core concepts:

- **Docker Image**: A static, immutable blueprint or snapshot of an application and its environment. It's like a read-only template that includes the code, runtime, libraries, and dependencies needed to run the app. Images are built in layers (e.g., from a Dockerfile) and stored locally or on registries like Docker Hub. You can't change an image once it's built—you create new ones for updates.  
  - Example: When you run `docker pull bkimminich/juice-shop`, you're downloading the Juice Shop image, which contains the vulnerable web app ready to run.  
  - View images with `docker images`.

- **Docker Container**: A runnable instance of an image. It's like starting a virtual machine from a disk image—containers are dynamic and can be started, stopped, or modified during runtime. Multiple containers can run from the same image (e.g., several Juice Shop instances). Changes inside a container (like adding files) don't affect the original image unless you commit them to create a new image.  
  - Example: `docker run ... bkimminich/juice-shop` creates and starts a container from the image.  
  - View containers with `docker ps` (running) or `docker ps -a` (all).

In short: Images are the "recipes" (built once, used many times); containers are the "dishes" (prepared from recipes, consumable instances). This separation enables portability and scalability.



### Common Docker Commands for Beginners

Docker is a tool for running applications in isolated containers. Here's a list of the most commonly used commands to help you get started. These cover listing images and containers, starting/stopping, and cleanup. Run them without sudo if you're in the docker group (from step 4 above).

- **List Installed Images**: Shows all Docker images on  system, including size and creation date.  
  ```
  docker images
  ```

- **List Running Containers**: Displays currently running containers with details like ID, name, status, and ports.  
  ```
  docker ps
  ```

- **List All Containers (Running and Stopped)**: Useful to see everything, including stopped ones.  
  ```
  docker ps -a
  ```

- **Start a Stopped Container**: Replace `<container_id_or_name>` with the ID or name (e.g., `juice-shop`).  
  ```
  docker start <container_id_or_name>
  ```

- **Stop a Running Container**: Gracefully stops the container.  
  ```
  docker stop <container_id_or_name>
  ```

- **Restart a Container**: Stops and starts it in one go.  
  ```
  docker restart <container_id_or_name>
  ```

- **View Logs for a Container**: Shows output from the container (great for debugging). Add `-f` to follow live logs.  
  ```
  docker logs <container_id_or_name>
  ```

- **Remove a Container**: Deletes a stopped container (use `docker stop` first if it's running). Add `-f` to force removal if running.  
  ```
  docker rm <container_id_or_name>
  ```

- **Remove an Image**: Deletes an image (ensure no containers are using it; remove them first if needed).  
  ```
  docker rmi <image_id_or_name>
  ```

- **Pull an Image from Docker Hub**: Downloads an image (e.g., for updates).  
  ```
  docker pull <image_name>
  ```

- **Run a New Container**: Basic command to start a container from an image. Options like `-d` (detached), `-p` (ports), `--name` (custom name) are common.  
  ```
  docker run [options] <image_name>
  ```

- **Search for Images on Docker Hub**: Finds available images.  
  ```
  docker search <keyword>
  ```

- **Clean Up Unused Resources**: Removes stopped containers, dangling images, etc., to free space.  
  ```
  docker system prune
  ```

For more details, run `docker --help` or `docker <command> --help` (e.g., `docker run --help`). 
Explore the official Docker docs at https://docs.docker.com for more information.
