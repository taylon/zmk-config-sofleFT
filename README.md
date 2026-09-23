# Sofle FT — Adv360 layout

ZMK configuration for the FalbaTech Sofle wireless, adapted from the personal
`Adv360-Pro-ZMK/config/adv360.keymap`. The letter layout, home-row modifiers,
behavior timings, Numpad and Symbols layers match the Adv360. ZMK Studio is
disabled; edit `config/sofle.keymap` and rebuild to change the layout.

## Base layout

Rows are shown left to right as viewed while typing. The two keys in the gap
on the fourth row are normal keys: Escape on the left and Enter on the right.
This keyboard has no encoders. The bottom row has five thumb keys per half.

```text
 F1    F2    F3    F4    F5    F6                  F9    F10   F11   F12   F13   F14
 Del   Q     W     F/Num P     B                   J     L     U     Y     ;     F17
 Tab   A/GUI R/Alt S/Ctrl T    G                   M     N     E/Ctrl I/Alt O/GUI Quote
 KP-   Z     X     C     D     V     Esc     Enter K     H     ,     .     /     _
             Copy  Left  Right Bksp Shift   Symbols Space Up    Down  Mod
```

- Hold **A/R/S** for left GUI/Alt/Ctrl, or **E/I/O** for left Ctrl/Alt/GUI.
  These retain the Adv360's balanced 240 ms tapping term, 175 ms quick tap,
  150 ms prior idle, and opposite-hand hold triggers remapped to Sofle positions.
- Tap **F** to type `f`; hold it for **Numpad**.
- Tap **Shift** once for sticky left Shift (1-second timeout and quick release),
  twice for Caps Word. All tap dances retain the Adv360's 200 ms tapping term.
- **Quote** produces `"`, or `'` with left Shift.
- Tap **Copy** once for Ctrl+C, twice for Ctrl+X.
- Tap **Symbols** for the sticky Symbols layer; holding it also keeps the layer active.
- Hold the outermost right thumb key for **Mod**.

## Numpad

Hold **F**. Numbers stay on the same letter positions as on the Adv360:

```text
 L = 7    U = 8    Y = 9
 N = 4    E = 5    I = 6
 H = 1    , = 2    . = 3
```

On the right thumb row, **Up = 0**, **Down = decimal point**, and **Mod = equals**.
Other positions fall through to Base.

## Symbols

The left letter block is unchanged. Paired delimiters use one tap for the
opening character and two taps for the closing character.

| Base key | Symbols output |
|---|---|
| F4 | `:=` macro |
| Q / W / F / P / B | `%` / `@` / `{` or `}` / `$` / `\|` |
| A / R / S / T / G | `#` / `~` / `(` or `)` / `=` / `+` |
| Z / X / C / D / V | `^` / `!` / `[` or `]` / `&` / `*` |
| Copy thumb | `->` macro |
| Left thumb arrow | Backslash |
| Right thumb arrow | Grave accent |

Other positions fall through to Base (or Numpad if F is also held).

## Mod

Hold **Mod**, then press the indicated Base key:

| Base key | Action |
|---|---|
| F2–F6 | Select Bluetooth profile 0–4 |
| K | Clear the selected Bluetooth profile |
| Esc / Enter inner key | Bootloader on that key's half |
| E / I | Select USB / Bluetooth output |
| Del | Toggle external power |
| Q / W | RGB hue down / up |
| F / P | RGB saturation down / up |
| B | Next RGB effect |
| A / R | RGB brightness down / up |
| S / T | RGB speed up / down |
| Space | Toggle RGB |
| Left / Right thumb arrows | Page Up / Page Down |
| Up / Down thumb arrows | Home / End |

## Differences from the Adv360

- Escape and Enter move to the left and right inner keys.
- The thumb row retains Copy/Cut, all four arrows, Backspace, Shift/Caps Word,
  Symbols and Space. Mod moves to the outermost right thumb key.
- Page Up/Down are available through Mod + Left/Right;
  Home/End move to Mod + Up/Down.
- The `->` macro moves from the missing F21 position to Symbols + Copy.
  Numpad equals moves from the missing F22 position to the Mod thumb key.
- F8, F15, F16, F18–F24 and the unused thumb positions are omitted.
  F7 was already absent from the Adv360 keymap.
- Kinesis-specific battery reporting, version macro and backlight controls
  are omitted. Sofle RGB, output selection and external-power controls are
  available on Mod.

## Hardware and firmware

- Upstream `sofle` shield with two nice!nano v2 controllers.
- 60 normal keys, including switches in the two encoder positions.
- OLED SSD1306 or nice!view, depending on the selected build.
- 30 per-key RGB LEDs per half; encoder support is disabled.

GitHub Actions builds these configurations from `build.yaml`:

| Artifact | Half / display |
|---|---|
| `sofle_left_oled` | Left / OLED |
| `sofle_left_niceview` | Left / nice!view |
| `sofle_right_oled` | Right / OLED |
| `sofle_right_niceview` | Right / nice!view |
| `settings_reset` shield build | Clear stored settings |

Flash the matching firmware onto **both halves**. Connect each half over USB,
double-press Reset to enter its bootloader, and copy its UF2 onto the `NICENANO`
drive. The halves communicate wirelessly. Pair the keyboard as **Sofle FT**,
using Mod + F2–F6 to select a Bluetooth profile when needed.
