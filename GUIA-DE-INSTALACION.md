# Agenda de Tutorías de Proyectos de Egreso
## Guía de instalación

Esta guía sirve tanto para la primera instalación como para cualquier otro instituto
que adopte la herramienta. Cada instalación tiene su propia hoja de cálculo y sus
propios datos: nada queda en la cuenta de nadie más.

Lleva unos veinte minutos la primera vez.

---

## Lo que se necesita

- Una cuenta de Google (personal o institucional).
- Una cuenta de GitHub, gratuita.

---

## Paso 1 — Crear la hoja de cálculo

1. Entrar a [sheets.google.com](https://sheets.google.com) y crear una hoja en blanco.
2. Ponerle un nombre reconocible, por ejemplo **Agenda Tutorías TA4 2026**.

Esta hoja va a ser la base de datos. No hay que armar nada adentro: las pestañas
se crean solas en el paso siguiente.

---

## Paso 2 — Instalar el código

1. En la hoja, menú **Extensiones → Apps Script**.
2. Se abre un editor con un archivo `Código.gs` que trae unas líneas de ejemplo.
   Borrar todo lo que haya.
3. Abrir el archivo `Codigo.gs` de este paquete, copiar todo su contenido y pegarlo ahí.
4. Guardar con el ícono del disquete.
5. Arriba hay un desplegable de funciones. Elegir **instalar** y presionar **Ejecutar**.
6. Google va a pedir autorización la primera vez. Ver la sección siguiente antes de
   continuar.
7. Cuando termine, volver a la hoja: van a estar las pestañas CONFIG, GRUPOS,
   RESERVAS, BLOQUEOS e INTENTOS, ya con los grupos de proyecto y los feriados cargados.

---

## Sobre la pantalla de permisos

Al ejecutar `instalar` por primera vez, Google pide autorización. Es normal y ocurre
con cualquier script propio. Lo que conviene decidir antes es si quiere los avisos
automáticos por correo, porque de eso depende cuán simple sea esta pantalla.

**Sin avisos por correo — instalación sin advertencias.**
Antes de guardar el código, en `Codigo.gs` buscar el cartel que dice
`SECCIÓN OPCIONAL — AVISOS POR CORREO` y seguir la instrucción que está ahí:
borrar esa sección y dejar en su lugar la línea `function avisarCancelaciones() {}`.
Con eso el script solo pide permiso sobre **esta** hoja de cálculo, y la autorización
es una pantalla común de "permitir acceso". Los bloqueos y las cancelaciones siguen
funcionando igual; simplemente no sale correo.

**Con avisos por correo.**
Dejar el código como está. Es posible que aparezca una pantalla que dice
**"Google no verificó esta aplicación"**, con un botón grande para volver atrás y
ninguna opción visible para seguir. No es un error ni una alerta de virus: Google la
muestra para cualquier script que pida permiso de enviar correo y no haya pasado por
su proceso de revisión, que está pensado para aplicaciones de distribución masiva.
La "aplicación" acá es el código que usted misma acaba de pegar en su propia cuenta.

Para pasarla: **Configuración avanzada** (abajo a la izquierda) → el enlace chico que
dice **Ir a (nombre del proyecto)** → **Permitir**. Se hace una sola vez.

---

## Paso 3 — Publicar el servicio

1. En el editor de Apps Script, botón **Implementar → Nueva implementación**.
2. En el engranaje, elegir el tipo **Aplicación web**.
3. Completar:
   - **Ejecutar como:** Yo
   - **Quién tiene acceso:** Cualquier usuario
4. **Implementar**, y copiar la **URL de la aplicación web**. Termina en `/exec`.

> Guardar esa URL: se usa en el paso siguiente.
>
> Si su cuenta es institucional y el administrador bloquea la opción
> "Cualquier usuario", hay que instalar la herramienta con una cuenta personal
> de Google. Es una restricción del dominio, no de la herramienta.

---

## Paso 4 — Conectar las dos páginas

En los archivos `agenda.html` y `panel.html`, cerca del comienzo del bloque de
código, hay una línea así:

```javascript
const API = "PEGAR_AQUI_LA_URL_DEL_APPS_SCRIPT";
```

Reemplazar el texto entre comillas por la URL del paso anterior, **en los dos
archivos**. Se puede editar con cualquier editor de texto, o directamente en
GitHub una vez subidos.

---

## Paso 5 — Publicar en GitHub Pages

1. Entrar a [github.com](https://github.com) y crear un repositorio nuevo.
   Marcarlo como **Public** (GitHub Pages gratuito requiere repositorio público).
2. Subir los archivos `agenda.html` y `panel.html` con **Add file → Upload files**.
3. Ir a **Settings → Pages**.
4. En **Source**, elegir **Deploy from a branch**, rama `main`, carpeta `/ (root)`. Guardar.
5. A los pocos minutos las páginas quedan en:
   - Estudiantes: `https://USUARIO.github.io/REPOSITORIO/agenda.html`
   - Panel docente: `https://USUARIO.github.io/REPOSITORIO/panel.html`

**Solo se reparte el primer enlace.** El del panel no se comparte con estudiantes.

> El repositorio es público, así que el código está a la vista —es lo que corresponde
> a una obra con licencia abierta—, pero **los datos no**: viven en su hoja de cálculo
> privada. Lo que sí queda visible es la dirección del Apps Script. Ver la nota de
> seguridad al final.

---

## Paso 6 — Configurar la herramienta

Entrar al panel docente. La clave inicial es **cambiar1234**.

**La agenda arranca cerrada.** Los estudiantes que entren van a ver un aviso de que
todavía no está disponible. Se abre cuando usted lo decide, y no antes.

En la pestaña **Configuración**, arriba de todo, hay una lista de lo que falta
completar para poder abrirla:

- Turnos de tutoría definidos
- Grupos de proyecto cargados
- Período definido (primer lunes y cantidad de semanas)
- Correo del grupo de clase cargado
- Clave del panel cambiada

A medida que complete cada punto, se marca solo. Cuando estén los cinco, el botón
**Abrir la agenda** se habilita.

Los turnos se cargan uno por renglón, con hora de comienzo y de finalización. Se
agregan y se quitan con los botones de esa sección.

En la pestaña **Grupos**, ajustar la lista de grupos de proyecto.

## Tutorías obligatorias

Es un régimen distinto de la tutoría. El grupo no reserva: se compromete a estar
trabajando en sala determinados días y turnos, mientras el docente puede estar
atendiendo una tutoría de otro grupo en simultáneo. Por eso la permanencia **no
ocupa el horario**: otro grupo puede reservar tutoría en esa misma franja.

Cada compromiso se registra en la pestaña **Grupos** e incluye el grupo, los días de
la semana, el turno de inicio y el de finalización, y su vigencia. La vigencia es lo
que permite que un grupo entre en régimen obligatorio en cualquier momento del
período y salga después, sin que se le computen inasistencias fuera de ese lapso.

En la grilla semanal, cada celda indica qué grupos deben encontrarse en sala. En la
pestaña **Asistencia**, cada jornada transcurrida lista por separado los grupos con
permanencia y los que agendaron tutoría, para registrar unos y otros.

Cada acción del panel confirma en pantalla que se guardó. Si no aparece la
confirmación, el cambio no se aplicó.

> **Cambiar turnos con tutorías ya reservadas.** Si corrige el horario de un turno,
> las tutorías reservadas ahí se conservan y se mudan solas al horario nuevo. Si
> elimina un turno, el panel le muestra qué tutorías se cancelarían antes de aplicar
> el cambio. En los dos casos sale un correo al grupo de clase pidiendo disculpas y
> avisando qué hacer. Las tutorías que ya se dictaron nunca se tocan: conservan su
> asistencia y sus notas.

---

## Paso 7 — Repartir el enlace

Los estudiantes entran a la página de la agenda y eligen su grupo de proyecto.
La primera vez, el grupo define un código de cuatro cifras que después comparten
entre sus integrantes. Si lo olvidan, se reinicia desde la pestaña **Grupos**.

Conviene avisar en clase que **cada grupo elija su propio código**, para que nadie
reclame el de otro por error.

---

## Uso cotidiano

| Para… | Ir a |
|---|---|
| Bloquear un feriado, una asamblea o una actividad institucional | Agenda y bloqueos |
| Registrar asistencia de tutorías y de tutorías obligatorias | Asistencia |
| Grupos, permanencia obligatoria y reinicio de códigos | Grupos |
| Ver el acumulado por grupo y descargar respaldos | Síntesis |
| Abrir o cerrar la agenda a los estudiantes | Configuración |
| Cargar o corregir feriados y jornadas institucionales | Feriados |
| Asignaturas presentes en tutoría y sus horarios | Asignaturas |
| Respaldo de todo lo que el sistema comunicó | Comunicaciones |
| Convocar a un grupo a una tutoría obligatoria | Agenda y bloqueos → tocar un horario libre |

## Asignaturas

Los estudiantes eligen cuándo asistir según qué asignaturas están presentes ese día,
así que la grilla muestra en cada horario las asignaturas disponibles.

En la pestaña **Asignaturas**, la carga rápida incorpora las denominaciones y las
horas semanales de una carrera con un botón. Después se completa, para cada una, en
qué días y turnos está presente: eso varía de un grupo a otro. La columna Turnos
compara lo asignado con las horas semanales y marca en rojo cuando no coinciden.

Al comenzar un período nuevo, la pestaña reclama verificar los horarios y no deja de
hacerlo hasta que se pulsa **Horarios verificados**. Es deliberado: un error acá se
traslada directamente a los estudiantes.

El traslado entre instalaciones copia la configuración a otra copia de la herramienta
sin volver a escribirla.

## Comunicaciones

Todo lo que el sistema envía queda asentado en la pestaña **Comunicaciones**, con su
fecha, destinatario, asunto, texto completo y si se envió o falló. Es el respaldo:
existe aunque el correo no haya salido.

Cada grupo de proyecto registra su propia dirección de correo la primera vez que
ingresa a la agenda, junto con su código. Los avisos van directo al grupo afectado.
Si en la configuración hay una dirección cargada, recibe copia de todo.

## Feriados

La pestaña **Feriados** trae cargados los del calendario oficial del año en curso.
Se editan, se quitan y se agregan como cualquier lista: sirve también para jornadas
institucionales, asambleas o el aniversario de la escuela. Cada día de esa lista
queda bloqueado en la agenda con su nombre como motivo.

Cuando el período pase a un año nuevo, la pestaña avisa que no hay feriados cargados
para ese año y ofrece el botón **Cargar feriados del nuevo período**. Los genera con
la regla de la ley vigente y los marca como **provisorios**, porque la norma cambia
y el calendario oficial manda. Hay que compararlos con el calendario del año y
corregir lo que corresponda: al editar uno, deja de ser provisorio.

## Convocatorias

En la pestaña **Agenda y bloqueos**, al tocar un horario libre se puede **convocar a
un grupo** en vez de bloquearlo. La tutoría queda agendada como obligatoria: el grupo
la ve marcada como convocatoria y no puede cancelarla. Se elige el grupo, la dirección
de correo a la que enviar el aviso, y se puede agregar texto al mensaje predeterminado.

Solo se puede convocar sobre horarios libres: nunca desplaza una reserva de otro grupo.

**Descargar el respaldo en CSV cada tanto.** La hoja de cálculo ya es una copia de
los datos, pero un respaldo aparte no cuesta nada y protege de un borrado accidental.

---

## Nota de seguridad, sin adornos

- La clave del panel se verifica en el servidor, no en el navegador: quien no la
  tenga no puede ejecutar acciones del panel aunque lea el código de la página.
- El código de cuatro cifras identifica al **grupo**, no a cada estudiante. Los
  integrantes lo comparten. Después de cinco intentos fallidos, el grupo queda
  bloqueado diez minutos.
- La dirección del Apps Script es visible en el código de la página. Alguien con
  conocimiento técnico podría escribir en la hoja por fuera de la interfaz. Para una
  agenda de tutorías el riesgo es bajo, y el historial de versiones de Google Sheets
  permite deshacer cualquier cambio.
- Si alguna vez cambia la URL del Apps Script (por ejemplo, al crear una
  implementación nueva en vez de actualizar la existente), hay que actualizarla en
  los dos archivos HTML.

---

## Actualizaciones del código

Si más adelante se modifica el `Codigo.gs`, no crear una implementación nueva:
usar **Implementar → Administrar implementaciones → Editar → Versión: Nueva**.
Así la URL se mantiene y no hay que tocar los HTML.

---

**Agenda de Tutorías de Proyectos de Egreso**
© 2026 Tamara Ricketts. DGETP.
Licencia Creative Commons Atribución-NoComercial-CompartirIgual 4.0 Internacional (CC BY-NC-SA 4.0).
Usted es libre de compartir y adaptar esta herramienta, siempre que atribuya la autoría
original, no la utilice con fines comerciales, y distribuya sus adaptaciones bajo esta
misma licencia.
Texto completo: https://creativecommons.org/licenses/by-nc-sa/4.0/deed.es
Cita sugerida: Ricketts, T. (2026). *Agenda de Tutorías de Proyectos de Egreso*
[software educativo]. CC BY-NC-SA 4.0.
