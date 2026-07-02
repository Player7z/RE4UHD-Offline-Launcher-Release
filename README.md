## Preservation Methods

This repository offers three distinct methods to achieve offline decoupling and plugin loading, depending on your system configuration and preference.

### Method 1: DLL Proxy Method (`winmm.dll`)
A lightweight, non-intrusive approach utilizing a system DLL proxy to load mods and communicate with the emulation components.

*   **Files Required:** `winmm.dll`, `steamclient.dll` (Goldberg Emulator component).
*   **Installation:** Place both files inside the game's `Bin32` folder next to `bio4.exe`.
*   **Behavior:** When launched, `winmm.dll` will verify the presence of `steamclient.dll`. If it is not found, the proxy safely falls back to acting as a standard standalone `.asi` loader.

### Method 2: Standalone Launcher Method (`re4uhd_launcher.exe` & `re4uhd_launcher.dll`)
A robust injection method designed to bypass OS-level DLL proxy mitigations often found in newer versions of Windows 10 and 11.

*   **Files Required:** `re4uhd_launcher.exe`, `re4uhd_launcher.dll`, `steamclient.dll`.
*   **Installation:** Place all three files inside the `Bin32` folder next to `bio4.exe`.
*   **Behavior:** Running `re4uhd_launcher.exe` sets the appropriate Steam environment variables, initializes the game process in a suspended state, injects `re4uhd_launcher.dll` to set up the registry redirect, and then resumes execution.

### Method 3: Import Table Patching Method (`Imports_Adder.exe`)
An advanced utility that permanently modifies the Import Address Table (IAT) of `bio4.exe` to natively require your custom decoupling DLL.

*   **Files Required:** `Imports_Adder.exe`, `re4uhd_launcher.dll`.
*   **Installation:** Place the utility and your target `.dll` inside the `Bin32` folder.
*   **Behavior:** The patcher edits the PE headers of `bio4.exe` to append a new import entry. This ensures the game always loads the designated DLL on startup without needing an external launcher or system-level proxy.
*   **Safety:** The utility automatically creates a backup of the untouched executable as `bio4.exe.unpatched` before applying any modifications.
