# ⌨️ ZMK Config - Corne Keyboard (Nice!OLED Edition)

Configuración personalizada para mi teclado dividido **Corne**, con soporte para pantalla OLED en ambos lados, modtap, macros, combos y RGB funcional.  
Distribución **Colemak**, pensada para productividad, programación y diseño.

---

## 📷 Vista de la distribución

![Distribución del teclado](assets/my_keymap.png)

📄 También puedes ver la versión editable en vector:  
[🔗 Ver SVG (my_keymap.svg)](assets/my_keymap.svg)

---

## 🔧 Cambios principales

### 🧩 Hardware
- **Teclado:** Corne (con ProMicro NRF52840)
- **Pantalla:** Nice!OLED en ambos lados
- **RGB:** Activado con efecto `Swirl` y brillo inicial al 15%
- **Bluetooth:** Potencia TX mejorada (`CONFIG_BT_CTLR_TX_PWR_PLUS_8=y`)

---

## 🖥️ Pantalla OLED

- `CONFIG_ZMK_DISPLAY=y`
- `CONFIG_ZMK_DISPLAY_STATUS_SCREEN_CUSTOM=y`

### Widgets activos:
- Estado de capa (`layer status`)
- Porcentaje de batería
- Estado de conexión (BLE/USB)
- WPM (Words Per Minute)
- Luna (mascota animada, opcional)

---

## ⌘ Modtap (Home Row Mods)

Teclas que actúan como **modificador si se mantienen** y como **tecla normal si se tocan rápidamente**.

Ejemplo:

```dts
&mt LCTRL A     // A si la tocas, Ctrl si la mantienes
&mt LALT SPACE  // Space si la tocas, Alt si la mantienes
```

Parámetros importantes:

```conf
CONFIG_ZMK_HOLD_TAP_DELAY_MS=200
CONFIG_ZMK_HOLD_TAP_PER_KEY=y
```

Además, se usa una macro HRM (`MAKE_HRM`) en `helpers.h` para modular los home row mods sin timers externos.

---

## 🔀 Combos

Combinaciones de dos teclas que disparan otra tecla. Configurados desde keymap.

| Combo   | Teclas combinadas     | Resultado |
|---------|------------------------|-----------|
| `tab`   | home row derecha       | Tabulador |
| `ctrl`  | home row izquierda     | Control   |
| `cmd`   | teclas inferiores      | Cmd/GUI   |

---

## ⚙️ Macros

Automatización de secuencias complejas.

Ejemplo útil:

```plaintext
CTRL + ALT + SHIFT + HOME
```

Usado para centrar texto en After Effects. Implementado con `&macro_press`.

---

## 🌈 RGB Underglow

Activado en `corne.conf`:

```conf
CONFIG_ZMK_RGB_UNDERGLOW=y
CONFIG_ZMK_RGB_UNDERGLOW_EFF_START=3  // Swirl
CONFIG_ZMK_RGB_UNDERGLOW_HUE_START=240
CONFIG_ZMK_RGB_UNDERGLOW_SAT_START=10
CONFIG_ZMK_RGB_UNDERGLOW_BRT_START=15
```

---

## 🧪 Extras útiles

- `CONFIG_ZMK_EXT_POWER=y`: apaga OLED si no hay USB
- `CONFIG_ZMK_BLE_EXPERIMENTAL_CONN=y`: mejora conexión BLE
- `CONFIG_ZMK_KSCAN_DEBOUNCE_PRESS_MS=1`: menos latencia

---

## 🧼 Problemas resueltos

- ❌ `multiple definition of 'widget_layer_status'`  
  ✅ Se solucionó estructurando correctamente los módulos OLED y evitando conflicto entre lados.

---

## 📁 Archivos incluidos

| Archivo                | Descripción                            |
|------------------------|----------------------------------------|
| `assets/my_keymap.png`| Vista gráfica del layout               |
| `assets/my_keymap.svg`| Versión vectorial editable del layout  |
| `corne.conf`          | Configuración principal del teclado    |
| `corne.keymap`        | Keymap con combos/macros/modtap        |
| `helpers.h`           | Home row mods personalizados (HRM)     |
| `keys.h`              | Definición estructural de columnas     |
| `west.yml`            | Configuración de módulos y dependencias|

---

## 🧩 Herramientas utilizadas

- [keymap-editor](https://nickcoutsos.github.io/keymap-editor/)
- [zmk-nice-oled](https://github.com/mzeglinski/zmk-nice-oled)
- [ZMK Firmware](https://zmk.dev/)

---

## 🛠️ Instalación de Firmware ZMK

ZMK permite compilar el firmware de dos formas: **en la nube (GitHub Actions)** o **localmente**.

### 📡 GitHub Actions (recomendado)

1. Crea un repo vacío en GitHub llamado `zmk-config`  
2. Ejecuta:

```bash
bash -c "$(curl -fsSL https://zmk.dev/setup.sh)"
```

3. Selecciona teclado, MCU, usuario y repo.  
4. GitHub compilará el firmware automáticamente.
5. Descarga los `.uf2` desde la pestaña **Actions**.

### 💻 Compilación local

```bash
git clone https://github.com/zmkfirmware/zmk
git clone https://github.com/tu_usuario/zmk-config
cd zmk-config

# Lado izquierdo
west build -s zmk/app -d build/left -b nice_nano_v2 -- -DSHIELD=corne_left

# Lado derecho
west build -s zmk/app -d build/right -b nice_nano_v2 -- -DSHIELD=corne_right
```

### 🚀 Flashear firmware

1. Presiona dos veces el botón reset en el nice!nano
2. Aparecerá como dispositivo USB
3. Copia el `.uf2` correspondiente
4. Reinicia automáticamente

### 🔄 Teclado dividido

- Solo el lado izquierdo envía salida (USB/BLE)
- El derecho se conecta automáticamente si está pareado
- Asegúrate que ambos tengan energía

### 📶 Bluetooth

- ZMK anuncia el dispositivo si no está conectado
- Empareja desde tu celular o laptop
- Soporte para múltiples perfiles BLE

---

## ✍️ Autor

Yahir Salazar  
Junio 2025  
[github.com/yahirsalazar](https://github.com/yahirsalazar)

---

## ❤️ Créditos

- ZMK Community  
- Nick Coutsos (keymap editor)  
- M. Zeglinski (nice-oled fork)  
- Todos los contribuidores del ecosistema ZMK
