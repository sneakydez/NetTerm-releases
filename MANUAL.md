# Manual de NetTerm

NetTerm es un cliente de terminal para Windows para conectarse a routers, switches, servidores y
Raspberry Pi por **SSH, Telnet, SFTP y FTP**, con botones que envían comandos o contraseñas con un clic.

## 1. Instalar y abrir

1. Descarga `NetTerm.exe` desde https://github.com/sneakydez/NetTerm-releases/releases/latest
2. Guárdalo donde quieras (Escritorio, `Documentos\NetTerm`…). **No necesita instalación.**
3. Ábrelo con doble clic.
4. Si Windows muestra **«Windows protegió su PC»**, pulsa **Más información → Ejecutar de todas formas**.
   Aparece porque el programa aún no está firmado digitalmente; no es un virus.

La primera vez tarda unos segundos en abrir mientras Windows lo analiza.

## 2. Primeros pasos

1. Pulsa **＋ Nueva sesión**.
2. Elige el protocolo (**SSH**, **Telnet**, **SFTP** o **FTP**). El puerto se rellena solo.
3. Escribe un **nombre**, el **host** (IP o nombre) y, si quieres, **usuario** y **contraseña**.
4. Pulsa **Guardar y conectar**.

Para conectar más tarde: **doble clic** sobre la sesión en el panel de la izquierda.

## 3. La pantalla

| Zona | Para qué sirve |
|---|---|
| Panel de sesiones (izquierda) | Tus sesiones guardadas, agrupadas y con buscador |
| `☰` (arriba a la izquierda) | Mostrar u ocultar el panel de sesiones (`Ctrl+B`) |
| Pestañas | Una por conexión. El punto indica el estado: verde conectado, amarillo conectando, rojo desconectado. **Arrástralas** para cambiar el orden (`Ctrl+Tab` sigue ese orden) |
| `🔍` | Buscar y filtrar en la terminal (`Ctrl+Shift+F`) |
| `📡` | Multienvío: escribir en varias sesiones a la vez |
| `▥` | Pantalla dividida: ver 1, 2 o 4 terminales |
| `⚙` | Preferencias (`Ctrl+,`) |
| `?` | Este manual (`F1`) |
| Barra de botones | Tus botones de comandos y contraseñas |
| Barra inferior | Sesión activa, usuario, host y estado; versión de NetTerm |

## 4. Sesiones

- **Grupos:** escribe un grupo al crear la sesión (por ejemplo «Oficina central») y aparecerán agrupadas.
- **Buscar:** escribe en «Buscar sesión…» parte del nombre, la IP o el grupo.
- **Editar, duplicar o borrar:** clic derecho sobre la sesión, o el lápiz ✎ al pasar el ratón.
- **Tema por sesión:** en el formulario de la sesión, elige un tema propio. Por ejemplo, «Producción (rojo)» para
  los equipos críticos, así no te equivocas de ventana.
- **Clave privada SSH:** en el formulario, «Clave privada» → «Examinar…».

### Si la contraseña es incorrecta

NetTerm te pide la contraseña en la propia terminal (no se ve lo que escribes). Escríbela y pulsa `Enter`.
Si funciona, aparece un aviso para **guardarla** en la sesión. `Esc` cancela.

> Tras varios intentos fallidos, muchos servidores (OpenSSH, routers) **bloquean tu IP unos minutos**.
> Si ves «El servidor cortó la conexión», espera y vuelve a intentarlo.

### Reconectar

Si una sesión se cae, pulsa `Enter` en su pestaña, o clic derecho en la pestaña → **Reconectar**.

## 5. Trabajar en la terminal

- **Copiar:** sombrea el texto con el ratón; se copia solo. También `Ctrl+Shift+C`.
- **Pegar:** clic derecho, `Ctrl+Shift+V` o `Ctrl+V`. Si el texto tiene **varias líneas**, NetTerm te muestra
  antes la configuración completa, con números de línea, y te pregunta si quieres pegarla (como MobaXterm): cada
  línea se ejecuta como un comando. Se ajusta en Preferencias → Terminal → «Preguntar antes de pegar».
- **Menú contextual:** `Ctrl` + clic derecho (o configúralo para que el clic derecho abra siempre el menú, ver
  Preferencias → Terminal). Opciones: Copiar, Pegar, **Resaltar** la palabra, Seleccionar todo, Limpiar pantalla.
- `Ctrl+C`, `Ctrl+Z`, `Tab`, flechas… funcionan como en cualquier terminal.
- Clic derecho en una **pestaña**: Reconectar, Abrir log, Limpiar pantalla, Cerrar.

