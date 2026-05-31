# Especificación del sistema web: Biblioteca Personal de Animes y Series


## 1. Nombre del sistema


**AniTrack — Biblioteca Personal de Animes y Series**


---


## 2. Objetivo general


Desarrollar un sistema web para que un usuario pueda administrar su biblioteca personal de animes y series de forma ordenada, visual y persistente.


El sistema debe permitir:


- Registrar animes y series.
- Ver el listado completo del contenido guardado.
- Editar registros existentes.
- Cambiar el estado de visualización.
- Marcar contenidos como favoritos.
- Eliminar registros.
- Buscar títulos por nombre.
- Filtrar por tipo, estado, género y favoritos.
- Visualizar métricas básicas de la biblioteca.
- Guardar la información en una base de datos **SQLite**.


Este sistema está pensado como un ejercicio académico local, de dificultad media, adecuado para ser desarrollado por una fábrica de agentes de IA.


---


## 3. Alcance del sistema


El sistema será una aplicación web con interfaz moderna y estructura cliente-servidor.


Debe incluir:


- Backend web.
- Base de datos SQLite.
- Frontend web simple con **REACT + BOOTSTRAP**.
- API REST para operaciones CRUD.
- Validaciones básicas y de negocio.
- Dashboard simple con métricas.
- Búsqueda y filtros.
- Estructura clara de archivos.
- Documentación mínima para instalación y ejecución.


No se requiere autenticación de usuarios en esta primera versión.


---


## 4. Tipo de aplicación


Aplicación web monousuario.


El sistema podrá ejecutarse localmente en el computador del usuario usando un servidor de desarrollo.


Tecnologías sugeridas:


- Backend: Python con **FASTAPI**.
- Base de datos: **SQLite**.
- Frontend: **REACT + BOOTSTRAP**.


---


# 5. Funcionalidades principales


## 5.1 Registrar contenido


El usuario debe poder registrar un nuevo anime o serie desde un formulario.


Campos requeridos:


- Título.
- Tipo de contenido.
- Género principal.
- Estado de visualización.
- Plataforma opcional.
- Puntaje personal opcional.
- Comentario personal opcional.


Reglas:


- El título es obligatorio.
- El título debe tener entre 2 y 150 caracteres.
- El tipo solo puede ser: anime o serie.
- El estado inicial por defecto debe ser pendiente.
- El puntaje personal es opcional, pero si se informa debe estar entre 1 y 10.
- El comentario puede quedar vacío.


---


## 5.2 Listar contenidos


El sistema debe mostrar todos los contenidos registrados.


Cada registro debe mostrar:


- ID.
- Título.
- Tipo.
- Género.
- Estado.
- Plataforma.
- Puntaje.
- Indicador de favorito.
- Fecha de creación.
- Botones de acción:
  - Editar.
  - Cambiar estado.
  - Favorito / quitar favorito.
  - Eliminar.


Los registros deben mostrarse ordenados por fecha de creación descendente, mostrando primero los más recientes.


---


## 5.3 Editar contenido


El usuario debe poder modificar un contenido existente.


Campos editables:


- Título.
- Tipo.
- Género.
- Estado.
- Plataforma.
- Puntaje.
- Comentario.
- Favorito.


Reglas:


- No se puede guardar un registro sin título.
- Si el contenido no existe, se debe mostrar un mensaje de error.
- Al editar un registro, debe actualizarse el campo `updated_at`.


---


## 5.4 Cambiar estado de visualización


El usuario debe poder actualizar el estado de un anime o serie.


Estados permitidos:


- Pendiente.
- Viendo.
- Pausada.
- Terminada.
- Abandonada.


Reglas:


- Solo se permiten los estados definidos.
- Al cambiar el estado, debe actualizarse el campo `updated_at`.
- El cambio debe reflejarse inmediatamente en la interfaz.


---


## 5.5 Marcar como favorito


El usuario debe poder marcar o desmarcar un contenido como favorito.


Reglas:


- Si el contenido no es favorito, se marca como favorito.
- Si ya es favorito, se puede quitar de favoritos.
- El cambio debe persistirse en la base de datos.


---


## 5.6 Eliminar contenido


El usuario debe poder eliminar un registro.


Reglas:


- Antes de eliminar, la interfaz debe pedir confirmación.
- Si el contenido existe, se elimina de la base de datos.
- Si el contenido no existe, se muestra un mensaje de error.


---


## 5.7 Buscar contenido


El usuario debe poder buscar contenido por nombre.


Reglas:


- La búsqueda debe ignorar mayúsculas y minúsculas.
- El sistema debe mostrar coincidencias parciales.
- Si no hay coincidencias, debe mostrarse un mensaje claro al usuario.


---


## 5.8 Filtrar contenido


El usuario debe poder filtrar el listado.


Filtros mínimos:


- Por tipo: anime, serie, todos.
- Por estado: pendiente, viendo, pausada, terminada, abandonada, todos.
- Por favorito: sí, no, todos.
- Por género: opcional.


Los filtros deben poder combinarse entre sí.


---


## 5.9 Ver métricas de la biblioteca


El sistema debe mostrar un resumen visual con métricas básicas del contenido registrado.


Métricas mínimas:


- Total de contenidos.
- Total de animes.
- Total de series.
- Total en estado pendiente.
- Total en estado viendo.
- Total en estado terminada.
- Total de favoritos.


Estas métricas deben actualizarse automáticamente al crear, editar o eliminar registros.


---


# 6. Requisitos no funcionales


## RNF-01 Simplicidad


