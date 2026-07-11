# TextOS Architecture Overview

1. THE MBR (Stage 1)
   - Function: Hardware Handshake
   - Responsibility: Locate Stage 2 on storage; load into RAM.
   - Limitation: 512 bytes (BIOS constraints).

2. THE KERNEL (Stage 2)
   - Function: Hardware Bridge
   - Responsibility: Configure Video Controller (VGA 13h);
     switch to 320x200 pixel-level graphics mode.

3. THE GUI ENGINE (Stage 3)
   - Function: Desktop Rendering
   - Responsibility: Manage linear framebuffer (0xA0000).
   - Core Mechanics: 
     - Pixel Mapping: Direct memory-to-screen address translation.
     - Double Buffering: Prevent flicker by saving/restoring
       background pixels behind moving UI objects (cursor/windows).
     - Event Loop: Continuous cycle of Reading inputs (keyboard/mouse),
       Calculating state, and Redrawing UI elements.

4. USER INTERFACE ILLUSION
   - Taskbar: Fixed coordinate memory range (Bottom rows).
   - Windowing: Rectangle-drawing routines using borders/fills.
   - Interaction: Keyboard interrupts drive coordinate changes;
     State variables track active window focus.
