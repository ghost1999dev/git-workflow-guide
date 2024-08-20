# Guia para trabajar con Git y convenciones de commits

Este documento proporciona una guia basica para gestionar ramas en Git y seguir las convenciones de commits convencionales en tus proyectos.

## 1. Actualizar la rama de desarrollo local con los cambios remotos

Si estas trabajando en la rama `develop`, es importante mantenerla actualizada con los ultimos cambios

```bash

git pull origin develop

```

## 2. Cambiar entre ramas

Para cambiar entre diferentes ramas en Git, puedes utilizar los siguientes comandos:

```bash
# Cambiar a una rama especifica
git switch <nombre-de-la-rama>

#0 alternativamente
git checkout <nombre-de-la-rama>
```

Ejemplo
```bash
# Cambiar a la rama develop
git switch develop

# Cambiar a tu rama de trabajo
git switch feat/mi-rama
```
# 3. Enviar los cambios al repositorio remoto

Una vez que hayas realizado tus cambios, debes aniadirlos, crear un commit con un mensaje descriptivo y finalmente enviarlos al repositorio remoto. Sigue estos pasos:

```bash

# Aniadir todos los cambios al area de preparacion
git add .

# Crear un commit con un mensaje que siga la convencion de commits convencionales
git commit -m "tipo: Descripcion breve del cambio"

# Enviar los cambios a la rama correspondientes en el repositorio remoto
git push origin <nombre-de-la-rama>
```

Ejemplo

```bash
git commit -m "feat: Agregar autenticación de usuarios"
git push origin feat/mi-rama

```