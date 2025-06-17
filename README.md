# ⌨️ ZMK Config – Corne con OLED, RGB, ModTap y más

Este es mi layout personalizado para el teclado dividido **Corne**, con soporte completo para **OLED**, **RGB**, **modtap**, **combos**, y **macros funcionales**.  
Hecho para mejorar productividad, estética y experiencia de escritura con distribución **Colemak (no DH)**.  
Pensado para **uso cotidiano**, **programación** y **diseño** (Blender, Maya y otros programas 3D).

---

## 🌐 Distribución (Vista previa)

![Distribución del teclado](assets/my_keymap.png)  
🔗 [Ver en formato vectorial SVG](assets/my_keymap.svg)

---

## 🧠 Características

- **Distribución Colemak clásica** (no DH).
- **Home Row Mods (ModTap)**.
- **OLED funcional** en el lado izquierdo con animación.
- **RGB Underglow** con efecto swirl y colores suaves.
- **Combos definidos para ESC y ENTER**.
- **Macros útiles para After Effects**.
- **Modularizado** con `helpers.h` y `keys.h`.

---

## 🧩 Capas principales

### 🔤 ALPHA
- Colemak clásica.
- Home row mods: letras que al mantener se vuelven Ctrl, Alt, GUI o Shift.

### 🧭 NAV
- Flechas y navegación sin mover las manos.
- Delete, Home, End, PgUp/PgDn.

### 🔣 SIMB
- Símbolos `{ } [ ] ( )`, `=`, `+`, `*`, `!`, `?` bien posicionados para programación.

### 🔢 NUM
- Numpad al estilo tradicional, accesible con una capa.

### 🖥️ FUNC
- F1–F12 (en proceso de ser agregados).
- Espacio reservado para acciones multimedia, BLE y herramientas.

---

## 🔁 Combos funcionales

| Combo       | Resultado |
|-------------|-----------|
| `W + F`     | ESC       |
| `R + S`     | ENTER     |

Pensados para ejecutarse sin mover las manos de la posición base.

---

## ⚡ Macros definidas

### 🎯 Macro 1 – Centrar texto en After Effects
```c
&macro_press &kp LC(LA(LS(HOME)))
```

### ✂️ Macro 2 – Cortar capas en After Effects
```c
&macro_press &kp LC(LS(D))
```

Estas macros están definidas en `helpers.h` y llamadas desde `corne.keymap`.

---

## 🌈 RGB UNDERGLOW

```conf
CONFIG_ZMK_RGB_UNDERGLOW=y
CONFIG_ZMK_RGB_UNDERGLOW_EFF_START=3  // Swirl
CONFIG_ZMK_RGB_UNDERGLOW_HUE_START=240
CONFIG_ZMK_RGB_UNDERGLOW_SAT_START=10
CONFIG_ZMK_RGB_UNDERGLOW_BRT_START=15
```

---

## 🖥️ OLED

- OLED activado en el lado izquierdo.
- Pantalla muestra animación (como Luna), estado de capa, batería, etc.
- OLED derecho desactivado para evitar errores de doble definición.

---

## 📁 Archivos principales

| Archivo            | Descripción                                         |
|--------------------|-----------------------------------------------------|
| `corne.keymap`     | Capas, combos, macros y bindings                    |
| `corne.conf`       | Configuración ZMK del teclado                       |
| `helpers.h`        | Definiciones de macros y alias                      |
| `keys.h`           | Mapeo físico del teclado                            |
| `west.yml`         | Dependencias como nice-oled y nodefree              |

---

## 🧪 Compilación local

```bash
git clone https://github.com/zmkfirmware/zmk
git clone https://github.com/tu_usuario/zmk-config
cd zmk-config

# Compilar lado izquierdo
west build -s zmk/app -d build/left -b nice_nano -- -DSHIELD=corne_left

# Compilar lado derecho (opcional, OLED desactivado)
west build -s zmk/app -d build/right -b nice_nano -- -DSHIELD=corne_right
```

---

## 🚀 Alternativa: GitHub Actions

```bash
bash -c "$(curl -fsSL https://zmk.dev/setup.sh)"
```

Sigue los pasos y GitHub compilará tus `.uf2` automáticamente. Descárgalos desde la pestaña **Actions**.

---

## 🧼 Problemas comunes

| Problema                              | Solución                                       |
|--------------------------------------|------------------------------------------------|
| `widget_layer_status` duplicado      | Desactiva `CONFIG_ZMK_DISPLAY` en `corne_right` |
| RGB no responde                      | Verifica `CONFIG_WS2812_STRIP=y`               |
| OLED derecho no prende               | Solo está activo en `corne_left`               |
| ModTap no responde                   | Usa `CONFIG_ZMK_HOLD_TAP_DELAY_MS=200`         |

---

## 🧡 Créditos

- **urob** por el sistema de Home Row Mods.
- **nickcoutsos** por [Keymap Visual Editor](https://nickcoutsos.github.io/keymap-editor/).
- **mzeglinski** por el módulo `zmk-nice-oled`.
- Comunidad ZMK & Colemak.

---

## ✍️ Autor

Yahir Salazar  
📅 Junio 2025  
🔗 [github.com/yahirsalazar](https://github.com/yahirsalazar)