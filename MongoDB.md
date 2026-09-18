Here is the updated version focused **only on MongoDB backup and restore**, with practical examples for local MongoDB, authentication, Atlas, specific databases/collections, compressed backups, and selective restores.

# 📦 MongoDB Backup & Restore – Complete Commands Guide

A practical reference for MongoDB **backup and restore** using `mongodump` and `mongorestore`.

---

# 🚀 1. `mongodump` — Backup MongoDB

`mongodump` creates a **BSON binary backup** of MongoDB data.

## 🔹 1.1 Backup a Single Database

```bash
mongodump --db=myDatabase --out=backup
```

Example:

```bash
mongodump --db=csfx --out=backup
```

Creates:

```text
backup/
└── csfx/
    ├── users.bson
    ├── users.metadata.json
    ├── orders.bson
    └── orders.metadata.json
```

---

## 🔹 1.2 Backup All Databases

```bash
mongodump --out=backup
```

Example:

```bash
mongodump --out=mongodb-backup
```

Structure:

```text
mongodb-backup/
├── admin/
├── config/
├── local/
├── csfx/
└── myDatabase/
```

---

## 🔹 1.3 Backup Using MongoDB URI

```bash
mongodump --uri="mongodb://localhost:27017/myDatabase" --out=backup
```

Example:

```bash
mongodump --uri="mongodb://localhost:27017/csfx" --out=backup
```

---

# 🔐 2. Backup MongoDB with Username & Password

## 🔹 2.1 Local MongoDB Authentication

```bash
mongodump \
  --uri="mongodb://username:password@localhost:27017/myDatabase" \
  --out=backup
```

Example:

```bash
mongodump \
  --uri="mongodb://admin:MyPassword@localhost:27017/csfx" \
  --out=backup
```

### If the user authenticates against `admin`

```bash
mongodump \
  --uri="mongodb://admin:MyPassword@localhost:27017/csfx?authSource=admin" \
  --out=backup
```

> If your password contains special characters such as `@`, `:`, `/`, or `#`, URL-encode the password.

---

# 🌐 3. MongoDB Atlas Backup

## 🔹 3.1 Backup Atlas Database

```bash
mongodump \
  --uri="mongodb+srv://username:password@cluster0.mongodb.net/myDatabase" \
  --out=backup
```

Example:

```bash
mongodump \
  --uri="mongodb+srv://admin:MyPassword@cluster0.xxxxx.mongodb.net/csfx" \
  --out=backup
```

---

## 🔹 3.2 Atlas Backup Without Specifying Database

```bash
mongodump \
  --uri="mongodb+srv://username:password@cluster0.mongodb.net/" \
  --out=backup
```

This can back up all databases that the authenticated user has permission to read.

---

# 📁 4. Backup Specific Collection

```bash
mongodump \
  --db=myDatabase \
  --collection=users \
  --out=backup
```

Example:

```bash
mongodump \
  --db=csfx \
  --collection=users \
  --out=backup
```

Result:

```text
backup/
└── csfx/
    ├── users.bson
    └── users.metadata.json
```

---

# 🗜️ 5. Create a Compressed Backup

Useful when your database is large.

```bash
mongodump \
  --db=myDatabase \
  --archive=backup.archive.gz \
  --gzip
```

Example:

```bash
mongodump \
  --db=csfx \
  --archive=csfx-backup.archive.gz \
  --gzip
```

Result:

```text
csfx-backup.archive.gz
```

This is convenient for transferring or storing backups.

---

# 📦 6. Backup All Databases into One Compressed File

```bash
mongodump \
  --archive=all-databases.archive.gz \
  --gzip
```

Example:

```bash
mongodump \
  --archive=mongodb-backup-2026-09-18.archive.gz \
  --gzip
```

---

# 📅 7. Create Date-Based Backup Folder

### Linux/macOS

