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

# 4 Convencion de commits convencionales

Es importante seguir una convencion de commits que permita a otros desarrolladores entender rapidamente el proposito de cada cambio. Aqui se muestran ejemplos de los diferentes tipos de commits:

1. feat: Agrega una nueva funcion o caracteristica al proyecto.

```bash
git commit -m "feat: Agregar autenticación de usuarios"

```

2. fix: Corrige un error o bug en el codigo.
```bash

git commit -m "fix: Corregir error de desbordamiento de memoria"

```
3. docs: Realiza cambios o mejoras en la documentacion del proyecto.

```bash
git commit -m "docs: Actualizar el archivo README con instrucciones de instalación"

```

4. style: Realiza cambios en el formato o estilo del codigo, sin modificar su funcionamiento.
```bash

git commit -m "style: Aplicar sangría consistente en el archivo main.js"

```
5. refactor: Realiza cambios en el codigo para mejorar su estructura o legibilidad, sin cambiar su comportamiento
```bash
git commit -m "refactor: Reorganizar funciones de validación en un módulo separado"

```
6. test: Agrega o modifica pruebas unitarias o de integracion.

```bash

git commit -m "refactor: Reorganizar funciones de validación en un módulo separado"

```

7. chore: Realiza tareas de mantenimiento, actualizacion de dependencias, etc.

```bash
git commit -m "chore: Actualizar biblioteca de gráficos a la última versión"


```
## Licencia

Este proyecto está protegido por fernandoDev.

© 2024 Fernando Blanco. Todos los derechos reservados.
