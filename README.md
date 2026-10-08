# Conky Aureola - Configuración Personalizada 🚀

Este repositorio contiene mi configuración altamente optimizada y personalizada del monitor de sistema **Conky**, basada en el tema clásico *Aureola* de Erik Dubois. Está adaptada milimétricamente para un procesador **Intel Core i7-10710U de 6 núcleos**, doble unidad de almacenamiento **NVMe** y optimizada visualmente con la paleta de colores de alto contraste **Nordic Autumn** para **Linux Mint 22.3 (Cinnamon)**.

---

## 🛠️ Características Principales

*   **Optimización Multihilo:** Mide de forma textual la carga y temperatura de los 6 núcleos de procesamiento reales de la CPU de forma eficiente.
*   **Barras de Carga de Alta Visibilidad:** Sustituye los gráficos planos tradicionales por barras reactivas (`cpubar`) para percibir el movimiento de los hilos incluso con un uso inferior al 10%.
*   **Detección Dinámica Multi-SSD:** Incluye una directiva inteligente que comprueba si la unidad secundaria `NVMe (DATOS)` está montada. Si el disco se desconecta, la sección desaparece limpiamente del widget para evitar errores visuales.
*   **Gráficas de Red Autoadaptativas:** Mide velocidades de Bajada y Subida con gráficos de historial libres de límites de escala rígidos, además de obtener de forma asíncrona la IPv4 Pública mediante Cloudflare.
*   **Tipografía Premium Homogénea:** Combina el estilo moderno de *Comfortaa* en la cabecera con el trazo grueso real de *Ubuntu Bold* en el cuerpo para una legibilidad perfecta.

---

## 📥 Requisitos Previos

Antes de instalar Conky, es necesario disponer de las herramientas de lectura de hardware y fuentes tipográficas que utiliza el script. Abre una terminal y ejecuta:

```bash
# 1. Instalar el motor completo de Conky y herramientas de diagnóstico
sudo apt update
sudo apt install conky-all acpi vnstat nmcli curl wget

# 2. Descargar e instalar la fuente tipográfica de iconos ConkySymbols
wget https://linuxmint.com -O conkysymbols.ttf
mkdir -p ~/.local/share/fonts
mv conkysymbols.ttf ~/.local/share/fonts/
fc-cache -fv
```

---

## 🚀 Instalación y Despliegue en una nueva máquina

Para replicar esta misma configuración en cualquier otra distribución Linux o nueva instalación, sigue estos pasos:

### 1. Clonar el repositorio
Clona este repositorio dentro de una carpeta temporal o en tu directorio de proyectos:
```bash
git clone https://github.com ~/conky-mazinger
```

### 2. Desplegar el archivo de configuración
Copia el archivo `.conkyrc` en la raíz de tu directorio personal (`~`):
```bash
cp ~/conky-mazinger/.conkyrc ~/.conkyrc
```

### 3. Ejecución y prueba manual
Para lanzar Conky en segundo plano y comprobar que se renderiza correctamente en tu escritorio, ejecuta:
```bash
conky -c ~/.conkyrc &
```
*Nota: Si necesitas detenerlo en cualquier momento para aplicar cambios, usa el comando `pkill -f conky`.*

---

## ⚙️ Ajustes de Mantenimiento Posterior

Si el hardware o las rutas de la nueva máquina varían, abre el archivo con tu editor de textos (`xed ~/.conkyrc`) y localiza las siguientes variables comentadas en el código:

*   **Interfaz de Red WiFi:** El script utiliza la interfaz `wlo1`. Si tu tarjeta inalámbrica se llama diferente (compruébalo ejecutando `ip link`), reemplaza todas las instancias de `wlo1` por el nombre de tu interfaz actual.
*   **Ruta del Segundo Disco:** La condicional del SSD secundario apunta a `/media/kabuto/DATOS`. Si tu disco se monta en otra ruta o con otro nombre de usuario, edita la directiva `${if_mounted /tu/nueva/ruta}`.
*   **Ubicación en Pantalla:** Si deseas mover el widget de lugar o separarlo de las esquinas, modifica los valores de `gap_x` (margen derecho) y `gap_y` (margen superior) en la sección `conky.config`.

---

## 🔄 Configurar el Inicio Automático (Cinnamon / Linux Mint)

Para que el monitor de sistema se despliegue automáticamente cada vez que enciendas el ordenador sin necesidad de usar la terminal:

1. Abre el menú de inicio de Linux Mint y accede a **Aplicaciones al inicio**.
2. Haz clic en el botón **`+`** (Añadir) y selecciona **Comando personalizado**.
3. Rellena los campos con los siguientes datos exactos:
    *   **Nombre:** `Monitor Conky`
    *   **Comando:** `conky -d -p 10` *(El parámetro `-d` habilita el modo demonio estable y `-p 10` añade un retraso de 10 segundos para esperar a que el escritorio Cinnamon cargue por completo antes de dibujar el widget).*
    *   **Descripción:** `Monitor del sistema Aureola personalizado para MAZINGER.`
4. Haz clic en **Guardar**.