```bash
mongodump \
  --db=csfx \
  --out="backup/$(date +%Y-%m-%d)"
```

Example:

```text
backup/
└── 2026-09-18/
    └── csfx/
        ├── users.bson
        └── orders.bson
```

### Windows CMD

```cmd
mongodump --db=csfx --out=backup\2026-09-18
```

### PowerShell

```powershell
mongodump --db=csfx --out="backup\$(Get-Date -Format yyyy-MM-dd)"
```

---

# 🔄 8. `mongorestore` — Restore MongoDB

`mongorestore` restores BSON backups created by `mongodump`.

---

## 🔹 8.1 Restore a Database

If your backup is:

```text
backup/
└── csfx/
    ├── users.bson
    └── orders.bson
```

Run:

```bash
mongorestore --db=csfx backup/csfx
```

---

# 🔹 8.2 Restore to a Different Database Name

For example, restore `csfx` backup into `csfx_test`:

```bash
mongorestore \
  --db=csfx_test \
  backup/csfx
```

This is useful for creating a testing copy.

---

# 🔹 8.3 Restore All Databases

If backup was created using:

```bash
mongodump --out=backup
```

Restore using:

```bash
mongorestore backup
```

Example:

```bash
mongorestore mongodb-backup
```

---

# ⚠️ 9. Drop Existing Database Data Before Restore

To remove existing collections before restoring:

```bash
mongorestore \
  --drop \
  --db=csfx \
  backup/csfx
```

Example:

```bash
mongorestore --drop --db=csfx backup/csfx
```

### What happens?

If the database contains:

```text
users
orders
transactions
```

and your backup contains the same collections, `--drop` removes the existing collections before restoring them.

> ⚠️ Use `--drop` carefully in production.

---

# 🔐 10. Restore with Authentication

## 🔹 Local MongoDB

```bash
mongorestore \
  --uri="mongodb://admin:MyPassword@localhost:27017/csfx?authSource=admin" \
  backup/csfx
```

---

## 🔹 Restore with `--drop`

```bash
mongorestore \
  --uri="mongodb://admin:MyPassword@localhost:27017/csfx?authSource=admin" \
  --drop \
  backup/csfx
```

---

# 🌐 11. Restore to MongoDB Atlas

```bash
mongorestore \
  --uri="mongodb+srv://username:password@cluster0.mongodb.net/csfx" \
  backup/csfx
```

Example:

```bash
mongorestore \
  --uri="mongodb+srv://admin:MyPassword@cluster0.xxxxx.mongodb.net/csfx" \
  backup/csfx
```

---

# 🗜️ 12. Restore Compressed Backup

For a backup created with:

```bash
mongodump \
  --db=csfx \
  --archive=csfx-backup.archive.gz \
  --gzip
```

Restore:

```bash
mongorestore \
  --gzip \
  --archive=csfx-backup.archive.gz
```

---

# 🗜️ 13. Restore Compressed Backup to Specific Database

```bash
mongorestore \
  --gzip \
  --archive=csfx-backup.archive.gz \
  --nsFrom="csfx.*" \
  --nsTo="csfx_test.*"
```

This restores:

```text
csfx.users
csfx.orders
```

into:

```text
csfx_test.users
csfx_test.orders
```

---

# 📌 14. Restore a Specific Collection

If backup contains:

```text
backup/
└── csfx/
    ├── users.bson
    ├── orders.bson
    └── transactions.bson
```

Restore only `users`:

```bash
mongorestore \
  --db=csfx \
  --collection=users \
  backup/csfx/users.bson
```

---

# 🔄 15. Restore Collection to Another Database

```bash
mongorestore \
  --db=csfx_test \
  --collection=users \
  backup/csfx/users.bson
```

This copies:

```text
csfx.users
```

to:

```text
csfx_test.users
```

---

# 🔥 16. Complete Production Backup Example

For an authenticated production database:

