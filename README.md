# CP-421-ASSIGNMENT1
 A PROJECTFOR STUDENT AND SUBJECT API
 THERE SHOULD BE A HOST XAMPP APPLICATION AND VS CODE/PHP ENVIRONMENT
 # CP 421 ASSINGMENT 2
 ## 🔧 Bash Scripts for Server Automation

This directory contains three Bash scripts to automate server management tasks for the deployed API on an AWS Ubuntu EC2 instance. These scripts ensure regular health checks, backups, and updates, helping maintain system reliability and performance.

---

### 📜 Scripts Overview

#### 1. `health_check.sh`
- **Purpose:** Monitors CPU, memory, disk space, web server status, and API endpoints (`/student.php` and `/subject.php`).
- **Logs to:** `/var/log/server_health.log`
- **Warnings:** If CPU/memory/disk thresholds are exceeded or endpoints fail, it logs a warning.

#### 2. `backup_api.sh`
- **Purpose:** Creates daily backups of API project files and MySQL database.
- **Backups saved to:** `/home/ubuntu/backups/`
- **Logs to:** `/home/ubuntu/backup.log`
- **Old backups:** Automatically deletes backups older than 7 days.

#### 3. `update_server.sh`
- **Purpose:** Updates system packages, pulls the latest code from GitHub, and restarts the web server.
- **Logs to:** `/home/ubuntu/update.log`
- **Error handling:** If `git pull` fails, the script exits early and logs the error.

---

### ⚙️ Setup Instructions

1. **Upload scripts to your EC2 instance (e.g., using scp or Git).**
2. **Make all scripts executable:**
   ```bash
   chmod +x health_check.sh backup_api.sh update_server.sh
## Backup Schemes

There are several backup schemes to consider when creating automated backups for your API and server environment. Below are three common schemes, each with their own advantages and disadvantages:

### 1. Full Backup
- **Description:** A complete backup of all data, files, and configurations.
- **Execution:** Uses commands like `tar` or `rsync` to back up everything in the system or database.
  ```bash
  tar -czf /backup/full_backup.tar.gz /path/to/important_data
Advantages:

    Simple to implement and restore.

    No dependency on other backups.

Disadvantages:

    Resource-intensive.

    Requires significant storage space.

   Slower to perform and restore.
   2. Incremental Backup

    Description: Backs up only the data that has changed since the last backup (full or incremental).

    Execution: Uses tools like rsync to back up only modified files.

    rsync -av --link-dest=/backup/previous_full_backup /path/to/important_data /backup/incremental_backup/

    Advantages:

        Efficient in terms of storage and backup time.

        Only backs up changed files.

    Disadvantages:

        Restoration is complex and requires all previous backups.

        Risk of data loss if any incremental backup is missing or corrupted.

3. Differential Backup

    Description: Backs up all data that has changed since the last full backup.

    Execution: Similar to incremental, but it only relies on the last full backup.

    rsync -av --compare-dest=/backup/full_backup /path/to/important_data /backup/differential_backup/

    Advantages:

        Simpler restoration than incremental backups.

        Uses less storage than full backups.

    Disadvantages:

        Larger storage requirements over time compared to incremental backups.

        Slower backup times as the differential grows in size.


