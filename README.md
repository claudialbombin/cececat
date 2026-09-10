# CeceCat 🐾

Gestor de torneos de debate por parejas (estilo académico), inspirado en Tabbycat, hecho a medida para el **Trofeo Rector de Comillas**.

Es una web estática de un solo archivo (`index.html`): todo el algoritmo de emparejamientos, puntuación y clasificación corre en el propio navegador. Por eso funciona perfectamente en GitHub Pages. Además del guardado local de siempre, ya tiene activado el envío remoto de puntuaciones por parte de los jueces (ver más abajo) usando tu propio proyecto Firebase gratuito "CeceCat" y tu propia cuenta de EmailJS — no hace falta configurar nada más, funciona en cuanto lo publiques.

## Qué hace

- Crear un torneo es un asistente guiado de 6 pasos, con botón "Atrás" en cada uno sin perder lo ya rellenado: 1) nombre del torneo, 2) formato de debate (y apartados de puntuación si es académico), 3) número de parejas, 4) cómo poner los nombres, 5) salas/aulas, 6) jueces.
  - **Formato (paso 2):** Académico (1 pareja a favor vs 1 en contra) o **British Parliamentary** (4 parejas por sala: OG, OO, CG y CO, rankeadas 1º–4º).
  - **Puntuación:**
    - **Académico:** tú decides los apartados de puntuación del torneo (p.ej. "Contenido", "Estilo", "Estrategia" — vienen esos tres de ejemplo, pero puedes borrarlos y poner los tuyos; hace falta al menos uno). En "Ronda actual" se introduce la puntuación de cada apartado para cada pareja; se suman solas para dar el total, y gana quien más sume (sin empates, igual que antes). Puedes añadir o quitar apartados más tarde, a mitad de torneo, desde la pestaña "Datos" — el cambio solo afecta a las rondas que aún no hayas guardado, las ya jugadas conservan su propio desglose.
    - **BP:** se introduce la puntuación de cada orador de la pareja (Orador 1 y Orador 2), un número entre 50 y 100 cada uno — el propio formulario no deja meter nada fuera de ese rango. Se suman los dos oradores para dar el total de la pareja, y ese total marca el orden 1º–4º de la sala.
  - **Número de parejas (paso 3):** si el formato es BP y el número no es múltiplo de 4, la propia pantalla avisa de cuántas parejas **Swing** (Swing 1, Swing 2...) se añadirán automáticamente para completar las salas — así nunca hay descansos por descuadre en BP, en vez de eso juegan parejas de relleno que no compiten por el trofeo.
  - **Nombres (paso 4):** solo el número (se llaman "Pareja 1", "Pareja 2"...), añadiéndolas una a una (con un contador que avisa cuándo ya se ha llegado al número indicado en el paso 3), o importando un archivo `.txt` o `.pdf` con un nombre por línea (vista previa editable antes de confirmar).
  - **Salas/aulas (paso 5):** opcional. Puedes ponerle nombre real a cada sala (p.ej. "Aula 1 - A1"); las que falten (o todas, si no añades ninguna) se numeran solas como "Sala 1", "Sala 2"...
  - **Jueces (paso 6):** opcional. Se añaden uno a uno, marcando si son trainee, y con su email (obligatorio). En cuanto añades un juez le llega automáticamente por correo su enlace personal — el mismo durante todo el torneo, así no hace falta generarle uno nuevo cada ronda. Si no añades ninguno, puedes hacerlo luego desde la pestaña Jueces (también con email obligatorio, y con el mismo envío automático).
