# ansible_dcos_special

**Comandos probados**
```bash
ansible-playbook plays/uninstall.yml
ansible-playbook plays/install.yml
```
### Ficheros
**./ansible-dcos/hosts.yaml**
Fichero de configuración del ansible dc/os

**./ansible-docs/roles/bootstrap/templates/config.yaml.j2**
Fichero de configuracion del dc/os para la generación de nodos.
Complementa la informacion del **hosts.yaml**

### Pasos
###En todos los nodos
- DNS y NTP activos y sincronizados. (sol. en entornos aislados dnsmasq y chrony)
```bash
 yum install epel-release -y
```
###En el nodo bootstrap
```bash
yum install python-pip2 -y
pip install --upgrade pip
```
###En el nodo bootstrap.
Descargamos **dcos_generate_config** y lo copiamos en la raiz del bootstrap.
En el original, no conseguia realizar la descarga, se realiza una primera vez
un playbook install, se copia el fichero /var/lib/dcos_bootstrap, y se ejecuta una segunda vez el playbook install
[pinchar aqui](curl -O https://downloads.dcos.io/dcos/stable/dcos_generate_config.sh)

a.- desinstalamos con ansible-playbook plays/uninstall.sh

#Troubleshooting

Todos los nodos con el **ntp activado** 
```bash
 timedatectl
 sytemctl restart chronyd
```
**La configuración del proxy no la coge del sistema, se agrega en el fichero config.yaml anterior**

