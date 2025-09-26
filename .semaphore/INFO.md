# Hinweise für Ansible Semaphore
- Task Template → Type: "Ansible Playbook"
- Repository: dieses Repo
- Playbook: `playbooks/update-all.yml`
- Inventory: `inventories/prod.ini` (oder `staging.ini`)
- Extra Vars Beispiel:
```
{"do_reboot": true, "update_mode": "dist"}
```