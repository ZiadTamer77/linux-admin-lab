# Day 1 - Linux User, Permissions & DNS Fundamentals

## Objective

Understand how Linux manages users, groups, file permissions, and how DNS resolution works within a real server environment.

---

## Scenario (Real-World Context)

Simulated a multi-user environment similar to a shared cloud storage system (e.g., Nextcloud), where:

* Different users require different levels of access
* Sensitive data must be restricted
* Shared collaboration must be controlled

---

## Tasks Performed

### 1. Created Users

* devuser → represents a developer
* opsuser → represents operations user

```bash
sudo adduser devuser
sudo adduser opsuser
```

---

### 2. Created Groups

* developers → for development access
* operations → for operational access

```bash
sudo groupadd developers
sudo groupadd operations
```

---

### 3. Assigned Users to Groups

```bash
sudo usermod -aG developers devuser
sudo usermod -aG operations opsuser
```

---

### 4. Created Shared Directory

```bash
sudo mkdir -p /opt/project-data
```

---

### 5. Set Ownership

```bash
sudo chown devuser:developers /opt/project-data
```

👉 Ensures only the developer group owns the directory

---

### 6. Set Permissions

```bash
sudo chmod 770 /opt/project-data
```

👉 Meaning:

* Owner → full access (read, write, execute)
* Group → full access
* Others → no access

---

## Testing & Validation

### Test 1 — Authorized Access

```bash
su - devuser
touch /opt/project-data/test.txt
```

✅ Success → correct permissions

---

### Test 2 — Unauthorized Access

```bash
su - opsuser
touch /opt/project-data/test.txt
```

❌ Permission Denied → expected behavior

---

## Permission Deep Dive

* `r` → read (list files)
* `w` → write (create/delete files)
* `x` → execute (enter directory)

⚠️ Important:
Without `x`, a user cannot access a directory even if read is enabled.

---

## DNS Investigation (Real System)

### Checked Resolver Configuration

```bash
cat /etc/resolv.conf
```

Observed:

* Primary DNS → Pi-hole (192.168.100.12)
* Secondary DNS → Tailscale

---

### Tested DNS Resolution

```bash
dig google.com
```

Observed:

* Query handled by Pi-hole
* Returned valid public IP

---

### DNS Flow (Actual System)

1. User enters domain (google.com)
2. Local system checks cache (systemd-resolved)
3. Query sent to Pi-hole (local DNS resolver)
4. Pi-hole checks cache / filtering rules
5. If not found → forwards to upstream DNS
6. Upstream performs recursive resolution
7. IP returned back to system

---

## System Inspection

### Active Ports & Services

```bash
sudo ss -tulnp
```

Used to identify:

* Services running on ports (80, 443, 53)
* Which processes are listening

---

### Network Interfaces

```bash
ip a
```

* Identified LAN interface (192.168.x.x)
* Observed Docker and Tailscale interfaces

---

### Routing Table

```bash
ip route
```

* Identified default gateway
* Understood traffic path

---

## Issues Faced

### 1. Permission Denied (chmod 000)

```bash
chmod 000 /opt/project-data
```

* Completely blocked access
* Fixed by restoring permissions

```bash
chmod 770 /opt/project-data
```

---

### 2. DNS Multiple Servers Warning

* Multiple DNS entries configured
* Some entries may be ignored
* Potential inconsistency in resolution path

---

## Key Learnings

* Linux access control is based on **user, group, others**
* Directory permissions require **execute (x)** to enter
* DNS resolution involves multiple layers (local → resolver → upstream)
* System inspection tools (`ss`, `ip`, `dig`) are essential for troubleshooting
* Real systems often have multiple services (Docker, VPN, DNS)

---

## Commands Summary

* User management: `adduser`, `usermod`
* Group management: `groupadd`
* Permissions: `chmod`, `chown`
* Networking: `ip`, `ss`, `dig`
* System inspection: `ls -l`, `ip route`

---

## Outcome

Built a controlled multi-user environment with enforced access restrictions and validated DNS resolution flow within a real server setup.



