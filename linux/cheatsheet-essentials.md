# 🐧 Linux Essentials - Guía de Estudio

## 1. Rutas y Navegación
En Linux, todo cuelga de una única raíz representada por la barra inclinada `/`. No existen discos C: ni D:.
- **Ruta Absoluta:** Siempre empieza por `/` (ej. `/var/log/syslog`). Es como dar una dirección completa desde el principio.
- **Ruta Relativa:** Empieza desde donde estás parado (ej. `./backups` o `../etc`).
  - `.` = carpeta actual.
  - `..` = carpeta padre (un nivel arriba).
  - `~` = tu carpeta personal (`/home/tu_usuario`).

**Comandos clave:**
- `pwd`: Muestra la ruta absoluta de donde estás.
- `cd -`: Vuelve a la carpeta donde estabas hace un segundo (como el botón "Atrás").
- `pushd` y `popd`: Usan una "pila" (stack) de rutas. `pushd` te mueve a una carpeta y guarda la actual en memoria. `popd` te devuelve a la guardada.

## 2. Visualización de Archivos
No todos los archivos se leen igual:
- **`cat`**: Vuelca todo el texto a la pantalla. Úsalo solo para archivos cortos. `tac` lo muestra al revés (de la última línea a la primera).
- **`less`**: El paginador profesional. Para archivos enormes (como logs), te permite bajar, subir, y buscar.
  - *Nota DevOps:* Pulsa `/` para buscar hacia adelante y `?` para buscar hacia atrás. Pulsa `q` para salir. 
- **`head -n X` / `tail -n X`**: Muestran las primeras/últimas X líneas.
  - *Nota DevOps:* `tail -f archivo` es vital. Se queda "escuchando" el archivo y te muestra en tiempo real cómo se escriben nuevas líneas (perfecto para ver logs de servidores).

## 3. Enlaces Duros (Hard Links) y Blandos (Soft Links)
- **Enlace Duro (`ln original enlace`)**: Crea otro nombre para el mismo archivo físico. Comparten el mismo "inodo" (el número de identidad en el disco). Si borras uno, el archivo sigue vivo por el otro.
- **Enlace Blando/Simbólico (`ln -s original enlace`)**: Es un "acceso directo" (como en Windows). Es un archivo independiente que apunta a la ruta del original. Si borras el original, el enlace blando se rompe (queda huérfano).

## 4. Búsqueda de Archivos
- **`which comando`**: Te dice dónde está el ejecutable de un comando (ej. `which python3`).
- **`whereis comando`**: Te dice dónde está el ejecutable, el código fuente y el manual.
- **`locate`**: Busca en una base de datos preconstruida. Es instantáneo, pero puede no tener los archivos más recientes.
- **`find ruta -opciones`**: Busca en el disco duro en tiempo real. Es más lento pero infalible.
  - `find . -name "*.log"` (Por nombre).
  - `find . -size +100M` (Archivos de más de 100 MB).
  - `find . -mtime -1` (Modificados en el último día).
  - *Comodines:* `*` (cualquier letra), `?` (un solo carácter), `[abc]` (cualquiera de esas 3).

## 5. Flujos de Datos y Redirecciones (Streams)
En Linux, todo comando tiene 3 canales (streams):
1. **stdin (0)**: Entrada estándar (tu teclado).
2. **stdout (1)**: Salida estándar (los resultados correctos en pantalla).
3. **stderr (2)**: Error estándar (los mensajes de error).

**Operadores:**
- `>`: Redirige stdout a un archivo (borra el contenido anterior).
- `>>`: Redirige stdout a un archivo (añade al final).
- `2>`: Redirige los errores a un archivo.
- `|` **(Pipe/Tubería)**: Toma la salida (stdout) de un comando y la usa como entrada (stdin) del siguiente. Ej: `ls -l | grep ".txt"` (lista archivos y luego filtra los .txt).

## 6. Gestión de Paquetes (El App Store de Linux)
Los sistemas basados en RedHat (CentOS/Fedora) usan `rpm` (bajo nivel) y `dnf` (alto nivel). Los basados en Debian (Ubuntu) usan `dpkg` (bajo nivel) y `apt` (alto nivel).

**Comandos de alto nivel (los que usarás a diario):**
- `apt update`: Actualiza la lista de repositorios (el catálogo).
- `apt upgrade`: Instala las actualizaciones de los paquetes instalados.
- `apt install <paquete>`: Descarga e instala el paquete con sus dependencias.
- `apt remove <paquete>`: Desinstala el paquete (conserva configuraciones).
- `apt autoremove`: Limpia dependencias huérfanas que ya no se necesitan.

## 7. Apagado y Reinicio
- **`halt`**: Detiene la CPU (modo de bajo consumo), pero no corta la electricidad.
- **`poweroff`**: Apaga el sistema por completo.
- **`reboot`**: Reinicia.
- **`shutdown -h +10`**: Programa el apagado en 10 minutos.
- **`shutdown -r now`**: Reinicia inmediatamente.
- **`shutdown -c`**: Cancela un apagado que estaba programado.
