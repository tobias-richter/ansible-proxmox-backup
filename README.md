# tobias_richter.proxmox_backup

[![Build Status](https://travis-ci.org/tobias-richter/ansible-proxmox-backup.svg?branch=master)](https://travis-ci.org/tobias-richter/ansible-proxmox-backup)

This role setups a backup for the proxmox configuration.
This role reuses the backup script `prox_config_backup.sh` from <https://github.com/DerDanilo/proxmox-stuff/> by 
wrapping it and providing configurable values for `BACK_DIR` and `TMP_DIR`.

## Requirements

This role requires Ansible 2.7 or higher.

## Role Variables

Available variables are listed below, along with their default values (see [defaults/main.yml](defaults/main.yml)):

    proxmox_backup_script_url: https://raw.githubusercontent.com/DerDanilo/proxmox-stuff/3660e828a2014738a2a2736ae850c6edbae55592/prox_config_backup.sh

URL to retrieve the backup script from.

    proxmox_backup_script_path: /usr/local/sbin/prox_config_backup.sh

Path of the backup script on the proxmox instance.

    proxmox_backup_wrapper_script_path: /usr/local/sbin/prox_config_backup_wrapper.sh

Path of the wrapper script that configures the real backup script.

    proxmox_backup_dir: /mnt/backups/proxmox

The destination directory for the backups.

    proxmox_backup_temp_dir: /var/tmp

Temp dir used during backup creation.

    proxmox_backup_log_dir: /var/log/pve-backup
    proxmox_backup_log_file: "{{ proxmox_backup_log_dir }}/pve-backup.log"

Path for the backup log files and path to the logfile.

    proxmox_backup_cron_configure: false

Enables/Disables the task for managing the cronjob.

    # proxmox_backup_cron_minute:
    # proxmox_backup_cron_hour:
    # proxmox_backup_cron_day:
    # proxmox_backup_cron_month:
    # proxmox_backup_cron_weekday:
    # proxmox_backup_cron_special_time:

Use the proxmox_backup_cron_.* vars to configure the execution times for the cronjob.

## Example Playbook

Configures the backup to be executed every friday at 21:30.

    - hosts: pve
	  roles:
	    - role: tobias_richter.proxmox_backup
	      proxmox_backup_cron_configure: true
	      proxmox_backup_cron_hour: 21
	      proxmox_backup_cron_minute: 30
	      proxmox_backup_cron_weekday: 5
	      