### Buscar y filtrar en la terminal

Pulsa `🔍` o `Ctrl+Shift+F` (si tienes texto sombreado, lo busca directamente).

- **Buscar:** escribe la palabra. Todas las coincidencias se marcan en amarillo y la actual en naranja; el
  contador indica «3 de 27». `Enter` va a la siguiente, `Mayús+Enter` a la anterior, `Esc` cierra.
- **Opciones:** `Aa` distingue mayúsculas, `ab` solo palabras completas y `.*` usa una expresión regular
  (por ejemplo `et-0/0/[0-3] +up +down` para ver las interfaces caídas).
- **Filtrar líneas:** muestra **solo las líneas que contienen la palabra**, como un `| include`, pero sobre lo que
  ya tienes en pantalla, sin volver a lanzar el comando. Ideal para revisar una configuración larga.
  - **Con la palabra / Sin la palabra:** incluir o excluir (como `| exclude`).
  - **Contexto:** muestra además 1, 3 o 5 líneas alrededor de cada coincidencia (en gris).
  - Haz clic en una línea para ir a ella en la terminal. **Copiar** copia el resultado; **Actualizar** vuelve a
    leer la terminal si ha llegado salida nueva.

`Ctrl+F` sin `Mayús` no se usa para buscar porque la CLI de los equipos lo usa para mover el cursor.

### SFTP y FTP

Las sesiones SFTP/FTP abren una consola de archivos. Escribe `help` para ver los comandos:

| Comando | Qué hace |
|---|---|
| `ls [ruta]` | Listar el directorio remoto |
| `cd <ruta>` / `pwd` | Cambiar de directorio / ver dónde estás |
| `get <remoto> [local]` | Descargar (por defecto a tu carpeta Descargas) |
| `put <local> [remoto]` | Subir un archivo |
| `mkdir`, `rmdir`, `rm`, `mv` | Crear, borrar, renombrar |
| `lcd`, `lls`, `lpwd` | Carpeta local |

## 6. Botones personalizados

Pulsa **＋ Botón** en la barra de botones.

- **Comandos:** una o varias líneas; se envían en orden con el retardo que elijas (útil para
  `terminal length 0` + `show running-config`).
- **Contraseña:** envía una contraseña guardada (por ejemplo la de `enable`) sin que se vea nunca en pantalla.
- **Pulsar Enter al final:** márcalo para que se ejecute directamente.
- **Atajo de teclado:** haz clic en el campo «Atajo» y pulsa la combinación (`Ctrl+Alt+1`, `F5`, `Ctrl+→`…).
  `Ctrl`+letra no se permite porque la terminal la necesita (`Ctrl+C`, `Ctrl+D`…). Las flechas, Inicio, Fin,
  RePág, AvPág e Insert necesitan `Ctrl` o `Alt`. `Supr` quita el atajo.
- **Color:** para distinguirlos de un vistazo.

Clic derecho sobre un botón para **editarlo, moverlo o borrarlo**. El botón se aplica a la pestaña activa
(o a todas las marcadas si el multienvío está activo).

### Editor de teclas

Para asignar textos a teclas sin crear botones (como el «Keymap Editor» de SecureCRT):
**Preferencias → Teclas**.

1. Elige los modificadores (`Ctrl`, `Alt`, `Mayús`) y haz clic en una tecla del teclado en pantalla. También
   puedes hacer clic en el teclado y pulsar la combinación real.
2. Escribe el texto que debe enviar, por ejemplo `show interfaces diagnostics optics et-0/0/0`. Puede tener
   varias líneas.
3. Marca «Pulsar Enter al final» si quieres que se ejecute directamente, y pulsa **Asignar**.

Colores del teclado: azul = asignada; verde = atajo de un botón; raya azul = asignada con otros modificadores;
atenuada = la usa NetTerm. Abajo tienes la lista de teclas asignadas para editarlas o quitarlas.

## 7. Pantalla dividida

Pulsa `▥` y elige:

| Diseño | Atajo |
|---|---|
| Una terminal | `Ctrl+Shift+1` |
| Dos, lado a lado | `Ctrl+Shift+2` |
| Dos, arriba y abajo | `Ctrl+Shift+3` |
| Cuatro | `Ctrl+Shift+4` |

- El panel seleccionado tiene un **borde azul**. Haz clic en un panel para seleccionarlo.
- Haz clic en una **pestaña** para mostrarla en el panel seleccionado (o en un hueco libre).
- Cada panel muestra arriba el nombre y el estado de la sesión.