```bash
mongodump \
  --uri="mongodb+srv://admin:password@cluster.mongodb.net/csfx" \
  --archive="csfx-2026-09-18.archive.gz" \
  --gzip
```

Result:

```text
csfx-2026-09-18.archive.gz
```

---

# 🔥 17. Complete Production Restore Example

```bash
mongorestore \
  --uri="mongodb+srv://admin:password@cluster.mongodb.net/csfx" \
  --gzip \
  --archive="csfx-2026-09-18.archive.gz"
```

---

# ⚠️ 18. Production Restore with `--drop`

```bash
mongorestore \
  --uri="mongodb+srv://admin:password@cluster.mongodb.net/csfx" \
  --drop \
  --gzip \
  --archive="csfx-2026-09-18.archive.gz"
```

Use this when you intentionally want the restored database to replace existing collections.

---

# 🛠️ 19. Useful `mongodump` Options

| Option                     | Purpose                | Example                          |
| -------------------------- | ---------------------- | -------------------------------- |
| `--db`                     | Select database        | `--db=csfx`                      |
| `--collection`             | Select collection      | `--collection=users`             |
| `--out`                    | Backup directory       | `--out=backup`                   |
| `--uri`                    | MongoDB connection URI | `--uri="mongodb://..."`          |
| `--archive`                | Create single archive  | `--archive=backup.gz`            |
| `--gzip`                   | Compress backup        | `--gzip`                         |
| `--authenticationDatabase` | Authentication DB      | `--authenticationDatabase=admin` |

---

# 🛠️ 20. Useful `mongorestore` Options

| Option         | Purpose                         | Example                 |
| -------------- | ------------------------------- | ----------------------- |
| `--db`         | Target database                 | `--db=csfx`             |
| `--collection` | Target collection               | `--collection=users`    |
| `--uri`        | MongoDB connection URI          | `--uri="mongodb://..."` |
| `--drop`       | Drop collections before restore | `--drop`                |
| `--archive`    | Restore archive                 | `--archive=backup.gz`   |
| `--gzip`       | Read compressed backup          | `--gzip`                |
| `--nsFrom`     | Source namespace                | `--nsFrom="csfx.*"`     |
| `--nsTo`       | Target namespace                | `--nsTo="csfx_test.*"`  |

---

# 📂 21. Normal Backup Structure

```text
backup/
└── csfx/
    ├── users.bson
    ├── users.metadata.json
    ├── orders.bson
    ├── orders.metadata.json
    ├── transactions.bson
    └── transactions.metadata.json
```

---

# 🗜️ 22. Archive Backup Structure

With:

```bash
mongodump --db=csfx --archive=csfx-backup.gz --gzip
```

you get:

```text
csfx-backup.gz
```

instead of multiple `.bson` files.

---

# 🚀 Quick Reference

### Backup database

```bash
mongodump --db=csfx --out=backup
```

### Backup all databases

```bash
mongodump --out=backup
```

### Backup collection

```bash
mongodump --db=csfx --collection=users --out=backup
```

### Compressed backup

```bash
mongodump --db=csfx --archive=csfx.gz --gzip
```

### Restore database

```bash
mongorestore --db=csfx backup/csfx
```

### Restore all databases

```bash
mongorestore backup
```

### Restore with drop

```bash
mongorestore --drop --db=csfx backup/csfx
```

### Restore compressed backup

```bash
mongorestore --gzip --archive=csfx.gz
```

### Backup Atlas

```bash
mongodump --uri="mongodb+srv://username:password@cluster.mongodb.net/csfx" --out=backup
```

### Restore Atlas

```bash
mongorestore --uri="mongodb+srv://username:password@cluster.mongodb.net/csfx" backup/csfx
```

### Backup → Restore test database

```bash
mongodump --db=csfx --out=backup
```

```bash
mongorestore --db=csfx_test backup/csfx
```

This last pattern is particularly useful for **testing a production backup without touching the production database**.
