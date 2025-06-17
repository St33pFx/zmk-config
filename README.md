# ⌨️ ZMK Config - Corne Keyboard (Nice!OLED Edition)

Configuración personalizada para mi teclado dividido **Corne**, con soporte para pantalla OLED, modtap, macros, combos y RGB funcional.  
Incluye mejoras de productividad para programación, diseño y uso general.

---

## 📷 Vista de la distribución

![Distribución del teclado](assets/my_keymap.png)

📄 También puedes ver la versión editable en vector:  
[🔗 Ver SVG (my_keymap.svg)](assets/my_keymap.svg)

---

## 🔧 Cambios principales

### 🧩 Hardware
- **Teclado:** Corne (con Nice!Nano v2)
- **Pantalla:** Nice!OLED (instalada en el lado izquierdo)
- **RGB:** Activado con efecto `Swirl` y brillo inicial al 15%
- **Bluetooth:** Potencia TX mejorada (`CONFIG_BT_CTLR_TX_PWR_PLUS_8=y`)

---

## 🖥️ Pantalla OLED

- `CONFIG_ZMK_DISPLAY=y`
- `CONFIG_ZMK_DISPLAY_STATUS_SCREEN_CUSTOM=y`

En el lado **derecho**, para evitar errores de compilación (`multiple definition`):

```conf
CONFIG_ZMK_DISPLAY=n
```

### Widgets activos:
- Capa activa (`layer status`)
- Porcentaje de batería
- Conexión activa (BLE/USB)
- WPM (Words Per Minute)
- Luna (mascota animada, si está activada)

---

## ⌘ Modtap

Teclas que actúan como **modificador si se mantienen** y como **tecla normal si se tocan rápidamente**.

Ejemplos:

```dts
&mt LCTRL A     // A si la tocas, Ctrl si la mantienes
&mt LALT SPACE  // Space si la tocas, Alt si la mantienes
```

Parámetros importantes:

```conf
CONFIG_ZMK_HOLD_TAP_DELAY_MS=200
CONFIG_ZMK_HOLD_TAP_PER_KEY=y
```

---

## 🔀 Combos

Combinaciones de dos teclas que disparan otra tecla:

| Combo | Teclas combinadas | Resultado |
|-------|--------------------|-----------|
| `tab` | home row derecha   | Tabulador |
| `ctrl` | home row izquierda| Control   |
| `cmd` | fila inferior      | Cmd/GUI   |

Configurados con el editor visual de keymap.

---

## ⚙️ Macros

Automatización de combinaciones complejas.

Ejemplo útil:

- **Centrar texto en After Effects**:
  ```plaintext
  CTRL + ALT + SHIFT + HOME
  ```

Macro asignado a una tecla con `&macro_press`.

Otros macros: letras automáticas (`Z`, `M`, `K`) o comandos frecuentes.

---

## 🌈 RGB Underglow

- Activado:
  ```conf
  CONFIG_ZMK_RGB_UNDERGLOW=y
  ```
- Efecto:
  ```conf
  CONFIG_ZMK_RGB_UNDERGLOW_EFF_START=3  // Swirl
  ```
- Color inicial:
  ```conf
  CONFIG_ZMK_RGB_UNDERGLOW_HUE_START=240
  CONFIG_ZMK_RGB_UNDERGLOW_SAT_START=10
  CONFIG_ZMK_RGB_UNDERGLOW_BRT_START=15
  ```

---

## 🧪 Extras

- `CONFIG_ZMK_EXT_POWER=y`: apaga el OLED si no hay USB
- `CONFIG_ZMK_BLE_EXPERIMENTAL_CONN=y`: más estabilidad con Windows/iPad
- `CONFIG_ZMK_KSCAN_DEBOUNCE_PRESS_MS=1`: menor latencia en pulsación

---

## 🧼 Problemas resueltos

- ❌ `multiple definition of 'widget_layer_status'`  
  ✅ Solucionado desactivando `CONFIG_ZMK_DISPLAY` en el lado derecho (`corne_right`).

---

## 📁 Archivos incluidos

| Archivo | Descripción |
|--------|-------------|
| `assets/my_keymap.png` | Vista gráfica del layout |
| `assets/my_keymap.svg` | Versión vectorial editable del layout |

---

## 🧩 Herramientas utilizadas