## 8. Multienvío (escribir en varias sesiones a la vez)

1. Abre las sesiones (por ejemplo, todos los switches de una planta).
2. Pulsa `📡` (o `Ctrl+Shift+M`). Aparece una **barra naranja** y todas las sesiones SSH/Telnet quedan marcadas ☑.
3. Desmarca las que no quieras con el ☑ de su pestaña («Marcar todas» / «Ninguna» en la barra naranja).
4. Escribe en cualquier sesión marcada: **lo que tecleas llega a todas las marcadas**. Los botones también.
5. Pulsa **Desactivar** (o `📡` otra vez) al terminar.

> ⚠ Ten cuidado con los cambios de configuración: se aplican a todas las sesiones marcadas a la vez.
> Combínalo con la pantalla dividida para ver qué responde cada equipo.

## 9. Resaltado de palabras

Los routers y switches no envían colores, así que NetTerm los añade. Por defecto:

| Qué | Color |
|---|---|
| `up`, `active`, `connected`, `established`… | Verde negrita |
| `down`, `err-disabled`, `failed`, `error`… | Rojo negrita |
| `administratively down`, `admin-down`, `%Warning`… | Naranja |
| Direcciones IPv4 e IPv6 | Cian |
| Direcciones MAC (`0050.56c0.0001`, `aa:bb:cc:dd:ee:ff`) | Morado |
| Interfaces agregadas / trunk (`ae3`, `BE3.9`, `Port-channel10`, `Eth-Trunk0`…) | Dorado negrita |
| Interfaces de 100G y 400G (`et-0/0/0`, `Hu0/0/0/1`, `HundredGigE…`, `100GE…`) | Rosa |
| Interfaces de 10G (`xe-0/1/4`, `TenGigE…`, `Te1/1/1`, `XGigabitEthernet…`) | Turquesa |
| El resto de interfaces (`ge-0/0/1`, `Gi0/1`, `lo0`…) | Azul |

**Resaltar una palabra al momento:** clic derecho sobre la palabra en la terminal (o `Ctrl`+clic derecho) →
**🎨 Resaltar**. Elige una plantilla o crea una nueva. Se aplica a lo que llegue a partir de ese momento.

**Preferencias → Resaltado:**

- **Plantillas de estilo:** color del texto, fondo (∅ = sin fondo), **B** negrita, *I* cursiva, U subrayado.
- **Reglas:** a qué se aplica cada plantilla.
  - *Palabras:* palabras exactas separadas por comas (`up, active, connected`). `UP` no colorea `BACKUP`.
  - *Contiene:* como Palabras, pero también dentro de otras palabras: `MPLS` colorea `MPLS_VPN_SLAES`.
  - *Patrón:* IPv4, IPv6, MAC o un **tipo de interfaz**: trunks/agregadas, 100G-400G, 40G-25G, 10G, 1G,
    gestión/lógicas, o cualquier interfaz. Así puedes poner cada tipo del color que quieras.
  - *Regex:* expresión regular (por ejemplo `VLAN\d+`). Si está mal escrita, el campo se pone en rojo.
  - `Aa` = ignorar mayúsculas. `▲▼` = prioridad: si dos reglas coinciden, gana la de arriba.
- **Restaurar** vuelve a las reglas predeterminadas.

## 10. Preferencias (`⚙` o `Ctrl+,`)

Los cambios se guardan solos.

- **Terminal:** 13 temas, tipo y tamaño de letra, interlineado, grosor, cursor, colores propios,
  historial en pantalla, comportamiento del clic derecho, aviso al pegar y **preguntar antes de cerrar NetTerm**
  (por defecto, si hay sesiones abiertas; para que no se cierre por accidente). Si la sesión abierta tiene tema
  propio, eliges si el tema se aplica a «Todas las sesiones» o «Solo esta».
- **Diseño:** botones arriba, abajo, izquierda o derecha; estilo y tamaño; panel de sesiones a la izquierda,
  derecha u oculto; lista, compacta o tarjetas.
- **Logs:** activar o desactivar y elegir la carpeta.
- **Resaltado:** ver el apartado 9.
- **Teclas:** editor de teclas (apartado 6).
- **Actualizaciones:** buscar actualizaciones al abrir y «Buscar actualizaciones ahora».

### Historial en pantalla

Cuántas líneas puedes subir con la rueda del ratón: de 1.000 a 1.000.000. Cada línea ocupa memoria
(con 1.000.000 de líneas, hasta ~1,5 GB **por pestaña**). Para guardar **todo sin límite**, usa los logs.

