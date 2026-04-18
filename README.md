# Day 1 - Linux User & Permission Management

## Objective
Understand how Linux manages users, groups, and file permissions.

---

## Tasks Performed

### 1. Created Users
- devuser
- opsuser

Command used:
sudo adduser devuser


---

### 2. Created Groups
- developers
- operations

command used:
sudo groupadd developers
---

### 3. Assigned Users to Groups
- devuser → developers
- opsuser → operations

command used:
sudo usermod -aG developers devops
---

### 4. Created Shared Directory
Path:
/opt/project-data


---

### 5. Set Ownership

chown devuser:developers /opt/project-data


---

### 6. Set Permissions
chmod 770 /opt/project-data


---
## System Inspection

### List users
cut -d: -f1 /etc/passwd

### List groups
cut -d: -f1 /etc/group

### Check user groups
id devuser

### Check group members
getent group developers
----

## Testing

- devuser → SUCCESS creating files
- opsuser → PERMISSION DENIED

---

## Issues Faced

- Permission denied after chmod 000
- Fixed by restoring correct permissions

---

## Key Learnings

- Difference between owner, group, others
- Importance of correct permissions
- How to debug access issues

---

## Commands Summary

- adduser
- groupadd
- usermod
- chmod
- chown
- ls -l
