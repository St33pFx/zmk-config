# Yahir Salazar's ZMK Config – Colemak OLED Edition ✨

Este es mi firmware personalizado para mi teclado dividido Corne, con pantalla OLED funcional en ambos lados, RGB, macros y modificaciones al home row. El diseño está basado en la distribución **Colemak** con mejoras centradas en escritura, diseño, programación y navegación eficiente.

---

## 🛠️ Características Principales

- Pantalla **Nice!OLED** personalizada en ambos lados (izquierdo y derecho).
- Distribución **Colemak** modificada con Home Row Mods tipo HRM sin temporizador (`MAKE_HRM`).
- Iluminación **RGB Underglow** con efecto `Swirl` y colores suaves preconfigurados.
- Configuración diseñada para **ZMK Studio**, con integración para visualización en vivo.
- **Combos**, **Macros** y capas diseñadas para productividad, edición y control.
- Código modular, limpio y mantenible usando archivos como `helpers.h`, `keys.h`, `corne.keymap`.

---

## 🧠 Home Row Mods (HRM)

El corazón de la configuración. Utilizo un sistema inspirado en la técnica de urob sin temporizador directo para los modificadores del home row. Estos están definidos en `helpers.h` mediante:

```c
#define MAKE_HRM(NAME, HOLD, TAP, TRIGGER_POS) ...
```

La implementación se apoya en la variable `HRM_TAPPING_TERM` de 400ms, con ajustes finos para evitar falsos positivos en letras comunes como `s` o `t`.

Esto permite escribir rápido y con fluidez sin sacrificar acceso inmediato a Ctrl, Alt, Shift y Cmd.

---

## ⌘ Combos y Macros

Utilizo combos en zonas estratégicas para maximizar la eficiencia sin saturar las capas:

| Combo   | Teclas             | Acción     |
|---------|--------------------|------------|
| `TAB`   | Home row derecha   | Tabulador  |
| `CTRL`  | Home row izquierda | Control    |
| `CMD`   | Inferior izquierda | Cmd/GUI    |

Además, tengo una macro personalizada (`&Centrar`) que ejecuta `Ctrl + Alt + Shift + Home`, ideal para centrar objetos/texto en After Effects con un solo toque.

---

## 🌈 RGB Configuración

Mi configuración incluye:

```conf
CONFIG_ZMK_RGB_UNDERGLOW=y
CONFIG_ZMK_RGB_UNDERGLOW_EFF_START=3   # Swirl
CONFIG_ZMK_RGB_UNDERGLOW_HUE_START=240
CONFIG_ZMK_RGB_UNDERGLOW_SAT_START=10
CONFIG_ZMK_RGB_UNDERGLOW_BRT_START=15
```

Con transiciones suaves y brillo medio-bajo para evitar fatiga visual.

---

## 🖥️ Pantalla OLED

Ambos lados del Corne tienen OLED funcional. Se muestran:

- Capa activa (layer)
- Porcentaje de batería
- Estado de conexión USB/BLE
- WPM (Words Per Minute)
- Widget Luna activo (cuando habilitado)

La configuración está basada en el módulo `zmk-nice-oled` corregido (fork de M. Zeglinski), con integración modular en el archivo `screen.c` y widgets custom.

---

## 🧪 Capas definidas

Trabajo con múltiples capas activables mediante thumbs y combinaciones, optimizadas para ergonomía y velocidad.

### Alpha Layer
- Basada en **Colemak** con teclas de control y espacio en posiciones intuitivas.
- Home Row Mods activos.

### Símbolos
- Inspirada en Pascal Getreuer y ShelZuuz.
- Simetría invertida `{ } [ ] ( )` para rolls internos.

### Navegación / Números
- Numpad a la derecha con coma decimal francesa.
- Flechas colocadas en home row izquierda (como WASD).
- Home, End, Page Up/Down debajo de las flechas.

### Funciones / Media
- F1–F12 y controles multimedia (F13/F14 → Mute/Deafen para Discord).
- Alternancia y limpieza de perfiles Bluetooth con Shift.

---

## 🔄 Bluetooth + Dividido (Split)

- El lado izquierdo es el maestro BLE/USB.
- El derecho se conecta automáticamente al encenderse (sincronía por reset).
- Soporte para múltiples perfiles y cambio fluido.

---

## ⚙️ Archivos clave

| Archivo         | Función                                       |
|----------------|-----------------------------------------------|
| `corne.conf`    | Config ZMK personalizada (OLED, RGB, BLE, etc.) |
| `corne.keymap`  | Layout completo con capas, combos y macros    |
| `helpers.h`     | Macros HRM para modtap sin temporizador       |
| `keys.h`        | Declaración estructural de posiciones          |
| `west.yml`      | Módulos externos integrados correctamente      |

---

## ⚡ Compilación

### Online (GitHub Actions)

1. Clona desde template oficial con:
```bash
bash -c "$(curl -fsSL https://zmk.dev/setup.sh)"
```
2. Configura tu MCU, shield y GitHub.
3. GitHub Actions compilará y te dará el `.uf2`.

### Local

```bash
git clone https://github.com/zmkfirmware/zmk
git clone https://github.com/yahirsalazar/zmk-config
cd zmk-config

west build -s zmk/app -d build/left -b nice_nano_v2 -- -DSHIELD=corne_left
west build -s zmk/app -d build/right -b nice_nano_v2 -- -DSHIELD=corne_right
```

---

## 📥 Flasheo

1. Presiona 2x el botón reset → modo bootloader.
2. Montará un disco USB.
3. Copia el `.uf2` del lado correspondiente.
4. Se reinicia solo y queda flasheado.

---

## 🧯 Problemas comunes

- OLED conflict: corregido no duplicando `widget_layer_status`.
- HRM bug: ajustado tapping term a 400ms.
- BLE pairing: solucionado usando `CONFIG_ZMK_BLE_EXPERIMENTAL_CONN=y`.

---

## 🙌 Créditos

- urob (HRM original)
- Nick Coutsos (keymap editor)
- Pascal Getreuer (símbolos ergonómicos)
- M. Zeglinski (nice-oled fork)
- Comunidad ZMK y QMK por tanto conocimiento compartido ❤️

---

## ✍️ Autor

**Yahir Salazar**  
Corne / ZMK Power User  
Junio 2025  
[github.com/yahirsalazar](https://github.com/yahirsalazar)