El sistema debe ser fácil de entender, instalar y ejecutar localmente.


## RNF-02 Ejecución local


El sistema debe ejecutarse sin depender de servicios externos obligatorios.


## RNF-03 Código ordenado


El código debe estar separado por responsabilidades: frontend, backend, modelos, rutas y servicios.


## RNF-04 Seguridad básica


El sistema debe validar los datos recibidos desde formularios y solicitudes HTTP.


## RNF-05 Usabilidad


La interfaz debe ser clara, simple, usable y responsive.


## RNF-06 Compatibilidad


El sistema debe funcionar en navegadores modernos.


## RNF-07 Persistencia confiable


La información debe conservarse al cerrar y volver a ejecutar la aplicación.


## RNF-08 Mantenibilidad


La estructura del proyecto debe facilitar futuras mejoras como autenticación o integración con APIs externas.


---


# 7. Flujo principal del usuario


1. El usuario abre la aplicación en el navegador.
2. El sistema muestra el dashboard y el listado de contenidos.
3. El usuario presiona “Agregar contenido”.
4. El usuario completa el formulario.
5. El sistema valida los datos.
6. El sistema guarda el registro en SQLite.
7. El sistema vuelve a la pantalla principal.
8. El usuario puede buscar, filtrar, editar, marcar favorito, cambiar estado o eliminar contenidos.


---


# 8. Casos de uso


## Caso de uso 1: Registrar un anime o serie


Actor: Usuario.


Flujo:


1. Usuario entra a la pantalla principal.
2. Usuario selecciona “Agregar contenido”.
3. Usuario ingresa título, tipo, género, estado y datos opcionales.
4. Usuario presiona “Guardar”.
5. Sistema valida los datos.
6. Sistema guarda el registro.
7. Sistema muestra mensaje de éxito.


Resultado: El contenido queda registrado en la biblioteca.


---


## Caso de uso 2: Cambiar el estado de visualización


Actor: Usuario.


Flujo:


1. Usuario visualiza el listado.
2. Usuario selecciona un contenido.
3. Usuario cambia el estado.
4. Sistema actualiza la base de datos.
5. Sistema refresca la interfaz.


Resultado: El contenido queda con su nuevo estado.


---


## Caso de uso 3: Marcar como favorito


Actor: Usuario.


Flujo:


1. Usuario visualiza un contenido.
2. Usuario presiona el botón de favorito.
3. Sistema actualiza el valor de favorito.
4. Sistema refresca la vista.


Resultado: El contenido queda marcado o desmarcado como favorito.


---


## Caso de uso 4: Buscar y filtrar contenido


Actor: Usuario.


Flujo:


1. Usuario escribe un nombre en la barra de búsqueda.
2. Usuario selecciona filtros complementarios.
3. Sistema procesa la consulta.
4. Sistema muestra solo los resultados coincidentes.


Resultado: El usuario encuentra contenido específico de forma rápida.


---


## Caso de uso 5: Eliminar un contenido


Actor: Usuario.


Flujo:


1. Usuario visualiza un contenido.
2. Usuario presiona “Eliminar”.
3. Sistema solicita confirmación.
4. Usuario confirma.
5. Sistema elimina el registro.


Resultado: El contenido ya no aparece en la biblioteca.


---


# 9. Criterios de aceptación


El sistema se considera terminado cuando cumple lo siguiente:


- Se puede ejecutar localmente.
- Crea automáticamente la base de datos SQLite si no existe.
- Permite registrar animes y series.
- Permite listar registros.
- Permite editar registros.
- Permite cambiar el estado de visualización.
- Permite marcar y desmarcar favoritos.
- Permite eliminar registros.
- Permite buscar por nombre.
- Permite filtrar por tipo, estado y favorito.
- Muestra métricas básicas actualizadas.
- Valida que el título no esté vacío.
- Valida que el puntaje, si existe, esté entre 1 y 10.
- Guarda los datos correctamente en SQLite.
- Tiene una interfaz simple, clara y entendible.
- Incluye un README con instrucciones de instalación y ejecución.


---


# 10. Checklist de pruebas


```text
[ ] La aplicación inicia sin errores.
[ ] La base de datos SQLite se crea automáticamente.
[ ] Se puede registrar un anime con datos válidos.
[ ] Se puede registrar una serie con datos válidos.
[ ] No se puede registrar un contenido sin título.
[ ] No se puede registrar un puntaje fuera del rango 1 a 10.
[ ] Se muestran los contenidos creados.
[ ] Se puede editar un contenido.
[ ] Se puede cambiar el estado de visualización.
[ ] Se puede marcar un contenido como favorito.
[ ] Se puede quitar un contenido de favoritos.
[ ] Se puede eliminar un contenido.
[ ] Se pide confirmación antes de eliminar.
[ ] La búsqueda por nombre funciona.
[ ] El filtro por tipo funciona.
[ ] El filtro por estado funciona.
[ ] El filtro por favoritos funciona.
[ ] Las métricas se actualizan correctamente.
[ ] Los datos persisten al reiniciar la aplicación.
```


---


# 25. Definición final del producto mínimo viable


El producto mínimo viable debe ser una aplicación web local llamada **AniTrackJota**, desarrollada con **FASTAPI, SQLite, REACT y BOOTSTRAP**, que permita administrar una biblioteca personal de animes y series mediante una interfaz simple y funcional.


Debe incluir registro, listado, edición, eliminación, cambio de estado, favoritos, búsqueda, filtros y visualización de métricas básicas.


El sistema debe estar organizado, documentado y listo para ser ejecutado como ejercicio académico.