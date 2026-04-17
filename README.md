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
sudo usermod -aG devops developers
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
