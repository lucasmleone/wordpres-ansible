# Desafío 6 - Instalación de WordPress con Ansible usando Roles

Este proyecto automatiza la instalación de WordPress en Ubuntu 22.04 utilizando Ansible y una estructura modular basada en roles. Cada rol se encarga de una parte específica del proceso de instalación y configuración, cumpliendo todos los requisitos del desafío 6.

## Arquitectura utilizada

- **Host de Ansible:** Máquina local creada con Multipass (Ubuntu).
- **Nodo gestionado:** Instancia EC2 en AWS con Ubuntu 22.04.
- **Conexión:** SSH entre el host y el nodo remoto.

## Estructura del proyecto

- `playbook.yml`: Playbook principal que llama a los roles.
- `roles/apache`: Instalación y configuración de Apache.
- `roles/php`: Instalación de PHP y extensiones necesarias.
- `roles/mariadb`: Instalación, aseguramiento y configuración de MariaDB.
- `roles/wordpress`: Instalación y configuración de WordPress y Apache para servir el sitio.


## Pasos automatizados

1. **Instalación y configuración de Apache**
2. **Instalación de PHP y extensiones**
3. **Instalación y aseguramiento de MariaDB**
4. **Creación de base de datos y usuario para WordPress**
5. **Descarga y configuración de WordPress**
6. **Configuración de Apache para WordPress**

## Uso

1. Edita tu archivo de inventario para definir los servidores (host local y nodo EC2).
   
   - El archivo `inventory.ini` debe contener la IP pública de tu instancia EC2 y los datos de acceso SSH.
   
   - Asegúrate de que el host de Ansible (Multipass) tenga acceso SSH al nodo EC2 y que el puerto 22 esté abierto en el grupo de seguridad de AWS.

2. Ejecuta el playbook principal:

   ```bash
   ansible-playbook -i inventory.ini site.yml
   ```

3. Al finalizar, abre tu navegador y accede a la IP pública de tu instancia EC2 para comprobar que WordPress está funcionando:

   ```
   http://<IP_PUBLICA_EC2>
   ```

## Ejemplo de resultados y estructura

### Estructura del proyecto

![Estructura de carpetas](./img/tree.png)

### Ejecución exitosa del playbook

![Play recap](./img/playbookok.png)

### AWS

![Instancia EC2](./img/ec2.png)
![Configuración de red](./img/aws%20tree.png)

### WordPress instalado y funcionando
![WordPress funcionando](./img/wordpress2.png)

![WordPress funcionando](./img/wordpress.png)

## Diagrama

![Diagrama](./img/diagrama6.png)