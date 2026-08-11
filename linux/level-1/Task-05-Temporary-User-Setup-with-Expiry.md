# Create a Temporary User with an Expiry Date

> **KodeKloud Engineer Task**  
> Create a temporary user account on App Server 1 with an expiration date to provide controlled access for a developer working on the Nautilus project.

---

## Objective

Create the following user on **App Server 1 (`stapp01`)**:

| Requirement | Value |
|------------|-------|
| Username | `kareem` |
| Username Format | Lowercase |
| Account Expiry | `2027-02-17` |
| Target Server | `stapp01` |

---

## Task Explanation

The `kareem` account is required for a temporary assignment to the **Nautilus** project.

Instead of creating a permanent account, the user must have an expiration date. Once the account reaches the specified expiry date, the account will no longer be considered valid for login.

Linux provides the `useradd` command with the `-e` option to configure an account expiration date.

---

## Server Details

| Server | Username | Purpose |
|---------|----------|---------|
| `stapp01` | `tony` | Nautilus App Server 1 |

---

## Implementation

### 1. Connect to App Server 1

From the jump host, connect to `stapp01`:

```bash
ssh tony@stapp01
```

Alternatively, use the server IP:

```bash
ssh tony@172.16.238.10
```

> **Note:** The hostname or IP can be used depending on the environment.

---

### 2. Switch to the Root User

```bash
sudo -i
```

The `sudo -i` command starts a root login shell, providing the administrative privileges required to create users.

---

### 3. Create the User with an Expiry Date

```bash
useradd -e 2027-02-17 kareem
```

### Command Breakdown

| Command / Option | Description |
|------------------|-------------|
| `useradd` | Creates a new Linux user |
| `-e` | Sets the account expiration date |
| `2027-02-17` | Expiration date in `YYYY-MM-DD` format |
| `kareem` | Username being created |

The username is lowercase as required.

---

## Verification

### Verify the User Exists

Run:

```bash
id kareem
```

Example output:

```text
uid=1002(kareem) gid=1002(kareem) groups=1002(kareem)
```

> UID and GID values may vary depending on the system.

---

### Verify the Account Expiry Date

Run:

```bash
chage -l kareem
```

Look for:

```text
Account expires                                    : Feb 17, 2027
```

This confirms that the account has been configured with the required expiration date.

---

## Command Summary

```bash
ssh tony@stapp01

sudo -i

useradd -e 2027-02-17 kareem

id kareem

chage -l kareem
```

---

## Result

The task is successfully completed with the following configuration:

- User `kareem` created on **App Server 1**.
- Username is lowercase as required.
- Account expiration date set to **February 17, 2027**.
- User account and expiry configuration verified successfully.

---

## Key Takeaway

Temporary accounts are useful when users need access for a limited period.

The `useradd -e` option allows administrators to define an account expiration date during user creation:

```bash
useradd -e YYYY-MM-DD username
```

The `chage -l` command can then be used to inspect the account's password-aging and expiration settings.

This approach helps administrators maintain controlled access and reduces the risk of unused temporary accounts remaining active indefinitely.