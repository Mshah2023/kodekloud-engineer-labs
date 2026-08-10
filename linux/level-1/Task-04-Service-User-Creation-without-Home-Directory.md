# Create a Service User Without a Home Directory

> **KodeKloud Engineer Task**  
> Create a service user account on the designated application server without creating a home directory.

---

## Objective

Create the following user on **App Server 2 (`stapp02`)**:

| Requirement | Value |
|------------|-------|
| Username | `mark` |
| Home Directory | None |
| Target Server | `stapp02` |

---

## Server Details

| Server | Username | Purpose |
|---------|----------|---------|
| `stapp02` | `steve` | Nautilus App Server 2 |

---

## Implementation

### 1. Connect to App Server 2

```bash
ssh steve@stapp02
```

> **Note:** In the KodeKloud environment, you can use the hostname (`stapp02`) instead of the IP address.

---

### 2. Switch to the Root User

```bash
sudo -i
```

---

### 3. Create the User Without a Home Directory

Use the `-M` option with `useradd`:

```bash
useradd -M mark
```

### Command Breakdown

| Option | Description |
|--------|-------------|
| `-M` | Do not create the user's home directory |
| `mark` | Username to create |

---

## Verification

### Verify the User Exists

```bash
id mark
```

Example output:

```text
uid=1002(mark) gid=1002(mark) groups=1002(mark)
```

> UID and GID values may vary depending on the system.

---

### Verify the Home Directory

Check the user's entry in `/etc/passwd`:

```bash
grep '^mark:' /etc/passwd
```

Example output:

```text
mark:x:1002:1002::/home/mark:/bin/bash
```

The `/home/mark` path may appear in `/etc/passwd`, but the directory itself should **not exist** because the `-M` option prevents its creation.

Verify with:

```bash
ls -ld /home/mark
```

Expected result:

```text
ls: cannot access '/home/mark': No such file or directory
```

---

## Command Summary

```bash
ssh steve@stapp02

sudo -i

useradd -M mark

id mark

grep '^mark:' /etc/passwd

ls -ld /home/mark
```

---

## Result

The task is successfully completed with the following configuration:

- User `mark` created on **App Server 2**.
- No home directory created for the user.
- User account verified successfully.
- The `-M` option was used to prevent automatic home directory creation.

---

## Key Takeaway

The `useradd -M` option is useful when creating service or application accounts that do not require a personal home directory.

Avoiding unnecessary home directories helps keep the system organized and follows the principle of assigning only the resources required by an account.