- **Pestaña Draw**, pensada para proyectar en pantalla: una tabla grande y limpia con la sala, las parejas en columnas según su posición (Favor/Contra, u OG/OO/CG/CO en BP) y, si has añadido jueces, la columna de jueces de cada sala (el primero es el juez principal, marcado con Ⓒ; los trainees se marcan con Ⓣ). Tiene un botón de pantalla completa. Si no has generado aún los emparejamientos de la ronda, te deja generarlos ahí mismo.
- Los jueces se reparten solos entre las salas al generar cada ronda: si hay al menos tantos jueces como salas, cada sala tiene un juez principal (repartido intentando que nadie presida muchas más veces que el resto, y evitando que un trainee presida si hay alguien más disponible); los jueces que sobran se añaden como jueces adicionales, también repartidos de forma equilibrada. Si hay menos jueces que salas, alguna se queda sin asignar (se ve como "Sin asignar" en el Draw).
- Las pestañas **Parejas**, **Salas** y **Jueces** permiten corregir nombres, añadir salas o jueces nuevos, o quitarlos, en cualquier momento del torneo sin perder resultados.
- Genera los emparejamientos de cada ronda: empareja/agrupa por clasificación (puntos de equipo → puntos de ítem), evita repetir rivales cuando es posible (formato académico), y reparte los roles/posiciones equilibrando quién los ha ocupado menos veces.
- Introduce los puntos de cada enfrentamiento (por apartados en académico, por orador en BP, ver "Puntuación" arriba; no se permiten empates en el total, igual que el original) y calcula el ganador o el ranking 1º–4º automáticamente, con la suma en vivo mientras vas rellenando. La pestaña "Ronda actual" (donde se introducen los puntos) muestra el mismo nombre de sala y los mismos jueces que el Draw.
- Lleva la clasificación (con columnas según el formato elegido), el historial de rondas (con sala, jueces y el desglose de puntos de cada enfrentamiento) y un resumen del torneo. Las parejas Swing aparecen marcadas con una etiqueta y no cuentan para el "líder actual" del resumen.
- En formato académico, si el número de parejas es impar, sigue señalando quién descansa esa ronda (ahí no se usan parejas Swing, solo en BP).
- Guarda el torneo automáticamente en el navegador (localStorage) para que si se recarga la página no se pierda nada.
- Permite descargar en cualquier momento una copia de seguridad (`.json`, para recuperar el torneo exacto) y un informe de resultados (`.txt`, legible, con sala y jueces de cada enfrentamiento, y las parejas Swing marcadas).
- Permite cargar una copia `.json` guardada antes, por si se cambia de ordenador o de navegador (enlace visible ya en el primer paso del asistente).
- La lectura de PDF funciona sin conexión a internet (la librería va incrustada en el propio archivo), pero si el PDF tiene un formato muy elaborado (columnas, tablas) puede no salir perfecto — por eso siempre hay una vista previa editable antes de crear el torneo.
- **(Opcional) Envío de puntuaciones por parte de los jueces, con enlace personal y persistente.** Si activas Firebase y EmailJS (ver la sección de más abajo, ya están activados en este `index.html`), cada juez tiene **un único enlace para todo el torneo** — se genera al añadirlo y se le envía automáticamente por correo (no hay que generar ni reenviar nada ronda a ronda). Ese enlace abre una vista solo para él, sin navegación ni datos del resto del torneo, con dos pestañas: **"Mi turno actual"**, que muestra la sala y ronda que le toca ahora mismo (o un aviso si esa ronda no le toca juzgar), y **"Draw"**, la misma tabla que se proyecta en pantalla. Dentro de cada sala solo hay **un juez principal (el primero asignado, el mismo que se ve marcado con Ⓒ en el Draw)**: solo él ve el formulario de puntuación y puede enviarla (con los mismos apartados/oradores y límites que tengas configurados); el resto de jueces de esa sala ven un aviso pidiéndoles que le compartan su valoración a él. En cuanto el juez principal envía, a central le aparece "✓ Recibido" en "Ronda actual" y los números se rellenan solos; tú sigues teniendo la última palabra: revisas y pulsas "Guardar resultados" igual que siempre. También puedes copiar el enlace del juez principal a mano en cualquier momento con el botón "Copiar enlace del juez principal" en "Ronda actual". Si un juez no tiene el enlace, no tiene email, o falla la conexión, simplemente metes los puntos a mano como se ha hecho siempre — nada de esto es obligatorio.

## Cómo publicarlo en GitHub Pages

