# Ansible Update Repo for Ansible Semaphore

Dieses Repository enthält ein minimales, produktionsnahes Setup, um OS-Updates
(apt/yum/dnf) via **Ansible Semaphore** zu starten, zu überwachen und zu planen.

## Struktur
```
playbooks/
  update-all.yml
group_vars/
  all.yml
inventories/
  prod.ini
  staging.ini
ansible.cfg
```

## Schnellstart
1. **Inventories** anpassen (`inventories/prod.ini` / `staging.ini`).
2. **group_vars/all.yml** anpassen (z. B. `do_reboot`, Paket-Optionen).
3. Repo zu GitHub pushen.
4. In **Semaphore**:
   - *Project → Repositories → Add* (dieses Repo verknüpfen)
   - *Inventories → Add* (entweder Inhalt aus `inventories/*.ini` einfügen oder das Repo-File referenzieren)
   - *Task Templates → New → Ansible Playbook*
     - Repository: dieses Repo
     - Playbook: `playbooks/update-all.yml`
     - Inventory: z. B. `prod.ini`
     - Extra Vars (optional): `{"do_reboot": true}`
   - Run → Logs live beobachten.

## Variables / Extra Vars
- `do_reboot` (bool): Ob nach Updates automatisch neu gestartet wird.
- `update_mode` (string): `dist` (Ubuntu/Debian) oder `safe` (nur security/empfohlene Updates, falls paketmanagerseitig unterstützt).
- `distro_lock_kernel` (bool): Kernel von Updates ausschließen (Debian/Ubuntu über APT Markierung).

## Sicherheit
- SSH-Keys in Semaphore **Key Store** hinterlegen.
- Optional: Vault für sensible Variablen nutzen.