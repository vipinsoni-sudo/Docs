# 📦 MongoDB Database Tools – Commands Guide

A quick reference guide for commonly used MongoDB Database Tools like `mongodump`, `mongorestore`, `mongoexport`, and `mongoimport`.

---

## 🚀 1. mongodump (Backup Database)

Creates a binary backup of your database.

### 🔹 Backup a single database

```bash
mongodump --db=yourDatabaseName --out=backupFolder
```

### 🔹 Backup all databases

```bash
mongodump --out=backupFolder
```

### 🔹 Backup using connection URI

```bash
mongodump --uri="mongodb://localhost:27017" --out=backupFolder
```

### 🔹 Backup specific collection

```bash
mongodump --db=yourDatabaseName --collection=yourCollection --out=backupFolder
```

---

## 🔄 2. mongorestore (Restore Backup)

Restores data from a backup.

### 🔹 Restore a database

```bash
mongorestore --db=yourDatabaseName backupFolder/yourDatabaseName
```

### 🔹 Restore all databases

```bash
mongorestore backupFolder
```

### 🔹 Drop existing data before restore

```bash
mongorestore --drop --db=yourDatabaseName backupFolder/yourDatabaseName
```

---

## 📤 3. mongoexport (Export to JSON/CSV)

Exports collection data to readable formats.

### 🔹 Export to JSON

```bash
mongoexport --db=yourDatabaseName --collection=yourCollection --out=data.json
```

### 🔹 Export to CSV

```bash
mongoexport --db=yourDatabaseName --collection=yourCollection --type=csv --fields=name,age --out=data.csv
```

### 🔹 Export with query filter

```bash
mongoexport --db=yourDatabaseName --collection=yourCollection --query='{"status":"active"}' --out=data.json
```

---

## 📥 4. mongoimport (Import JSON/CSV)

Imports data into MongoDB.

### 🔹 Import JSON

```bash
mongoimport --db=yourDatabaseName --collection=yourCollection --file=data.json
```

### 🔹 Import CSV

```bash
mongoimport --db=yourDatabaseName --collection=yourCollection --type=csv --headerline --file=data.csv
```

### 🔹 Drop collection before import

```bash
mongoimport --db=yourDatabaseName --collection=yourCollection --drop --file=data.json
```

---

## 🔐 5. Authentication Example

Use username & password if authentication is enabled:

```bash
mongodump --uri="mongodb://username:password@localhost:27017/yourDatabaseName"
```

---

## 🌐 6. MongoDB Atlas Example

```bash
mongodump --uri="mongodb+srv://username:password@cluster0.mongodb.net/yourDatabaseName"
```

---

## ⚙️ 7. Useful Options

| Option         | Description                              |
| -------------- | ---------------------------------------- |
| `--db`         | Specify database                         |
| `--collection` | Specify collection                       |
| `--out`        | Output directory                         |
| `--drop`       | Drop existing data before restore/import |
| `--uri`        | Connection string                        |
| `--query`      | Filter data                              |

---

## 📁 Example Backup Structure

```
backup/
 └── yourDatabaseName/
     ├── collection1.bson
     ├── collection2.bson
     └── metadata.json
```

---

## 💡 Tips

* Use **mongodump** for full backups (recommended)
* Use **mongoexport** for readable data (JSON/CSV)
* Always test restore using **mongorestore**
* Store backups in a safe location (cloud or external drive)

---

## ✅ Quick Summary

| Tool         | Purpose         |
| ------------ | --------------- |
| mongodump    | Backup database |
| mongorestore | Restore backup  |
| mongoexport  | Export JSON/CSV |
| mongoimport  | Import JSON/CSV |

---

## 🧑‍💻 Author

Prepared for quick developer reference 🚀
