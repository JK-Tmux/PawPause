# PawPause 🐾

PawPause is a lightweight Windows utility designed to stop cats from accidentally typing, sending messages, triggering shortcuts, or otherwise causing chaos when they walk across your keyboard.

Instead of disabling the keyboard entirely, PawPause watches the timing of physical key presses and attempts to distinguish normal human typing from the near-simultaneous key presses caused by a paw.

## How It Works

PawPause uses a Windows low-level keyboard hook to intercept keyboard input before it reaches other applications.

Normal keyboard input is briefly buffered. If the input looks like normal typing, it is immediately forwarded to Windows.

If multiple keys are pressed almost simultaneously in a pattern consistent with a paw landing on the keyboard, the buffered input is discarded instead.

By default, PawPause detects:

- 3 or more non-modifier keys
- Pressed within approximately 20 milliseconds
- While those keys are simultaneously held down

This allows PawPause to catch a paw press before the first key in the detected cluster reaches the active application.

## Why?

Because this:

```text
aaaaaaaaaaaaaaa
```

is annoying.

And this:

```text
[cat steps on keyboard]

Enter
```

can be considerably more annoying.

PawPause was created to let the keyboard remain usable without letting a cat accidentally interact with whatever happens to be open.

## Installation

1. Download the latest `PawPause.exe` from the **Releases** section of this repository.
2. Place `PawPause.exe` in a permanent location on your computer.
3. Double-click `PawPause.exe` to start PawPause.

No installation process is required.

PawPause is a standalone Windows executable. Python and other additional software are not required.

## Running PawPause Manually

Automatic startup is optional.

PawPause can be launched whenever it is needed by simply double-clicking:

```text
PawPause.exe
```

PawPause begins monitoring keyboard input as soon as it starts and remains active while the application is running.

Since no installation is required, `PawPause.exe` can be stored anywhere on your computer.

> **Tip:** If you plan to use PawPause regularly, store the executable in a permanent location such as a dedicated `PawPause` folder. This also prevents a Startup shortcut from breaking if the executable is later moved.

## Start PawPause Automatically

PawPause can be configured to launch automatically when you sign into Windows.

1. Press `Win + R`
2. Enter:

```text
shell:startup
```

3. Press Enter.
4. Create a shortcut to `PawPause.exe` inside the Startup folder.

Keep the actual executable in a permanent location. The Startup folder should contain a **shortcut** to the executable rather than the executable itself.

Once configured, PawPause will start automatically each time you sign into Windows.

## Detection

PawPause does **not** simply classify fast typing as cat input.

The detector looks for several physical keys being pressed almost simultaneously.

For example:

```text
Normal fast typing:

T ↓
    H ↓
T ↑
        E ↓
    H ↑
```

Compared with a paw:

```text
J ↓
K ↓  } within a few milliseconds
L ↓
```

The short buffering period allows PawPause to discard the entire detected cluster rather than waiting until several unwanted keystrokes have already reached the application.

## Current Limitations

PawPause is an experimental utility.

- Detection thresholds may need adjustment for different keyboards and typing styles.
- Some unusual human key combinations could potentially be mistaken for paw input.
- Windows secure key sequences are outside the control of a normal user-space keyboard hook.
- PawPause currently supports Windows only.

PawPause should not be relied upon as a security mechanism or as protection against destructive actions.

## Issues and Feedback

If you encounter a problem with PawPause, you can report it through the **Issues** section of this repository.

When reporting an issue, include as much information as possible about what happened and what you were doing when the problem occurred.

## License

PawPause is currently distributed as compiled software only. Source code is not included in this repository.

All rights reserved.