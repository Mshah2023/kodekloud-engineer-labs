# Configure Group-Based Access Control

> **KodeKloud Engineer Task**  
> Configure a shared group across all application servers and ensure the required user is a member of that group.

---

## Objective

Perform the following tasks on **all App Servers** (`stapp01`, `stapp02`, and `stapp03`):

| Requirement | Value |
|------------|-------|
| Group Name | `nautilus_noc` |
| User | `rajesh` |
| Action | Create the user if it does not exist |
| Group Membership | Add `rajesh` to `nautilus_noc` |

---

## Server Details

| Server | Username | Purpose |
|---------|----------|---------|
| `stapp01` | `tony` | Nautilus App Server 1 |
| `stapp02` | `steve` | Nautilus App Server 2 |
| `stapp03` | `banner` | Nautilus App Server 3 |

---

## Implementation

Repeat the following steps on each App Server.

### 1. Connect to the Server

**App Server 1**

```bash
ssh tony@172.16.238.10
```

**App Server 2**

```bash
ssh steve@172.16.238.11
```

**App Server 3**

```bash
ssh banner@172.16.238.12
```

---

### 2. Switch to the Root User

```bash
sudo -i
```

---

### 3. Create the Group

```bash
groupadd nautilus_noc
```

---

### 4. Create the User (if it does not already exist)

```bash
id rajesh || useradd rajesh
```

---

### 5. Add the User to the Group

```bash
usermod -aG nautilus_noc rajesh
```

---

## Verification

### Verify the Group Exists

```bash
getent group nautilus_noc
```

Expected output:

```text
nautilus_noc:x:1002:rajesh
```

> *The GID may vary depending on the system.*

---

### Verify the User's Group Membership

```bash
id rajesh
```

Expected output:

```text
uid=1002(rajesh) gid=1002(rajesh) groups=1002(rajesh),1003(nautilus_noc)
```

> *UID and GID values may differ.*

---

## Command Summary

Run the following commands on **each App Server**:

```bash
sudo -i

groupadd nautilus_noc

id rajesh || useradd rajesh

usermod -aG nautilus_noc rajesh

id rajesh
```

---

## Result

The task is successfully completed with the following configuration:

- Group `nautilus_noc` created on all App Servers.
- User `rajesh` created where necessary.
- User `rajesh` added to the `nautilus_noc` group.
- Group membership verified on each server.

---

## Key Takeaway

Managing permissions through groups simplifies administration, improves scalability, and follows best practices for Linux access control by assigning permissions to groups instead of individual users.