- [keymap-editor (Nick Coutsos)](https://nickcoutsos.github.io/keymap-editor/) – Para crear combos/macros visualmente
- [zmk-nice-oled (M. Zeglinski fork)](https://github.com/mzeglinski/zmk-nice-oled) – Módulo con soporte para múltiples widgets
- [ZMK Firmware](https://zmk.dev/) – Firmware principal para teclados mecánicos inalámbricos

---

## ⚙️ Instrucciones básicas para compilar

```bash
# 1. Entra al directorio
cd zmk-config

# 2. Compila para el lado izquierdo
west build -s app -d build/left -b nice_nano_v2 -- -DSHIELD=corne_left

# 3. Flashea
nrfutil dfu usb-serial -pkg build/left/zephyr/zmk.uf2

# 4. Repite para el lado derecho, o desactiva OLED ahí:
west build -s app -d build/right -b nice_nano_v2 -- -DSHIELD=corne_right
```

---

## ✍️ Autor

Yahir Salazar  
Junio 2025  
[github.com/yahirsalazar](https://github.com/yahirsalazar)

---

## ❤️ Créditos y agradecimientos

- ZMK Community  
- Nick Coutsos (por el visual keymap editor)  
- M. Zeglinski (por el fork funcional de nice-oled)  
- Todos los contribuidores del ecosistema QMK/ZMK


---

## 🛠️ Instalación de Firmware ZMK

ZMK permite dos formas de compilar e instalar tu firmware: **localmente** o usando **GitHub Actions (online)**.

---

### 📡 Opción 1: Usar GitHub Actions (Recomendado)

ZMK ha sido diseñado para que puedas mantener tu configuración personal (keymap, widgets, macros, etc.) sin modificar el repositorio principal de ZMK.

#### 🧪 Ventajas:
- No necesitas instalar toolchains o entornos complejos.
- GitHub Actions compila tu firmware automáticamente en la nube.
- Puedes descargar los `.uf2` listos para flashear desde la pestaña **Actions** de tu repositorio.

#### 🪜 Pasos rápidos:
1. Crea un nuevo repo llamado `zmk-config` en GitHub (vacío, sin README).
2. Ejecuta el script oficial:

```bash
bash -c "$(curl -fsSL https://zmk.dev/setup.sh)"
```

3. Selecciona:
   - Tu teclado (ej. Corne)
   - Tu MCU (ej. nice!nano v2)
   - Tu usuario y repo en GitHub

4. El script:
   - Clonará el template
   - Configurará tu `shield` y `board`
   - Subirá tu configuración y activará GitHub Actions

5. Espera a que termine la compilación (Actions → última build → download firmware).
6. Flashea el `.uf2` en tu teclado.

---

### 💻 Opción 2: Compilación local

Requiere tener el entorno de compilación de Zephyr y ZMK instalado (Linux/Mac recomendado).

#### 🧪 Requisitos:
- Git
- Python 3
- Zephyr toolchain
- West

#### 🪜 Compilar localmente

```bash
# Clona ZMK y tu config
git clone https://github.com/zmkfirmware/zmk
git clone https://github.com/tu_usuario/zmk-config

# Entra al folder de configuración
cd zmk-config

# Compila lado izquierdo
west build -s zmk/app -d build/left -b nice_nano_v2 -- -DSHIELD=corne_left

# Compila lado derecho
west build -s zmk/app -d build/right -b nice_nano_v2 -- -DSHIELD=corne_right
```

---

### 🚀 Flasheo del firmware (.uf2)

1. Presiona dos veces el botón de reset en tu nice!nano para entrar en modo bootloader.
2. Tu computadora detectará un dispositivo tipo USB.
3. Copia el archivo `.uf2` que corresponde (ej. `corne_left.uf2`) al dispositivo USB.
4. Se flasheará y reiniciará automáticamente.

---

### 🔄 Teclado dividido (Split Keyboards)

- Solo el lado maestro (izquierdo por lo general) se conecta por USB o Bluetooth.
- El lado esclavo se conecta al maestro automáticamente tras el encendido si ya fueron pareados.
- Asegúrate de que ambos lados tengan batería o estén alimentados.

---

### 📶 Conexión Bluetooth

- Al encender, ZMK anunciará el dispositivo si no está emparejado.
- Usa tu celular, tablet o laptop para emparejarlo vía Bluetooth.
- ZMK soporta múltiples perfiles Bluetooth (multi-host switching).
- Revisa la documentación para conocer los atajos y comportamientos BLE.

---

### 🧯 Problemas comunes

- ⚠️ Si no se conectan los halves: verifica la energía y reinicia ambos al mismo tiempo.
- ⚠️ Si no aparece el dispositivo: revisa que esté en modo bootloader.
- ⚠️ Problemas con el pairing: borra el perfil en tu dispositivo y vuelve a emparejar.

---

