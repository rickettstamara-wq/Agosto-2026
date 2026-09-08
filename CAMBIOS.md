# Registro de cambios

Sistema de Gestión de Proyectos de Egreso
© 2026 Tamara Ricketts. CC BY-NC-SA 4.0

---

## Septiembre de 2026

Archivos modificados: `Codigo.gs`, `panel.html`, `agenda.html`.

### Módulo de Evaluaciones (nuevo)

Devoluciones del equipo docente a cada grupo de proyecto, por instancia de entrega.

- Dos hojas nuevas: `EVALUACIONES`, con una fila por grupo e instancia, y `EVALUACIONES_LOG`, con el registro de cada guardado y su autor.
- Calendario de entregas definido en `Codigo.gs`: 21 de agosto, 25 de septiembre y 30 de octubre como entregas preliminares, y 20 de noviembre como entrega final.
- Pestaña **Evaluaciones** en el panel, disponible para todo el equipo docente de la agenda. Muestra el estado de cada grupo: en blanco, escrita, sin enviar o enviada.
- Escritura colaborativa con edición exclusiva. Abrir una devolución es solo lectura y pueden hacerlo varios docentes a la vez; para escribir hay que tomar la edición desde adentro. Si otro la tiene tomada, se avisa quién y desde hace cuánto, y puede liberarse.
- Envío al grupo con el documento adjunto en PDF. Cualquier docente del equipo puede enviarlo. Una vez enviada, la devolución queda cerrada: no admite edición ni eliminación.
- Las devoluciones **no llevan copia** a la dirección de respaldo: son de cada grupo de proyecto. El módulo usa su propia vía de envío, separada del resto de los avisos.
- Si el grupo no tiene correo registrado —porque nunca se agendó a tutorías— se avisa en pantalla y se ofrece cargarlo en el momento. La dirección queda registrada para todos los avisos posteriores.
- Documento consolidado descargable con todas las devoluciones guardadas de una instancia: portada con los datos de la agenda, referencia a la rúbrica de los Términos de Referencia, índice y un proyecto por página. No se envía a nadie; se descarga desde el panel. Incluye solo grupos activos.

### Corrección: fechas de los avisos por correo

Los correos mostraban la fecha del día anterior. La causa era la conversión a UTC al construir la fecha, que en un contexto UTC-3 la corría hacia atrás.

Se incorporó `fechaLarga()`, que arma la fecha a partir de sus componentes, sin conversión posible, y devuelve el texto en español: *viernes 21 de agosto de 2026*.

Se aplicó a todos los avisos: reserva de tutoría, cancelaciones, cambios de horario y convocatorias. Los que antes mostraban la fecha en formato `2026-08-21` ahora la muestran en palabras.

### Corrección: datos expuestos en la agenda de estudiantes

La agenda es de acceso público: alcanza con el enlace. Hasta ahora el sistema le entregaba el estado completo de la agenda, que incluía, de **todos** los grupos, el tema de cada tutoría, los nombres de los integrantes, el estado de asistencia, las observaciones escritas por los docentes y el nombre de quién las escribió. La pantalla no mostraba esos datos, pero viajaban al navegador y eran accesibles.

Esto contradecía lo que el propio sistema declara a los docentes al darlos de alta: que sus observaciones no son accesibles para los estudiantes.

- El estado público entrega ahora solo lo necesario para la grilla: fecha, franja, grupo que ocupa cada horario y si se trata de una convocatoria. El estado de asistencia de las reservas ajenas va enmascarado.
- Los datos propios de cada grupo —tema, integrantes y asistencia— se piden por una vía nueva, `misDatos`, que exige el código del grupo y devuelve únicamente los suyos.
- Las observaciones del equipo docente no se entregan nunca, ni siquiera al propio grupo.

Como consecuencia, para ver el tema y los integrantes de una tutoría desde la agenda ahora hay que identificarse con el código del grupo.

### Panel: mejoras de visibilidad

- **Grilla de Agenda.** Las celdas ocupadas muestran un punto discreto cuando la reserva tiene tema o integrantes anotados. Antes esa información existía pero nada indicaba que hubiera que abrir la celda para verla.
- **Pestaña Asistencia.** El botón de observaciones pasó del signo `✎` a texto: dice **+ Observación** cuando no hay nada escrito y **Observación ✓** cuando ya hay. Permite ver de un vistazo en qué instancias falta registrar.

### Panel: título

Las pantallas de acceso y principal pasaron a decir *Sistema de Gestión de Proyectos de Egreso*, en lugar de *Agenda de tutorías*. La agenda de estudiantes conserva su título, que sigue siendo el correcto para esa vista.

---

## Instalación de esta versión

1. Pegar `Codigo.gs` en Apps Script y guardar.
2. Ejecutar **`instalar()`** una vez. Es imprescindible: crea las hojas `EVALUACIONES` y `EVALUACIONES_LOG`.
3. Implementar → Administrar implementaciones → editar la implementación en uso → Versión: **Nueva versión** → Implementar.
4. Subir `panel.html` y `agenda.html` al repositorio.

Los tres archivos van juntos. Si se actualiza solo el backend, la agenda deja de mostrar el tema y los integrantes de la tutoría propia.

### Advertencia sobre las implementaciones

Los archivos `panel.html` y `agenda.html` tienen la dirección del backend escrita adentro. Si el proyecto de Apps Script tiene más de una implementación activa, hay que actualizar **la que figura en esos archivos**, no cualquiera: crear una versión nueva en otra implementación no tiene ningún efecto y produce fallas difíciles de diagnosticar.

Conviene archivar las implementaciones que no estén en uso.

---

## Notas técnicas

**Generación de PDF.** Se arma HTML y Google lo convierte. El conversor es antiguo: respeta tablas, bordes, cuerpos, colores de texto e interletrado, pero **descarta los fondos de color** y no entiende las disposiciones modernas. Por eso la maqueta de los documentos está resuelta con filetes y jerarquía tipográfica, sin bandas de color.

**Fechas.** No usar el sufijo `Z` al construir fechas destinadas a mostrarse en contexto UTC-3: fuerza la interpretación en UTC y corre el día. Usar `fechaLarga()` o `fechaTexto()`.

**Hojas nuevas.** Al agregar una hoja hay que sumarla a `HOJAS` y también a las dos listas sueltas que aparecen dentro de `instalar()` y de `renombrarAgenda()`, si la hoja pertenece a una agenda. De lo contrario no hereda el grupo de clase al crearse ni lo sigue si el código de la agenda cambia.
