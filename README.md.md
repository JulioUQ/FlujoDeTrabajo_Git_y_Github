

  ![[Git-y-Github.png|300]]
# Directrices de Github y Git para trabajar con repositorios remotos

<p align="justify">GitHub es una plataforma ampliamente utilizada para colaborar en proyectos de desarrollo de software a nivel global. Trabajar con repositorios remotos en GitHub es fundamental para compartir código, colaborar con otros desarrolladores y mantener un control preciso de las versiones de tu proyecto. Git es un sistema de control de versiones que me permite trabajar cambios sobre mi código con seguridad. 

En esta sección, te presentaremos algunas pautas y mejores prácticas esenciales de GitHub y Git para trabajar eficazmente con repositorios remotos. Estas directrices te ayudarán a gestionar y colaborar en proyectos de manera efectiva, desde clonar y colaborar en repositorios hasta sincronizar y contribuir al código de otros.</p>
## Configurando la autentificación SSH para una cuenta Github

<p align="justify">La autenticación SSH (Secure Shell) permite interactuar con GitHub de manera segura, sin necesidad de ingresar tu usuario y contraseña cada vez que accedes a tu cuenta o realizas operaciones de Git. En lugar de usar las credenciales habituales, GitHub utiliza un par de claves SSH: una **clave privada** y una **clave pública**.</p>

### **Comprueba las claves SSH existentes**
<p align="justify">Primero, comprueba si tienes claves SSH en tu PC. Abre tu terminal y ejecuta el siguiente comando:
</p>
```bash

ls -al ~/.ssh

```

Este comando listará cualquier clave SSH existente en tu directorio `~/.ssh`.
  
### **Generar claves pares SSH**
<p align="justify">Si no tienes una clave SSH o quieres generar un nuevo par, puedes hacerlo con el siguiente comando:  </p>

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Reemplaza `"your_email@example.com"` con el email asociado a tu cuenta de GitHub.

Presiona `Enter` para aceptar la localización del archivo por defecto y una frase vacía si prefieres no usar una doble validación. Este paso creara un nuevo par de claves SSH.

### **Añade la clave SSH al agente SSH**

Ahora, necesitas añadir tu clave SSH al agente SSH. Ejecuta el siguiente comando:

```bash
eval "$(ssh-agent -s)"

ssh-add ~/.ssh/id_ed25519
```

Asegurate de usar el camino correcto para tu clave privada (`~/.ssh/id_ed25519` en este ejemplo).

### **Copia la clave pública SSH a GitHub**
<p align="justify">Ahora, necesitas copiar tu clave SSH a tu cuenta de GitHub. Es posible usar el siguiente comando para copiarla en el portapapeles:</p>
```bash
pbcopy < ~/.ssh/id_ed25519.pub
```
<p align="justify">Entonces, dirígete a los ajustes de tu cuenta de GitHub, navega a 'SSH and GPG keys' y pincha en 'New SSH key'. Pega la clave publica en el campo 'Clave' y dale un título.</p>
### **Prueba la conexión SSH**
<p align="justify">Asegúrate que tu clave esta correctamente construida y ajustada, puedes testear la conexión a GitHub:</p>
```bash
ssh -T git@github.com
```

Puede que se te solicite confirmar la autenticidad. Presiona `Enter` y selecciona 'yes'. Si todo ha sido correctamente realizado, deberías recibir un mensaje como el siguiente:

> [!NOTE]
> Hi username! You've successfully authenticated, but GitHub does not provide shell access.
<p align="justify">Ahora, deberías poder clonar y trabajar con tus repositorios de GitHub utilizando la autenticación SSH, que es más segura y no requiere Tokens de Acceso Personal (PAT) para autenticación.</p>

## Flujo de trabajo con Git

El flujo de trabajo en Git es el conjunto de pasos y prácticas que sigues para desarrollar, gestionar y colaborar en un proyecto de software usando Git como sistema de control de versiones. Estos son algunos de los comandos más comunes en Git, pero Git ofrece una amplia gama de funcionalidades. 

