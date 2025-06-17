# Yahir’s Corne Keyboard ZMK Config

Este es mi setup personal de ZMK para un teclado dividido tipo Corne. Está hecho desde cero, buscando comodidad, estética y funcionalidad para uso diario, diseño, gaming y escritura fluida.

---

## 🧠 Características principales

- Layout personalizado Colemak-DH con Home Row Mods (HRM) sin temporizador (inspirado en urob)
- Configuración OLED custom usando nice!oled y nice!nano v2
- Macros personalizadas y combos para flujo de trabajo eficiente
- RGB underglow activo con efectos swirl
- ModTap (modificadores en letras) y capas espejo para navegación con una sola mano
- Sistema Bluetooth experimental activado
- Archivos limpios y organizados (`helpers.h`, `keys.h`, `corne.keymap`)

---

## 🎨 Capas principales

### 1. ALPHA (Base)
- Colemak-DH con modificadores en la fila central (Ctrl, Alt, GUI, Shift).
- Tap = letra | Hold = modificador.
- Espacio en pulgares y navegación rápida.

### 2. NAV
- Flechas en la fila central, sin mover manos.
- Acceso rápido a home, end, page up/down, delete.

### 3. SIMB
- Caracteres especiales y símbolos comunes `{ } [ ] ( )` alineados para escribir sin mirar.
- Inspirado por capas de programación.

### 4. NUM
- Numpad al estilo teclado normal en la derecha.
- Incluye coma para notación francesa y puntuación rápida.

### 5. FUNC
- F1–F12 y más: acceso a mute, Discord, Bluetooth swap.
- Layer sin HRM para acceso directo a modifiers sin retardo.

---

## 🔀 Combos activos

- `Q + W` → ESC
- `F + J` → TAB
- `D + K` → ENTER
- `S + L` → BACKSPACE

Pensados para ejecutarse con ambas manos sin interrumpir la escritura.

---

## 🔁 Macros útiles

(Algunas incompletas o en construcción)

```c
// Ejemplo de macro para abrir consola
&macro_press &kp LC(LA(T))
```

Puedes definir combinaciones complejas como abrir una app, pegar texto, etc.

---

## 💡 OLED activado

- Pantalla izquierda: animaciones y estado.
- Pantalla derecha: sin display (actualmente).
- Widgets desactivados para evitar conflictos (`layer`, `battery`, etc.).

---

## 🌈 RGB UnderGlow

- Activado efecto “swirl” por defecto (`CONFIG_ZMK_RGB_UNDERGLOW_EFF_START=3`)
- Brillo inicial moderado: 15%
- Color base azul: `HUE_START=240`
- Saturación baja para estética suave: `SAT_START=10`

---

## 📷 Vista previa del layout

![Distribución](./layout.svg)

---

## ⚙️ Archivos relevantes

- `corne.conf`: Configuraciones generales
- `helpers.h`: Macros de HRM, combinaciones y aliases
- `keys.h`: Mapeo de posiciones de teclas
- `corne.keymap`: Lógica de capas, combos, modtap y macros
- `west.yml`: Dependencias (zmk-nice-oled, helpers, etc.)

---

## 🙌 Créditos

Inspirado por:
- urob (HRM y estructura modular)
- kevinpastor (documentación y macros limpias)
- mctechnology17 (nice!oled)
- Colemak-DH community
- Pascal Getreuer (símbolos ergonómicos)

---

Disfruta este layout, modifícalo y hazlo tuyo ✨