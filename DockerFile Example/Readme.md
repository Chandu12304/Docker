## 1. Downloading and Running `hello-world` Docker Image

The `hello-world` image is a simple Docker image used for testing if Docker is installed correctly.

### Steps:
1. **Pull the Image from Docker Hub**:
   ```bash
   docker pull hello-world
   ```

2. **Run the Image**:
   ```bash
   docker run hello-world
   ```

This command will download the image (if not already downloaded) and run it, displaying a confirmation message that Docker is working properly.

![Hello World Output](https://i.imgur.com/1EE1omn.png)

---

## 2. Downloading and Running `ubuntu` Docker Image Interactively

The `ubuntu` image allows you to run a lightweight container with Ubuntu Linux. You can run this interactively, meaning you’ll get a terminal session inside the container to run commands just as you would on a regular Ubuntu system.

### Steps:
1. **Pull the Image from Docker Hub**:
   ```bash
   docker pull ubuntu
   ```

2. **Run the Image Interactively**:
   ```bash
   docker run -it ubuntu
   ```

   - The `-it` flag stands for "interactive" (`-i`) and "terminal" (`-t`), allowing you to interact with the container through a terminal.
   - This will start an interactive Ubuntu container and give you access to its shell. You can now run Ubuntu commands (e.g., `apt update`, `apt install`).

### Example Commands inside the Ubuntu container:
Once inside the Ubuntu container, you can install packages and run commands as if you were using a regular Ubuntu system:
```bash
ls
touch chandan.txt
ls
```
![Ubuntu Container Example](https://i.imgur.com/mWjE3BN.png)
