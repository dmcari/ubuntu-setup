
# Conexión a Github a través de SSH

Describo la conexión a Github a través de SSH para múltiples cuentas. Por ejemplo, puede servir para tener configuradas una cuenta personal y una cuenta de trabajo en el mismo equipo.

## Cuenta personal
Primero generamos la clave ssh con la etiqueta del mail personal
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

A continuación, se genera la consulta: "Ingresar un archivo donde guardar la clave". Para aceptar la ubicación predeterminada del archivo (`/home/you/.ssh/id_rsa`) apretar `Enter`.

Posterior a ello hay que escribir una contraseña segura o `passphrase`.

Luego, podemos instalar `xclip` que sirve para copiar desde la terminal.

```
# Descarga de xclip
sudo apt-get install xclip

# Copia el contenido de id_rsa.pub (que es el nombre asignado por defecto anteriormente)
xclip -sel clip < ~/.ssh/id_rsa.pub
```

Finalmente, abrir en un navegador la cuenta de github > Settings > SSH y hacer `ctrl+V` en donde pide la clave. Asignar un título descriptivo y guardar.

## Segunda cuenta

Los pasos son los mismos pero con algunas diferencias:

Generar la clave ssh con la etiqueta del segundo mail
```
ssh-keygen -t rsa -b 4096 -C "work_email@example.com"
```

A continuación, se genera la consulta: "Ingresar un archivo donde guardar la clave". USAR OTRA UBICACIÓN que no sea la predeterminada del archivo. Por ejemplo: `/home/you/.ssh/id_rsa_work`) apretar `Enter`.

Posterior a ello hay que escribir una contraseña segura o `passphrase`.


```
# Copiar el contenido de id_rsa_work.pub (que es el nombre asignado anteriormente)
xclip -sel clip < ~/.ssh/id_rsa_work.pub
```

Finalmente, abrir en un navegador la segunda cuenta de github > Settings > SSH y hacer ctrl+V en donde pide la clave. Asignar un título descriptivo y guardar.

IMPORTANTE: Generar un archivo config en la carpeta .ssh

```
touch ~/.ssh/config
```
Editar este archivo agregando:

```
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa

Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_work
```

Al momento de indicar el origen de un repositorio, tener en cuenta que la conexión ssh será por ejemplo al clonar:

Para la primera cuenta:
```
git@github.com:my_user/my_repo.git
```

Para la segunda cuenta:
```
git@github-work:my_user/my_repo.git
```