1. Crea un repositorio nuevo en GitHub (puede llamarse `cececat` o como prefieras). Puede ser público o privado — si es privado, GitHub Pages necesita un plan que lo permita; si no estás segura, hazlo público, no hay datos sensibles en el código, solo el propio programa.
2. Sube este archivo `index.html` a la raíz del repositorio (arrastrándolo en la web de GitHub, o con `git`):

   ```bash
   cd cececat
   git init
   git add index.html README.md
   git commit -m "CeceCat: gestor del Trofeo Rector de Comillas"
   git branch -M main
   git remote add origin https://github.com/TU_USUARIO/cececat.git
   git push -u origin main
   ```

3. En GitHub, ve a **Settings → Pages**.
4. En "Build and deployment", elige **Deploy from a branch**, rama `main`, carpeta `/ (root)`. Guarda.
5. En un par de minutos la página estará disponible en:

   ```
   https://TU_USUARIO.github.io/cececat/
   ```

6. Comparte ese enlace con tu profesor. Puede usarlo directamente desde el navegador, sin instalar nada.

## Envío de puntuaciones por parte de los jueces

Ya está activado, usando tu proyecto Firebase gratuito **"CeceCat"** (`cececat-d3ae2`, plan Spark — $0/mes) y tu cuenta de **EmailJS** (plan gratuito — 200 emails/mes). No tienes que hacer nada más — en cuanto publiques `index.html` en GitHub Pages, cada juez que añadas recibe automáticamente su enlace personal por email, y ya puede usarlo durante todo el torneo.

### Firestore

