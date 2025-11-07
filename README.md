# Witnull's Bypass NRO

## [!WARNING]
### ⚠️ Use at Your Own Risk!
This set of scripts and configurations makes deep changes to the Windows operating system. It is intended for personal use only on non-critical machines.

### ⛔ NOT FOR CORPORATE OR COMPANY USE
Do not use this in a business or enterprise environment. Many settings (like allowing blank passwords and disabling security checks) create significant security vulnerabilities and will violate company IT policies.

> **Note:** This method skips the Windows Microsoft account requirement without debloating Windows. All Windows features and functionality remain intact.

> **Note2:** Default password: pass

From the OOBE Screen press Shift + F10

```
curl -L https://raw.githubusercontent.com/Witnull/bypassnro/refs/heads/main/bypass.txt -o skip.cmd
skip.cmd
```

You'll be prompted to enter your desired username and password. This will skip the entire OOBE process including microsoft account and ANY questions during the setup process. It still allows you to select your language, region, and keyboard layout.

# What it do?
## 1. windowsPE Pass

Runs during the initial Windows Setup, before installation.

These commands modify the installer environment to bypass hardware requirements.

- Bypass TPM 2.0 Check: Allows installation on systems without a TPM 2.0 module.

- Bypass Secure Boot Check: Allows installation on systems without Secure Boot.

- Bypass RAM Check: Allows installation on systems with less than the required RAM.

## 2. specialize Pass

Runs before the "Out-of-Box Experience" (OOBE) to apply system-wide settings.

System-Wide Settings (HKLM)

- Disable Password Expiration: Sets net.exe accounts /maxpwage:UNLIMITED so passwords never expire.

- Enable Long Paths: Allows file paths longer than 260 characters.

- Harden C: Drive Permissions: Removes the 'Authenticated Users' group from the C:\ root for added security.

- Enable Process Auditing: Enables success/failure auditing for 'Process Creation' (Event ID 4688).

- Enable Command Line Logging: Forces Windows to include the full command line text in process creation audit logs.

- Set PowerShell Policy: Sets the machine's execution policy to RemoteSigned, allowing local scripts to run.

- Prevent Device Encryption: Disables automatic BitLocker device encryption.

- Allow Blank Passwords: Sets the LimitBlankPasswordUse policy to 0, which is critical for allowing login with a blank password.

- Disable Auto-Logon: Sets AutoLogonCount to 0 to ensure no pending automatic logins are attempted.

- Default User Profile Settings (Template for New Users)

- Show File Extensions: Disables HideFileExt so new users see file extensions (e.g., .txt, .exe) by default.

- Show Hidden Files: Sets Hidden to 1 so new users see hidden files and folders.

- Enable Taskbar 'End Task': Enables the "End Task" option when right-clicking an app on the taskbar (a Windows 11 feature).

## 3. oobeSystem Pass

Runs during the OOBE (the user setup screens) and on the user's first login.

OOBE Screen Configuration

- Hide EULA: Skips the End User License Agreement page.

- Hide OEM Registration: Skips the manufacturer's registration screen.

- Hide Online Account Screens: Skips the prompt to sign in with a Microsoft Account.

- Hide Wireless Setup: Skips the Wi-Fi connection screen.

- Set PC Protection: Sets to "3" (Express Settings).

- Create Local Account: Creates a local administrator account. The Name is set by your batch script, and the Password is set to be blank.

- First Logon Commands (For the New User)

- Restore Classic Context Menu: Applies the registry key to bring back the Windows 10-style right-click menu in Windows 11.

- Set Explorer to 'This PC': Changes File Explorer's default view from 'Home' to 'This PC'.

- Set Taskbar Search: Changes the taskbar search from a full box to 'Icon only'.

- Cleanup: Deletes the unattend.xml and other setup files from C:\Windows\Panther to remove any sensitive data (like the plain-text password).
