
# Ansible Security Project 🔐

Este proyecto automatiza el despliegue de una infraestructura de red segura usando Ansible y VMware ESXi. Incluye firewalls, servidores en VLANs, y un honeypot Cowrie listo para pruebas de ciberseguridad.

## 🧩 Componentes del Proyecto

- **pfSense**: 2 firewalls para segmentación de red (LAN y DMZ)
- **Servidor DNS**: ubicado en VLAN 10
- **Servidor Web**: ubicado en VLAN 20
- **Servidor Honeypot Cowrie**: ubicado en la DMZ (VLAN 30)
- **Seeds Cloud-init**: Instalación desatendida de Ubuntu para cada VM

## 🗂 Estructura del Proyecto

```
ansible_security_project/
├── inventory.yml               # Inventario Ansible con IPs de las VMs
├── vars.yml                   # Variables globales de infraestructura
├── deploy_all.yml            # Playbook maestro que ejecuta todos los demás
├── playbook_fw1.yml          # Crea Firewall 1
├── playbook_fw2.yml          # Crea Firewall 2
├── playbook_dns.yml          # Crea servidor DNS
├── playbook_web.yml          # Crea servidor Web
├── playbook_cowrie.yml       # Crea Honeypot Cowrie
└── seeds/                    # Seeds ISO para instalación desatendida
    ├── seed_dns.iso
    ├── seed_web.iso
    └── seed_cowrie.iso
```

## 🚀 Requisitos

- VMware ESXi o vCenter accesible
- Red con acceso a las VLAN configuradas
- Máquina de administración con:
  - Python 3.x
  - Ansible (`ansible-core`, `community.vmware`)
  - `pip install -r requirements.txt`
  - `sshpass`, si se usa autenticación con password
- Imágenes ISO de Ubuntu y pfSense cargadas en el datastore de ESXi
- Seeds `.iso` generados con `genisoimage`

## 🛠 Uso

1. Clona el repositorio:

```bash
git clone https://github.com/anllacarpro/ansible_security_project.git
cd ansible_security_project
```

2. Edita las variables en `vars.yml` y los datos de acceso en `inventory.yml`.

3. Asegúrate de tener los ISOs (`.iso` y seeds) cargados en tu `datastore`.

4. Ejecuta el despliegue completo:

```bash
ansible-playbook -i inventory.yml deploy_all.yml
```

## 🧪 Verificación

- Puedes verificar el honeypot accediendo por SSH al puerto 2222 de la IP configurada para Cowrie.
- Accede a pfSense por navegador: `https://<ip_fw1>` y `https://<ip_fw2>`.
- Asegúrate de que las VMs respondan ping y tengan sus servicios levantados (`DNS`, `Web`, etc).

## 🛡 Propósito Académico

Este proyecto fue diseñado para simular un entorno seguro de red, incluyendo elementos reales como honeypots y segmentación por VLAN. Ideal para prácticas de ciberseguridad y automatización.

---

© 2025 - Desarrollado por [anllacarpro](https://github.com/anllacarpro)
