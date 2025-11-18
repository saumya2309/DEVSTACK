# DEVSTACK





| Feature | **DevStack** | **Packstack** |
|--------|--------------|--------------|
| Purpose | Development & testing environment for OpenStack | Simplified deployment method for OpenStack (PoC / lab use) |
| Target Audience | Developers, contributors | System admins, testers |
| Installation Source | Builds from source | Installs from RPM packages |
| Deployment Type | Temporary, disposable | Semi-persistent (lab / demo) |
| Speed | Faster to deploy & reset | Slower initial setup |
| Flexibility | Very flexible & hackable | Limited customization |





---



## ✅ **DevStack Installation Guide (Ubuntu 22.04 / 20.04)**

### **1. System Requirements**

| Requirement | Value                              |
| ----------- | ---------------------------------- |
| OS          | Ubuntu 22.04 / 20.04 (recommended) |
| RAM         | 8 GB minimum (16 GB preferred)     |
| CPU         | 4 cores minimum                    |
| Disk        | 30+ GB free                        |
| User        | Non-root **sudo** user             |
| Networking  | Internet access required           |

---

### **2. Prepare System**

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install git -y
sudo apt install python3-dev python3-pip -y
```

Create a non-root `stack` user (DevStack requires it):

```bash
sudo useradd -s /bin/bash -d /opt/stack -m stack
echo "stack ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/stack
```

Switch to stack user:

```bash
sudo su - stack
```

---

### **3. Clone DevStack**

```bash
git clone https://opendev.org/openstack/devstack
cd devstack
```

---

### **4. Create `local.conf`**

```bash
nano local.conf
```

Paste:

```ini
[[local|localrc]]
ADMIN_PASSWORD=admin
DATABASE_PASSWORD=$ADMIN_PASSWORD
RABBIT_PASSWORD=$ADMIN_PASSWORD
SERVICE_PASSWORD=$ADMIN_PASSWORD
HOST_IP=127.0.0.1

# Recommended services
enable_service horizon
enable_service glance
enable_service keystone
enable_service neutron
enable_service nova
enable_service placement-api
```

Save & exit.

---

### **5. Start Installation**

```bash
./stack.sh
```



---

### **6. Access OpenStack Dashboard**

After successful install:

Open browser:

```
http://<your-ip>/dashboard
```

Username:

```
admin
```

Password:

```
admin
```

---




### **7. Manage DevStack**

Stop DevStack:

```bash
./unstack.sh
```

<img width="1919" height="629" alt="Screenshot 2025-11-18 235020" src="https://github.com/user-attachments/assets/717f9482-985a-469f-924c-d5b5f129f4a5" />
<img width="1919" height="1031" alt="Screenshot 2025-11-18 234847" src="https://github.com/user-attachments/assets/0c02eff0-aa37-4fc2-8e0d-5232af7a8307" />



