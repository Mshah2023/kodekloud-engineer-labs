````markdown
# Create a User with a Non-Interactive Shell

> **KodeKloud Engineer Task**  
> Create a system user with a non-interactive shell to support the backup agent's security requirements.

---

## Objective

Create the following user on **App Server 3 (`stapp03`)**:

| Requirement | Value |
|------------|-------|
| Username | `siva` |
| Shell | `/sbin/nologin` *(or `/usr/sbin/nologin` depending on the distribution)* |
| Target Server | `stapp03` |

---

## Server Details

| Server | Username | Purpose |
|---------|----------|---------|
| `stapp03` | `banner` | Nautilus App Server 3 |

---

## Implementation

### 1. Connect to App Server 3

```bash
ssh banner@stapp03
```

> **Note:** In the KodeKloud environment, you can use the hostname (`stapp03`) instead of the IP address.

---

### 2. Switch to the Root User

```bash
sudo -i
```

---

### 3. Create the User with a Non-Interactive Shell

```bash
useradd -s /sbin/nologin siva
```

> If `/sbin/nologin` is unavailable on your system, use:

```bash
useradd -s /usr/sbin/nologin siva
```

---

## Verification

### Verify the User Exists

```bash
id siva
```

Example output:

```text
uid=1002(siva) gid=1002(siva) groups=1002(siva)
```

> UID and GID values may vary.

---

### Verify the Assigned Shell

```bash
grep '^siva:' /etc/passwd
```

Expected output:

```text
siva:x:1002:1002::/home/siva:/sbin/nologin
```

---

## Command Summary

```bash
ssh banner@stapp03

sudo -i

useradd -s /sbin/nologin siva

id siva

grep '^siva:' /etc/passwd
```

---

## Result

The task is successfully completed with the following configuration:

- User `siva` created on **App Server 3**.
- Assigned a **non-interactive shell** (`/sbin/nologin`).
- User account verified successfully.

---

## Key Takeaway

Assigning a non-interactive shell to service accounts prevents direct logins while still allowing the account to own files or run specific services. This is a common security practice that reduces the attack surface by ensuring system or application users cannot be used for interactive sessions.
````