## 11. Logs de sesión

Con los logs activados (por defecto), cada conexión se guarda en un archivo de texto con la **fecha y hora en
cada línea**, por ejemplo `raspi_2026-10-23_18-30-00.log`.

- Carpeta por defecto: `Documentos\NetTerm Logs` (cámbiala en Preferencias → Logs).
- Abrir el log de una sesión: clic derecho en su pestaña → **Abrir log**.

## 12. Importar y exportar

Botón `⋯` junto a «Nueva sesión».

### Importar sesiones de otros programas

- **PuTTY** y **SecureCRT:** lee las sesiones guardadas en este PC (las carpetas de SecureCRT pasan a ser grupos).
  Estos programas no permiten leer sus contraseñas: NetTerm las pedirá al conectar.
- **Excel o CSV:** un archivo con una fila de cabecera. Columnas reconocidas: **Nombre, Host (o IP),
  Puerto, Protocolo, Usuario, Contraseña, Grupo**. Solo el host es obligatorio. «Descargar plantilla de
  Excel/CSV» te da un ejemplo.

Verás una lista para elegir cuáles importar. Las que ya tienes aparecen como «ya existe» y no se duplican.

### Compartir tu configuración con el equipo

- **Exportar configuración:** crea un archivo `.netterm` con sesiones, botones y/o preferencias.
  Las contraseñas **no se incluyen**, o van **cifradas con una contraseña** que tú eliges.
- **Importar configuración:** abre un `.netterm`. Si trae contraseñas cifradas, escribe la contraseña del archivo.
  Lo que ya tienes no se duplica. Las preferencias importadas reemplazan las tuyas (solo si lo marcas).

## 13. Actualizaciones

Al abrir, NetTerm comprueba si hay una versión nueva. Si la hay, verás las novedades y podrás elegir:

- **Actualizar ahora:** se descarga, se cierra, se reemplaza y se vuelve a abrir. Tus datos se conservan.
- **Más tarde** o **Omitir esta versión**.

Nunca se instala nada sin que lo aceptes.

## 14. Atajos de teclado

| Atajo | Acción |
|---|---|
| `Ctrl+Shift+N` | Nueva sesión |
| `Ctrl+Shift+W` | Cerrar pestaña |
| `Ctrl+Tab` / `Ctrl+Shift+Tab` | Pestaña siguiente / anterior |
| `Ctrl+B` | Mostrar u ocultar el panel de sesiones |
| `Ctrl+,` | Preferencias |
| `F1` | Este manual |
| `Ctrl+Shift+F` | Buscar y filtrar en la terminal |
| `Ctrl+Shift+1` … `4` | Pantalla dividida |
| `Ctrl+Shift+M` | Multienvío |
| `Ctrl+Shift+C` / `Ctrl+Shift+V` | Copiar / pegar |
| Los que tú asignes | Tus botones y el editor de teclas |

## 15. Tus datos y la seguridad

- Sesiones, contraseñas y botones se guardan **cifrados** en `%USERPROFILE%\.netterm`, protegidos con tu
  usuario de Windows: otra cuenta u otro PC no puede leerlos.
- Las preferencias están en `%USERPROFILE%\.netterm\settings.json`.
- NetTerm no envía tus datos a ningún servidor. Solo se conecta a tus equipos y, para buscar actualizaciones,
  a GitHub.

## 16. Problemas frecuentes

| Problema | Solución |
|---|---|
| «Windows protegió su PC» | Más información → Ejecutar de todas formas |
| «Usuario o contraseña incorrectos» | Escribe la contraseña en la terminal y guárdala si funciona. Revisa el teclado al crear la contraseña en el equipo (`@` frente a `2`) |
| «El servidor cortó la conexión» | Bloqueo temporal por intentos fallidos: espera unos minutos |
| «Conexión rechazada» | El puerto no está abierto o el servicio (SSH/Telnet) no está activo en el equipo |
| «Tiempo de espera agotado» | El equipo no responde: revisa la IP, la VPN o el cortafuegos |
| No veo el panel de sesiones | Pulsa `☰` o `Ctrl+B` |
| Las palabras no se colorean | Preferencias → Resaltado: comprueba que está activado. Solo afecta a lo que llega después |
| Un botón no hace nada | La sesión debe estar conectada (punto verde). Las contraseñas solo se envían a SSH/Telnet |
| El equipo recorta los comandos con `...` o descoloca las líneas | Desde la versión 1.4 NetTerm le comunica al equipo el ancho real de la ventana (SSH y Telnet). Si pasa con una versión anterior, actualiza |