Firestore está creado (Standard edition, región `eur3`, Europa). Las reglas publicadas en Firebase → Firestore Database → Reglas son estas:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /cececat_draws/{tournamentToken} {
      allow read: if true;
      allow write: if true;
    }
    match /cececat_judgerooms/{judgeToken} {
      allow read: if true;
      allow create: if true;
      allow update: if resource.data.status == 'pending'
        || request.resource.data.roundNumber != resource.data.roundNumber;
    }
  }
}
```

Hay dos colecciones: `cececat_draws` guarda el Draw completo de cada torneo (para que la pestaña "Draw" de cada juez lo pueda leer sin ver el resto de datos del torneo), y `cececat_judgerooms` guarda, por cada juez (`judgeToken`, el código largo y aleatorio de su enlace personal), la sala/ronda que le toca ahora y su puntuación cuando la envía. Solo el documento de un juez puede quedar bloqueado tras enviarse (mientras su ronda actual no cambie); en cuanto le toca una ronda nueva, su documento vuelve a aceptar un envío. **Nota de seguridad:** estas reglas son deliberadamente simples y abiertas — no hay usuarios ni contraseñas, la única "llave" es el propio enlace de cada juez (difícil de adivinar). Es un nivel de seguridad razonable para un torneo académico interno, pero no subas nada más sensible a esta base de datos.

### EmailJS

El envío automático del enlace usa tu cuenta de EmailJS, conectada a tu Gmail (`claudialbombin@gmail.com`) como servicio de envío, con una plantilla ("Judge Link Notification") que usa las variables `to_email`, `to_name`, `tournament_name` y `judge_link`. Los tres valores ya están puestos en `index.html` (busca `const EMAILJS_CONFIG = {` cerca del principio del `<script>`): tu Public Key, el Service ID de Gmail y el Template ID. El plan gratuito de EmailJS permite 200 emails al mes — de sobra para un torneo, pero si alguna vez lo agotas, EmailJS avisa por email y los jueces sin email enviado pueden seguir usando el botón "Copiar enlace del juez principal" a mano.

Antes del torneo conviene probarlo: crea un torneo de prueba con un juez con tu propio email, comprueba que te llega el correo con el enlace, ábrelo en tu móvil (o en modo incógnito) y comprueba que el envío de puntuación llega a central en segundos.

Si alguna vez quieres desactivar solo el envío automático de emails (Firestore seguiría funcionando, y podrías seguir copiando el enlace a mano), basta con volver a poner `publicKey: "TU_PUBLIC_KEY"` en `EMAILJS_CONFIG`. Si quieres desactivar todo el envío remoto de puntuaciones, vuelve a poner `apiKey: "TU_API_KEY"` en `const FIREBASE_CONFIG = {` — el resto de CeceCat sigue funcionando igual, todo a mano.

Si prefieres usar tus propios proyectos en vez de estos: en Firebase, crea uno en [console.firebase.google.com](https://console.firebase.google.com), activa Firestore Database (modo producción), añade una app web desde Configuración del proyecto → General → "Tus apps" (icono `</>`), copia su `firebaseConfig` sobre los 6 valores de `FIREBASE_CONFIG` en `index.html`, y pega las reglas de arriba en su Firestore → Reglas. En EmailJS, crea una cuenta gratuita en [emailjs.com](https://www.emailjs.com), conecta un servicio de email (Gmail u otro), crea una plantilla con las cuatro variables `to_email`, `to_name`, `tournament_name` y `judge_link` (usa `{{to_email}}` como "To Email" de la plantilla), y copia tu Public Key (Account → General) y los IDs de servicio/plantilla sobre `EMAILJS_CONFIG` en `index.html`.

## Durante el torneo — cosas a tener en cuenta

- Los datos se guardan **en el navegador que se esté usando**. Si tu profesor va a manejar el torneo, que lo haga siempre desde el mismo ordenador/navegador, o que descargue la copia de seguridad (`.json`) al terminar cada ronda desde la pestaña "Datos y copia de seguridad" para poder continuar desde otro sitio si hace falta.
- Conviene descargar esa copia de seguridad tras cada ronda por si se borra el historial del navegador.
- Los nombres de las parejas se pueden editar en cualquier momento desde la pestaña "Parejas", sin perder resultados ya guardados.
- Para empezar un torneo nuevo desde cero hay un botón en "Datos y copia de seguridad → Zona de peligro" (borra el actual, así que conviene exportar antes si se quiere conservar).
- Si usas los enlaces de jueces, cada juez tiene un enlace único y persistente para todo el torneo (se lo envías, o se lo reenvías, una sola vez) — al generar los emparejamientos de cada ronda nueva, su enlace muestra solos la sala y el turno que le toque en cada momento, sin necesidad de generar ni reenviar nada.

## Diferencias con el script original (`tabby_memoria.py`)

- "Equipos" pasa a llamarse "Parejas" en toda la interfaz.
- Es una interfaz visual en el navegador en vez de un menú de terminal.
- El guardado en disco (`.txt` / `.json`) se sustituye por guardado automático en el navegador + botones de descarga manual, porque una página estática no puede escribir archivos en el ordenador por sí sola.
- Se añaden dos formatos (el original solo tenía el equivalente a "Académico"), tres formas de dar de alta a las parejas, un asistente guiado paso a paso, las parejas Swing en BP, salas/aulas con nombre real, jueces, y la pestaña Draw para proyectar.
- En modo BP, para mantener el sistema "reducido y propio" que pediste, el emparejamiento agrupa las salas simplemente por orden de clasificación (bloques de 4), sin el sistema de pull-up/pull-down de Tabbycat ni evitar rivales repetidos entre salas — sí se equilibra, en cambio, qué posición (OG/OO/CG/CO) ha ocupado menos veces cada pareja.
- Las parejas Swing se calculan una sola vez, al crear el torneo (según el número real de parejas que introduzcas), y se mantienen fijas toda la competición — no se van añadiendo o quitando ronda a ronda.
- El reparto de jueces también es una versión simplificada: no tiene en cuenta experiencia, conflictos de interés ni historial de qué parejas ha visto cada juez — solo intenta que nadie presida ni sea asignado muchas más veces que el resto.
- Cada sala mantiene el mismo nombre en todas las rondas (la sala en la posición 1 de la clasificación siempre usa el primer nombre de sala que pusiste, y así sucesivamente) — no se sortean las aulas entre rondas.
- La lógica de emparejamientos, asignación de roles y cálculo de clasificación es una traducción fiel del script original a JavaScript (verificada con pruebas automáticas para número par e impar de parejas, en ambos formatos).
