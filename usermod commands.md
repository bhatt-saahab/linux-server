

### 📘 Basic Help

- `usermod --help`
    
    → Shows help info for usermod.
    

---

### 📝 Update User Info

- `usermod -c "HR user" u19`
    
    → Change **comment (GECOS)** field.
    
- `usermod -s /bin/sh u19`
    
    → Set **login shell** to `/bin/sh`.
    
- `usermod -s /sbin/nologin u19`
    
    → **Disable login** by setting shell to `nologin`.
    

---

### 🔐 Password Management

- `openssl passwd 123`
    
    → Generate **DES encrypted password**.
    
- `usermod -p <DES hash> u19`
    
    → Set password of `u19` using DES hash.
    
- `usermod -p <SHA-512 hash> u15`
    
    → Set password of `u15` using SHA-512 hash.
    

---

### 🔒 Lock/Unlock Accounts

- `usermod -L u19`
    
    → **Lock** user account (disable login).
    
- `usermod -U u19`
    
    → **Unlock** user account.
    

---

### 📅 Expiry & Inactivity

- `usermod -e 2020-12-30 u18`
    
    → Set **account expiry date**.
    
- `usermod -f 8 u18`
    
    → Set **inactivity** period (days after expiry before disable).
    

---

### 👤 UID and Home Directory

- `usermod -u 1030 u19`
    
    → Change **UID** to `1030`.
    
- `usermod -o -u 0 u19`
    
    → Set UID to `0` (root), allowing duplicate UID.
    
- `usermod -d /data/u19 u19`
    
    → Change **home dir** (does **not move** files).
    
- `usermod -m -d /opt/u19 u19`
    
    → Change home dir **and move** existing files.
    

---

### 👥 Group Management

### Primary Group

- `usermod -g 1027 u19`
    
    → Change **primary group** (by GID).
    
- `usermod -g armour it1`
    
    → Set primary group to `armour`.
    

### Supplementary Groups (Replace)

- `usermod -G admin,admin1 u18`
    
    → Replace all supplementary groups.
    
- `usermod -G u1,u2,EMP it1`
    
    → Replace all groups for `it1`.
    

### Supplementary Groups (Append)

- `usermod -aG u17 u18`
    
    → Append `u17` to `u18`'s group list.
    
- `usermod -aG u1,u2,EMP it1`
    
    → Append multiple groups to `it1`.
    

---

### 🔑 Password Change

- `passwd`
    
    → Change **current user's** password.
    
- `passwd u19`
    
    → Change password for **user `u19`** interactively.
    

---

Let me know if you'd like **groupadd**, **groupmod**, or **account deletion** commands added to this cheat sheet!
