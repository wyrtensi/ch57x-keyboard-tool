# Bluetooth audio trigger for the 3x4 CH57x keypad

## Problem

The right-knob press was initially assigned to `F24`, and then to `F13`.
Both keys worked through the USB HID connection, but did not reliably reach
Windows when the keypad was connected through its Bluetooth `HID Keyboard`
profile. As a result, AutoHotkey could not receive the trigger.

Bluetooth also sends a knob hold as a short key tap. A host-side script cannot
distinguish a hold from a single press after the key-up event has already been
sent.

## Solution

Use the standard keyboard chord `Ctrl+Alt+Shift+F12` for the right-knob press:

```yaml
press: "ctrl-alt-shift-f12"
```

The combination uses the normal HID `F12` usage with standard modifiers. It is
unlikely to conflict with normal shortcuts and works through both USB and
Bluetooth on this keypad.

The paired AutoHotkey script is `D:\modifications\autohotkey\ch57x-audio-cycle.ahk`.
It interprets the trigger as follows:

- one press: mute or unmute after 700 ms;
- two presses within 300 ms: switch between Speakers and Headphones;
- a physical 700 ms hold over USB: switch between Speakers and Headphones.

The double-press action is the Bluetooth-compatible replacement for a hold.
