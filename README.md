# Docker

**Docker** is a tool that allows developers to create, package, and run applications in lightweight, isolated environments called **containers**. These containers include everything needed to run the application, such as the code, dependencies, and configurations, ensuring it works consistently across different systems.

### **Understanding Docker Images and Containers**

![Docker](https://i.imgur.com/N5cOuPS.png)

1. **Docker Image**:
   - A Docker image is a **blueprint** or **template** that contains:
     - The application’s code.
     - All required dependencies, libraries, and modules (with specific versions).
     - Environment configurations and settings.
   - It is a **read-only file** that defines what is needed to create a running application environment.

2. **Container**:
   - A container is a **running instance** of a Docker image.
   - When a Docker image is transferred to another system and run, it creates a **container**.
   - The container:
     - Provides an **isolated environment** for the application.
     - Ensures the application runs consistently, regardless of the underlying system.

3. **Key Process**:
   - **Create a Docker Image**: Package the application and its environment.
   - **Transfer the Image**: Share the image with other systems.
   - **Run the Container**: The image is used to spin up an isolated and consistent environment for the app.

---

The isolated environment created by Docker (i.e., the container) will run within a **Linux subsystem** (such as **WSL 2** on Windows) or a native Linux kernel. This subsystem interacts with the host operating system to access and manage the necessary resources, such as CPU, memory, and storage, while maintaining the isolation of the container. 

### Organized Explanation:
1. **Isolated Environment**: 
   - Docker containers create isolated environments to run applications.
  
2. **Running Environment**: 
   - On **Linux** hosts, containers run directly on the Linux kernel.
   - On **Windows** or **macOS**, Docker uses a **Linux subsystem** (e.g., WSL 2 or a virtual machine) to simulate a Linux environment for the container.

3. **Interaction with Host OS**: 
   - The subsystem or virtual machine interacts with the **host operating system** to manage resources.
   - The container accesses CPU, memory, storage, and other resources through this interaction, while still being isolated from the host and other containers.

This ensures that containers run with the necessary resources while maintaining their isolation from the host system and other containers.

---

### **1. The Role of Linux Subsystem**
Docker containers rely on **Linux kernel features** (like namespaces and cgroups) to provide isolation and resource management. Since these features are native to Linux, Docker needs a Linux environment to run.

- On a **Linux Host**: Docker interacts directly with the Linux kernel, so no extra subsystem is needed.
- On **Non-Linux Hosts** (like Windows or macOS): Docker uses a lightweight Linux virtual machine or the **Windows Subsystem for Linux (WSL 2)** to provide this environment.

---

### **2. Interaction Between Components**
When a container runs:
1. **Docker Engine**:
   - It manages the lifecycle of containers (creation, starting, stopping, etc.).
   - It translates high-level commands (e.g., `docker run`) into actions that interact with the Linux kernel.

2. **Linux Subsystem or Virtual Machine**:
   - If you're on **Windows or macOS**, Docker uses a Linux virtual machine or WSL 2 to provide the necessary Linux kernel features.
   - This Linux environment is lightweight and optimized for Docker's needs.

3. **Host OS Resources**:
   - Containers do not emulate hardware like traditional virtual machines. Instead, they **share the host's kernel** and directly access system resources (CPU, memory, storage, etc.), but in a controlled and isolated way using **cgroups**.
   - For example:
     - If your app in the container needs to access files, it interacts with the Linux subsystem, which translates those requests for the host OS.

---

### **3. How It Works on Different Operating Systems**
#### **Linux Host**
- Docker runs natively and uses the host’s Linux kernel for container management.
  
#### **Windows Host**
- **Older Docker Versions**: Used Hyper-V to create a small Linux virtual machine.
- **Modern Docker (With WSL 2)**:
  - Leverages the **Windows Subsystem for Linux (WSL 2)**.
  - WSL 2 runs a lightweight Linux kernel inside Windows.
  - Containers run within this Linux environment, and WSL communicates with the Windows OS to access resources.

#### **macOS Host**
- Uses a virtual machine (VM) powered by tools like HyperKit or VirtualBox to provide a Linux kernel.
- The containers run inside this VM.

---

### **4. Simplified Flow**
1. **Docker Command**: You issue a command (e.g., `docker run`).
2. **Docker Engine**: It communicates with the Linux environment (Linux kernel or WSL 2).
3. **Linux Kernel Features**:
   - Provides isolation and resource management.
   - Runs the container as an isolated process.
4. **Host OS Resources**:
   - The Linux environment interacts with the host OS to allocate necessary resources like CPU, memory, and storage.

---

**Virtual Machines (VMs)** are a traditional way to run multiple applications with different environments simultaneously on a single physical machine while achieving **isolation**.

### **How VMs Achieve Isolation:**

1. **Full Virtualization**:
   - Each VM runs its own **full operating system (OS)**, separate from the host OS. 
   - It has its own kernel, libraries, and dependencies, so different environments can coexist on the same physical machine.

2. **Complete Isolation**:
   - VMs provide complete isolation between applications because each VM is a self-contained system.
   - The VM’s environment is isolated from others, so different applications with different OSes and configurations can run without interference.

---

### **VMs vs. Docker Containers**

While VMs can achieve isolation, **Docker containers** provide a more lightweight alternative. Here's a comparison:

| Feature              | Virtual Machines (VMs)             | Docker Containers               |
|----------------------|------------------------------------|----------------------------------|
| **Isolation**        | Full isolation with separate OS    | Process-level isolation (shares OS kernel) |
| **Resources**         | Heavy on resources (each VM includes a full OS) | Lightweight (only the app and dependencies) |
| **Startup Time**      | Minutes (due to booting the OS)    | Seconds (since containers share the host OS) |
| **Performance**       | Slower (due to virtualization overhead) | Faster (direct access to host OS kernel) |
| **Portability**       | Less portable (depends on VM software) | Highly portable (runs anywhere Docker is installed) |

---

### **Summary**:
- **VMs** can run multiple applications with different environments by fully virtualizing separate OSes.
- However, **Docker containers** achieve similar isolation but are more lightweight, faster, and more resource-efficient because they share the host's kernel instead of running full OSes.

So, while VMs are an older and heavier solution for running multiple isolated environments, **Docker** provides a more efficient and flexible way to do this in modern development.


Reference videos:- 
https://youtu.be/17Bl31rlnRM?si=2yH3EaDA-RdYj5op

https://youtu.be/H8Lyj2D_cWo?si=qktXTVqHwybtKf0H