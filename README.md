# RoboGestor

RoboGestor is a Python-based library for automating interactions with Android devices using the `uiautomator2` framework. It provides an easy-to-use interface for common tasks such as app management, screen unlocking, UI element interaction, and executing ADB shell commands.

## Features

- **App Management**: Start and stop Android apps by their package names.
- **Screen Control**: Unlock the screen, lock the device, and perform swipe gestures.
- **UI Interaction**: Click on UI elements, check for text visibility, and retrieve screen text.
- **Scrolling Utilities**: Scroll to the top or bring specific text into view by swiping.
- **Toggle State**: Get the ON/OFF state of switches associated with specific text elements.
- **Shell Commands**: Execute ADB shell commands directly on the device.

---

## Installation

Make sure you have `uiautomator2` installed. You can install it using pip:

```bash
pip install uiautomator2
```

For detailed instructions on setting up `uiautomator2`, refer to its [official documentation](https://github.com/openatx/uiautomator2).

---

## Usage

### Import and Initialize RoboGestor

```python
from RoboGestor import RoboGestor

# Initialize RoboGestor (connect to default device or specify IP address)
gestor = RoboGestor()
# For remote connection, pass the IP address
# gestor = RoboGestor(ip="192.168.1.100")
```

---

### Key Functionalities

#### 1. App Management
```python
gestor.open_app("com.example.app")  # Launch an app
gestor.close_app("com.example.app")  # Force-stop an app
```

#### 2. Screen Lock/Unlock
```python
gestor.unlock_phone()  # Unlock the phone
gestor.lock_with_power_button()  # Lock the phone
```

#### 3. UI Element Interaction
```python
# Click on a text element
gestor.find_and_click_text("Settings")

# Check if a text is visible on the screen
is_visible = gestor.check_text_on_view("Wi-Fi")
print(is_visible)

# Retrieve all visible text elements on the screen
screen_text = gestor.get_screen_text()
print(screen_text)
```

#### 4. Swipe and Scroll
```python
# Swipe up to unlock
gestor.swipe_up_to_unlock()

# Bring specific text into view by swiping
gestor.bring_text_into_view("Notifications")

# Scroll to the top
gestor.scroll_to_top()
```

#### 5. Toggle State
```python
# Get the ON/OFF state of a toggle switch
is_enabled = gestor.get_toggle_state("Wi-Fi")
print(is_enabled)
```

#### 6. Device Shell Commands
```python
# Run an ADB shell command
output = gestor.run_command_in_device_shell("ls /sdcard/")
print(output)
```

---

## Decorators

The library includes a `@delay_execution` decorator to add a 2-second delay before executing certain functions. This is particularly useful for allowing UI transitions to complete.

```python
@delay_execution
def my_function():
    print("This function runs after a 2-second delay.")
```

---

## Example Workflow

```python
from RoboGestor import RoboGestor

# Initialize RoboGestor
gestor = RoboGestor()

# Unlock the phone
gestor.unlock_phone()

# Launch an app
gestor.open_app("com.example.app")

# Interact with UI elements
if gestor.find_and_click_text("Login"):
    gestor.send_keys("username123")
    gestor.send_keys("password123")
    gestor.find_and_click_text("Submit")

# Retrieve screen text
print(gestor.get_screen_text())

# Lock the phone
gestor.lock_with_power_button()
```

---

## Requirements

- Python 3.x
- `uiautomator2` library
- Android device with Developer Options and USB Debugging enabled

---

## Notes

- Ensure that the `uiautomator2` server is installed and running on your Android device.
- Make sure your device and computer are on the same network if using a remote connection.

---

## License

This project is licensed under the MIT License. See the LICENSE file for details.