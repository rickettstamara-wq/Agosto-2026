# PROCEDIMIENTO DE ACTUALIZACIÓN DE VERSIÓN

**Sistema de Gestión de Proyectos de Egreso.** Guarde este documento: el procedimiento
es siempre el mismo.

La herramienta tiene **dos partes que se actualizan por separado**:

| Parte | Dónde vive | Qué contiene |
|---|---|---|
| El motor | Apps Script, dentro de la planilla | `Codigo.gs` |
| Las páginas | GitHub Pages | `panel.html` y `agenda.html` |

Actualizar una no actualiza la otra. Si le pasaron los cuatro archivos, van los cuatro.

---

## Parte 0 — Con el sistema en uso

Una vez que hay estudiantes con sus códigos y correos cargados, la actualización
lleva dos precauciones más. **Los datos nunca están en el código: viven en la
planilla.** Reemplazar `Codigo.gs` o los HTML no los toca.

**Antes de empezar**

1. Panel → **Configuración → Cerrar la agenda**. Mientras dura la actualización
   ningún estudiante queda a mitad de camino entre una versión y otra.
2. Planilla → **Archivo → Hacer una copia**. Es el respaldo verdadero: conserva
   todo, no solo lo que exportan los CSV.
3. Panel → **Síntesis** → descargar los tres respaldos en CSV.

**Después de terminar**

4. Verificar que el panel carga y que los grupos siguen con su código y su correo
   en la pestaña Grupos.
5. Abrir un enlace de estudiante y comprobar que la grilla se ve.
6. Panel → **Configuración → Abrir la agenda**.

**Si algo sale mal**

- Apps Script conserva las versiones anteriores: **Implementar → Administrar
  implementaciones → lápiz → Versión**, y elegir la anterior.
- GitHub conserva el historial de cada archivo: se puede volver a una versión
  previa desde el propio repositorio.
- La copia de la planilla del punto 2 permite reponer los datos.

**Cuándo hace falta ejecutar `instalar`:** solo cuando la actualización agrega
hojas o columnas nuevas. Se lo indico en cada entrega. Es la única operación que
reescribe la planilla, y por eso el respaldo previo.

**Cuándo conviene hacerlo:** fuera del horario de tutorías. Entre que se
reimplementa el Apps Script y se reemplazan los HTML hay unos minutos en que las
páginas viejas hablan con el servidor nuevo.

---

## Parte 1 — El código (Apps Script)

**Solo si le pasaron un `Codigo.gs` nuevo.**

1. Abrir la planilla → menú **Extensiones → Apps Script**.
2. Seleccionar todo el contenido del editor y borrarlo.
3. Pegar el `Codigo.gs` nuevo completo.
4. Guardar (ícono del disquete).
5. **Implementar → Administrar implementaciones**.
6. Tocar el **lápiz** de editar sobre la implementación existente.
7. En el desplegable **Versión**, elegir **Nueva versión**. La descripción se completa sola.
8. **Implementar**.

> **Nunca elegir "Nueva implementación".** Eso crea una dirección distinta y obliga
> a rehacer toda la Parte 2. Siempre "Administrar implementaciones" y versión nueva.

> **No hace falta tocar el botón Ejecutar.** Solo se usa cuando hay pestañas nuevas
> que crear, y en ese caso conviene hacerlo desde la planilla: menú
> **Sistema de Proyectos de Egreso → Instalar / reparar hojas**. Nunca borra datos existentes.

---

## Parte 2 — Las páginas (GitHub)

**Para cada archivo HTML nuevo, uno por vez.**

1. Entrar al repositorio → abrir el archivo que se reemplaza (`panel.html` o `agenda.html`).
2. Tocar el ícono de los **tres puntitos** → **Delete file** → **Commit changes**.
3. **Add file → Upload files**, subir el archivo nuevo → **Commit changes**.
4. Abrir el archivo recién subido y tocar el **lápiz** de editar.
5. **Ctrl+F**, buscar `PEGAR_AQUI`.
6. Seleccionar **únicamente** el texto `PEGAR_AQUI_LA_URL_DEL_APPS_SCRIPT`, sin tocar
   las comillas ni nada alrededor, y pegar encima la dirección del Apps Script.
7. **Verificar que la primera línea del archivo siga diciendo `<!DOCTYPE html>`.**
8. **Commit changes**.
9. Repetir del 1 al 8 con el otro archivo.

### La dirección que hay que pegar

```
https://script.google.com/macros/s/AKfycbzRhLC9ryra6bsnhPP-PjGii0V8KZSeKqZ7GOz4BXr1NwNCgJA4aKVNDplDB5MIs0ID1A/exec
```

> **Este es el paso que más se olvida.** Los archivos nuevos vienen siempre con el
> texto sin reemplazar. Si se saltea, la página abre pero dice
> *"no está conectada a su hoja de cálculo"*.

---

## Parte 3 — Verificar

1. En GitHub, pestaña **Actions**: esperar a que la primera publicación de la lista
   tenga tilde verde. Tarda entre uno y cinco minutos.
2. Abrir el panel agregando `?v=` y un número que no haya usado antes:
   `.../panel.html?v=7`. Ese agregado obliga al navegador a traer la versión nueva.
   No forma parte de la dirección: para el uso diario va sin él.
3. Comprobar que carga y que aparece lo que se agregó en esta actualización.

---

## Las direcciones

| | |
|---|---|
| Panel docente | `https://rickettstamara-wq.github.io/Agosto-2026/panel.html` |
| Agenda de estudiantes | `https://rickettstamara-wq.github.io/Agosto-2026/agenda.html?g=CÓDIGO` |

La agenda de estudiantes **necesita el código de la agenda al final**. Cada grupo de
clase tiene el suyo, formado por año, escuela y código de grupo (por ejemplo
`2026-ISCAB-TA4`). El enlace exacto figura en el panel, en Configuración, listo para
copiar. Sin ese código la página avisa que hay que usar el enlace del docente.

La dirección base sin nombre de archivo da error 404. Es normal: no hay página de inicio.

---

## Si algo no funciona

| Síntoma | Causa | Solución |
|---|---|---|
| "No está conectada a su hoja de cálculo" | Falta pegar la dirección en ese archivo | Parte 2, pasos 4 a 8 |
| Se ve el código como texto suelto | El archivo se dañó al pegar | Borrarlo y volver a subirlo |
| Los cambios no aparecen | Copia guardada en el navegador | `?v=` con número nuevo, o Ctrl+Shift+R |
| "Falta la hoja X" | Hay pestañas nuevas sin crear | Planilla → menú **Sistema de Proyectos de Egreso → Instalar / reparar hojas** |
| Error al ejecutar `instalar` desde el editor | No puede mostrar el cartel de confirmación | Las hojas ya se crearon igual; verificar en la planilla |
| Error 404 en la dirección base | No hay página de inicio | Agregar `panel.html` o `agenda.html` al final |

---

**Sistema de Gestión de Proyectos de Egreso**
© 2026 Tamara Ricketts. CC BY-NC-SA 4.0
