# Panel de mortalidad académica

Página web de un solo archivo (`index.html`) que lee el Excel de mortalidad académica **en el navegador de quien lo usa** y muestra:

- **Resumen:** resultados por programa, semestre y jornada, con gráficos.
- **Grupos críticos:** plan de refuerzo con prioridad, acción sugerida y dependencia de notas 0,0.
- **Alertas por estudiante:** niveles Alta, Media y Baja para el seguimiento de Bienestar.
- **Notas 0,0:** lista para verificar con los docentes y escenario sin esas notas.

El panel **no guarda ni envía datos**. Al cerrar la pestaña, la información desaparece.

## Publicar en GitHub Pages (plan gratuito)

1. Cree un repositorio **público**, por ejemplo `panel-mortalidad`. El plan gratuito de GitHub Pages solo funciona con repositorios públicos.
2. Suba `index.html`, `README.md` y `.gitignore`. **No suba ningún Excel.**
3. En el repositorio, vaya a **Settings > Pages**. En «Build and deployment», elija **Deploy from a branch**, rama `main` y carpeta `/ (root)`. Guarde.
4. Espere uno o dos minutos. La dirección será `https://SU-USUARIO.github.io/panel-mortalidad/`.
5. Abra la dirección, arrastre el Excel y use el panel.

Como la página es pública, cualquiera que conozca la dirección puede abrir el panel, pero **sin el Excel no ve ningún dato**. La página incluye la etiqueta `noindex` para que los buscadores no la listen.

## Reglas de manejo de datos

- Nunca suba el Excel, ni capturas con nombres, a GitHub ni a ningún sitio público. Si lo hace por error, borrarlo del repositorio no basta (queda en el historial): trate esos datos como expuestos, avise a la Secretaría General y elimine el repositorio.
- Por defecto el panel muestra códigos en lugar de nombres de estudiantes y docentes. Active los nombres solo con personal autorizado.
- Los archivos que se exportan desde el panel contienen datos personales cuando se activan los nombres: guárdelos en carpetas institucionales con acceso restringido.
- Antes de usarlo, confirme con la Secretaría General o con quien corresponda que el tratamiento cumple la política institucional de datos personales y la Ley 1581 de 2012.

## Uso en cada corte

1. Actualice el Excel de la Coordinación con las nuevas notas (misma estructura de hojas).
2. Abra el panel y cargue el archivo.
3. Revise primero la cinta verde «Cuadra con el Informe del Excel». Si aparece una advertencia amarilla, hay diferencias entre el panel y el Informe: revise las notas o los parámetros.
4. Use «Exportar a Excel» para generar las listas de seguimiento y regístrelo allí (el panel no guarda cambios).

## Formato esperado del Excel

- Cada hoja de notas tiene una fila de encabezados con **NOMBRES** y **ASIGNATURA**, y columnas **BÁSICO, INTERMEDIO, APROPIACIÓN, AVANZA, SEMESTRE, JORNADA, DOCENTE** y, opcionalmente, **GRUPO**.
- Se ignoran las filas vacías y los encabezados repetidos.
- Si existe una hoja que empiece por «Informe», se toman de ahí la nota aprobatoria (B5), el promedio mínimo del quinto momento (B6) y la nota máxima (B7), y se compara el total institucional.
- Los programas se toman del nombre de la hoja (por ejemplo, «TECNOLOGIA 2026-2»).

## Reglas de cálculo

- Cada momento vale 25 %. Los momentos sin nota se asumen en la nota máxima (5,0).
- **Sí, puede aprobar:** promedio proyectado de 4,0 o más. **Solo con 5.º momento:** entre 3,5 y 4,0. **No alcanza:** menos de 3,5.
- **Alerta alta:** al menos una asignatura en «No alcanza» o tres o más en riesgo. **Media:** dos en riesgo. **Baja:** una.
- **Grupos:** rojo desde 20 % de estudiantes en riesgo, amarillo desde 10 %.
- Todos los umbrales se pueden cambiar en «Parámetros», y sus valores por defecto están en `DEFAULTS` dentro de `index.html`.

## Verificación

El cálculo se probó con el archivo de corte 2 de 2026-2 y coincide con el Informe del Excel en los totales: 2.173 inscripciones, 315 estudiantes, 272 y 310 que pierden Básico e Intermedio, 95 «Solo con 5.º momento», 26 «No alcanza» y 74 estudiantes en riesgo.

## Personalización y licencias

- Título, colores y tipografía: variables CSS al comienzo de la etiqueta `<style>`.
- La página no hace conexiones externas: la etiqueta `Content-Security-Policy` bloquea el envío de datos y la librería de lectura de Excel va incluida en el mismo archivo.
- Incluye SheetJS (xlsx 0.18.5, Apache-2.0) para leer y escribir archivos de Excel.
