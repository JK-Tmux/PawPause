# PawPause 🐾

PawPause is a lightweight Windows utility designed to stop cats from accidentally typing, sending messages, triggering shortcuts, or otherwise causing chaos when they walk across your keyboard.

Instead of disabling the keyboard entirely, PawPause watches the timing of physical key presses and attempts to distinguish normal human typing from the near-simultaneous key presses caused by a paw.

## How It Works

PawPause uses a Windows low-level keyboard hook to intercept keyboard input before it reaches other applications.

Normal keyboard input is briefly buffered. If the input looks like normal typing, it is immediately forwarded to Windows.

If multiple keys are pressed almost simultaneously in a pattern consistent with a paw landing on the keyboard, the buffered input is discarded instead.

By default, PawPause detects:

- 3 or more non-modifier keys
- pressed within approximately 20 milliseconds
- while those keys are simultaneously held down

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

### Recommended

Download the latest `PawPause.exe` from the **Releases** section.

No Python installation is required.

Run:

```text
PawPause.exe
```

### Run From Source

PawPause currently requires Windows.

Install Python 3 and run:

```powershell
py pawpause.py
```

PawPause uses Python's standard library and does not require additional Python packages.

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

## Running PawPause Manually

Automatic startup is optional. PawPause can also be launched whenever it is needed by simply double-clicking `PawPause.exe`.

PawPause begins monitoring keyboard input as soon as it starts and remains active while the application is running.

No installation process is required. `PawPause.exe` is a standalone application and can be stored anywhere on your computer.

> **Tip:** If you plan to use PawPause regularly, store the executable in a permanent location such as a dedicated `PawPause` folder. This also prevents a Startup shortcut from breaking if the executable is later moved.

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
- PawPause currently targets Windows only.

Do not rely on PawPause as a security mechanism or as protection against destructive actions.

## Building the EXE

Install PyInstaller:

```powershell
py -m pip install pyinstaller
```

Build PawPause:

```powershell
py -m PyInstaller --onefile --clean --icon="pawpause.ico" --name PawPause pawpause.py
```

The resulting executable will be located at:

```text
dist\PawPause.exe
```

The computer running the compiled executable does **not** need Python installed.

## Contributing

Bug reports, testing results, and improvements to the detection algorithm are welcome.

If PawPause incorrectly detects normal typing or fails to detect a paw press, include information about the keyboard and the input pattern that caused the problem.

## License

See [LICENSE](LICENSE).