| **Comandos**                       | **Descripcion**                                                                                                                               |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **git --version**                  | Verificar si Git está instalado                                                                                                               |
| **git config --global user.name**  | Configura el nombre de Usuario en Git                                                                                                         |
| **git config --global user.email** | Configura el email en Git                                                                                                                     |
| **git init**                       | Inicializa un nuevo repositorio Git en el directorio actual                                                                                   |
| **git clone <URL>**                | Clona un repositorio Git existente desde la URL especificada en tu computadora local                                                          |
| **git status**                     | Muestra el estado actual de los archivos en el repositorio, indicando qué archivos han sido modificados, agregados o eliminados               |
| **git add <archivo(s)>**           | Agrega archivos al área de preparación (staging) para ser confirmados en el próximo commit                                                    |
| **git commit -m "mensaje"**        | Confirma los cambios en el repositorio con un mensaje descriptivo que explica qué se hizo en ese commit                                       |
| **git pull**                       | Obtiene los cambios desde el repositorio remoto y los fusiona con tu rama local                                                               |
| **git push**                       | Envía los cambios confirmados localmente al repositorio remoto.                                                                               |
| **git branch**                     | Lista todas las ramas en el repositorio y muestra la rama actual resaltada                                                                    |
| **git checkout <nombre_rama>**     | Cambia a una rama específica en el repositorio                                                                                                |
| **git merge <nombre_rama>**        | Muestra un registro de commits en la rama actual, incluyendo detalles como el autor, la fecha y el mensaje del commit                         |
| **git log**                        | Realiza operaciones y agrupación de datos en un Dataframe                                                                                     |
| **git remote -v**                  | Muestra una lista de los repositorios remotos configurados y sus URLs                                                                         |
| **git fetch**                      | Obtiene los cambios desde el repositorio remoto sin fusionarlos en tu rama local                                                              |
| **git reset <archivo(s)>**         | Descarta los cambios en el área de preparación de archivos específicos                                                                        |
| **git stash**                      | Guarda temporalmente los cambios no confirmados en una pila (stash) para poder trabajar en otra tarea y luego recuperar los cambios más tarde |
| **git remote add origin <URL>**    | Agrega un repositorio remoto con el alias "origin" y la URL especificada                                                                      |
| **git remote remove origin**       | Elimina el repositorio remoto llamado "origin" (o cualquier otro alias especificado)                                                          |

### **Instalar Git**

Si aún no tienes Git instalado en tu Mac, puedes hacerlo siguiendo estos pasos:  
1. Abre la Terminal (puedes encontrarla en la carpeta "Utilidades" dentro de la carpeta "Aplicaciones").
2. Ejecuta el siguiente comando para verificar si Git está instalado:

```bash
git --version
```

Si Git no está instalado, se te pedirá que lo instales. Sigue las instrucciones para hacerlo.
### **Configurar Git**

Antes de continuar, debes configurar tu nombre de usuario y dirección de correo electrónico en Git. Esto es importante para que tus contribuciones queden registradas correctamente en GitHub.

1. Verifica las configuraciones actuales de GIT para 'user.name' y 'user.email' ejecutando el siguiente comando:

```bash
git config --list --show-origin --name-only | grep user.name
```
  
2. Elimina las configuraciones no deseadas utilizando el siguiente comando en la Terminal:

```bash
git config --global --unset-all user.name
```
  
3. Ejecuta estos comandos, reemplazando "Tu Nombre" y "tu@email.com" con tu información real:

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
```
### **Crear un repositorio en GitHub**

1. Ve a GitHub (https://github.com) y asegúrate de estar conectado a tu cuenta.
2. Haz clic en el botón "+" en la esquina superior derecha y selecciona "Nuevo repositorio".
3. Completa la información del repositorio, incluyendo el nombre, descripción y otras opciones según tus necesidades.
4. Marca la casilla "Inicializar este repositorio con un README" si deseas crear un archivo README.md inicial. Luego, haz clic en el botón "Crear repositorio".

### **Clonar el repositorio en tu Mac**
  
Ahora, clonaremos el repositorio en tu Mac para que puedas empezar a trabajar en él. Reemplaza `nombredeusuario` y `nombredelrepositorio` con tu nombre de usuario de GitHub y el nombre de tu repositorio:

```bash

git clone https://github.com/nombredeusuario/nombredelrepositorio.git

```

Esto creará una copia local del repositorio en tu Mac.

### **Agregar archivos y hacer un commit**

1. Coloca los archivos que deseas subir al repositorio en la carpeta clonada en tu Mac.
2. Abre la Terminal y navega hasta la carpeta del repositorio utilizando el comando `cd`, por ejemplo:  

```bash
cd nombredelrepositorio
```

3. Usa los siguientes comandos para agregar los archivos al área de preparación y hacer un commit:

```bash
git add .
git commit -m "Mensaje de commit"
```

### **Verifica el estado de tus cambios**

Veamos el estado de los cambios realizados hasta ahora.

```bash
git status
```

Deberíamos ver el siguiente mensaje:

> [!NOTE]
> *'On branch main
> Your branch is up to date with 'origin/main'.
> nothing to commit, working tree clean*

### **Subir los cambios a GitHub**

Finalmente, sube los cambios a tu repositorio en GitHub con el siguiente comando:

```bash
git push origin main
```

  Donde `main` es la rama principal por defecto. Si tu repositorio utiliza otra rama principal, reemplázala en el comando anterior.
### **Cerrar conexión con un repositorio remoto**

<p align="justify">Para desconectar el repositorio actual, puedes simplemente cerrar la terminal o la ventana de la terminal. Esto terminará cualquier conexión o sesión con ese repositorio.</p>
<p align="justify">Es recomendable cambiar a la rama principal antes de desconectar el repositorio actual, en caso de estar en una rama diferente de la principal. Puedes hacerlo con el comando:</p>

```bash
git checkout main 
```

Reemplaza `main` con el nombre de tu rama principal si es diferente.