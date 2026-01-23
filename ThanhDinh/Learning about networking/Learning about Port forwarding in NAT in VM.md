Great idea—port forwarding in VMs is easiest to understand by _doing_ it.

Below is a **simple, concrete lab** you can run locally in ~10 minutes.  
It works with **VirtualBox** or **VMware**, and mirrors real-world usage.

---

## Goal of the Lab

You will:

- Run a web server **inside a VM** (listening on port `80`)
    
- Configure **port forwarding** so:
    
    ```
    Host machine: http://localhost:8080
            ↓
    VM:            http://<vm-ip>:80
    ```
    
- Verify that traffic from your host reaches the VM
    

---

## Step 1 – Create a VM with NAT networking

1. Create or use any Linux VM (Ubuntu is easiest).
    
2. Set its network adapter to **NAT**.
    

### VirtualBox

```
Settings → Network → Adapter 1 → Attached to: NAT
```

### VMware

```
VM Settings → Network Adapter → NAT
```

---

## Step 2 – Install and run a web server inside the VM

Inside the VM terminal:

```bash
sudo apt update
sudo apt install -y nginx
sudo systemctl start nginx
```

Verify inside the VM:

```bash
curl http://localhost
```

You should see HTML output like:

```
Welcome to nginx!
```

---

## Step 3 – Add a port forwarding rule

### Option A — VirtualBox GUI

```
Settings → Network → Adapter 1 → Advanced → Port Forwarding
```

Add a rule:

| Name | Protocol | Host IP   | Host Port | Guest IP | Guest Port |
| ---- | -------- | --------- | --------- | -------- | ---------- |
| web  | TCP      | 127.0.0.1 | 8080      |          | 80         |

> Leave **Guest IP empty** (VirtualBox fills it automatically).

#### Why Guest IP Can Be Empty in VM Port Forwarding (NAT)

**Short answer:**  
In NAT mode, the hypervisor already knows which VM the port-forwarding rule belongs to.

**Explanation:**

- Each VM in VirtualBox NAT has its **own NAT engine**.
    
- That NAT engine:
    
    - Assigns the VM a private IP (via DHCP)
        
    - Knows the VM’s current IP at all times
        
- So when you define:
    
    `Host: 8080 → Guest: 80`
    
    VirtualBox automatically forwards traffic to **that VM’s current IP**.
---
## Step 4 – Test from your host machine

On your **host browser**:

```
http://localhost:8080
```

✅ You should see the **nginx welcome page**  
served from **inside the VM**.

---

## Step 5 – Prove it’s really forwarding (optional)

Inside the VM, change the web page:

```bash
echo "Hello from the VM 🚀" | sudo tee /var/www/html/index.html
```

Refresh in host browser:

```
http://localhost:8080
```

You should now see:

```
Hello from the VM 🚀
```

---

## What Just Happened (Conceptually)

```
[ Your Host ]
    localhost:8080
          │
          ▼
   NAT Port Forwarding
          │
          ▼
[ Your VM ]
    port 80 (nginx)
```

- The VM is hidden behind NAT
    
- The NAT engine listens on `8080` on your host
    
- It forwards traffic to `VM:80`
    

---

## Extra Mini-Exercises (Highly Recommended)

### 1️⃣ Forward SSH instead of HTTP

Inside VM:

```bash
sudo apt install -y openssh-server
sudo systemctl start ssh
```

Port forward:

```
Host 2222 → Guest 22
```

Connect from host:

```bash
ssh user@localhost -p 2222
```