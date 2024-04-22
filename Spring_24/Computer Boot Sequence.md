---
aliases:
  - Boot Sequence
---
The computer boot sequence is a series of events that occur when you turn on or restart your computer, leading to the loading of the operating system and the initialization of the system for user interaction. Here's a detailed description of the typical computer boot sequence:

1. **Power On:**
   - When you press the power button or initiate a restart, the power supply sends power to the computer's components.

2. **Power-On Self-Test (POST):**
   - The first thing the computer does is perform a Power-On Self-Test (POST). This diagnostic process checks the integrity of the hardware components, including the processor, memory (RAM), storage devices, and other critical system components.
   - If any issues are detected during the POST, the computer may display error messages or beep codes to indicate hardware problems.

3. **BIOS/UEFI Initialization:**
   - After the POST, the Basic Input/Output System (BIOS) or Unified Extensible Firmware Interface (UEFI) takes control. The BIOS/UEFI is firmware stored on a chip on the motherboard.
   - The BIOS/UEFI initializes the system's hardware, including the CPU, memory, storage controllers, and input/output devices.

4. **Boot Device Selection:**
   - The BIOS/UEFI looks for the boot device, which is the storage device containing the operating system. This is typically the computer's internal hard drive or SSD, but it can also be an external drive or a network location.
   - The boot device is specified in the BIOS/UEFI settings.

5. **Boot Loader Execution:**
   - Once the boot device is identified, the BIOS/UEFI transfers control to the boot loader. The boot loader is a small program responsible for loading the operating system into memory.
   - For systems using the traditional BIOS, the boot loader might be the Master Boot Record (MBR) or another boot sector. For UEFI systems, the boot loader is an EFI executable.

6. **Operating System Kernel Loading:**
   - The boot loader loads the core components of the operating system, including the kernel, into memory.
   - The kernel is the central part of the operating system that manages hardware resources, executes processes, and provides essential services.

7. **Device Initialization:**
   - The operating system takes over control from the boot loader and proceeds to initialize additional hardware devices, such as peripherals, graphics cards, and network interfaces.

8. **File System Mounting:**
   - The operating system mounts the file system(s) on the boot device, making the file structure accessible to the user and applications.

9. **User Space Initialization:**
   - Once the core components are loaded, the operating system initializes user space services and processes. This includes starting system daemons, background services, and user login processes.

10. **User Login/Graphical User Interface (GUI):**
    - The system is now fully booted, and it prompts the user to log in. If a graphical user interface (GUI) is used, the desktop environment or window manager is loaded.

11. **Startup Applications:**
    - After user login, any user-specific startup applications or scripts are executed.

12. **Ready State:**
    - The computer is now in a ready state, and the user can interact with the operating system and launch applications.

It's important to note that variations exist in the boot sequence based on factors such as the computer's architecture (BIOS or UEFI), the operating system in use, and specific system configurations. Additionally, some systems may have additional steps or variations in the boot process, such as network booting, pre-boot authentication, or firmware-specific initialization procedures.