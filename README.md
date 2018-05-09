# SYNAPTIC-gocd

## Local con Docker (OSX)
  
En este modo se inicia el servidor y agentes GoCD usando docker. Esta estructura sirve para realizar pruebas de manera local

### Instalación

- Instalar Ansible [Link](http://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- Editar archivo ```roles/local/vars/main.yml```
 - ```gocd_version```: Verificar version de GoCD
 - ```gocd_server_host_http_port``` y ```gocd_server_host_https_port```: Cambiar puerto si fuese necesario
 - ```gocd_server_godata_path``` y ```gocd_agent_godata_path```: Seleccionar ruta local donde se almacenarán datos del servidor y de la gente. (Esto es para no perder los datos cuando se reinicie Docker)
- ```ansible-playbook -i "localhost" local.yml```

## Remoto (AWS)

En este modo se instala GoCD servidor y agentes en maquinas remotas (Ec2 AWS).

### Instalación

- Instalar Ansible en una maquina de la subnet. Esta actuará como Host
- Descargar repositorio
- Configurar archivo ```hosts```
  - Usar como referencia archivo ```hosts.template```
  - En ```server``` escribir IP interna del servidor que actua como server de GoCD
  - En ```agent``` escribir IP internta de los servidores que actuan como agentes
  - Guardar en ```/etc/ansible/hosts```
- Todas los servidores indicados en el archivo host deben tener permiso para que la maquina que actua como Host tenga acceso mediante SSH
- ```ansible-playbook non_local.yml```


## FAQ

<b>- Ya tengo el servidor y agentes configurados de antemano pero quiero agregar un nuevo Agente.</b>
Simplemente agrega la IP de la nueva maquina Agente a la lista de agentes en el archivo ```hosts``` y ejecuta la receta. La receta solo realizará cambios en aquellas maquina que no tengan GoCD instalado.
