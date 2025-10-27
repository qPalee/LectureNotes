Kernel-mode debugging
As mentioned, there are two debuggers that can be used for kernel debugging: a
command-line version (Kd.exe) and a GUI version (Windbg.exe). You can perform three types of kernel
debugging with these tools:
Open a crash dump file created as a result of a Windows system crash. (See Chapter 15, “Crash
dump analysis,” in Part 2 for more information on kernel crash dumps.)
Connect to a live, running system and examine the system state (or set breakpoints if you’re
debugging device driver code). This operation requires two computers: a target (the system being
debugged) and a host (the system running the debugger). The target system can be connected to the
host via a null modem cable, an IEEE 1394 cable, a USB 2.0/3.0 debugging cable, or the local
network. The target system must be booted in debugging mode. You can configure the system to boot
in debugging mode using Bcdedit.exe or Msconfig.exe. (Note that you may have to disable secure
boot in the UEFI BIOS settings.) You can also connect through a named pipe—which is useful when
debugging Windows 7 or earlier versions through a virtual machine product such as Hyper-V,
Virtual Box, or VMWare Workstation—by exposing the guest operating system’s serial port as a
named pipe device. For Windows 8 and later guests, you should instead use local network
debugging by exposing a host-only network using a virtual NIC in the guest operating system. This
will result in 1,000x performance gain.
Windows systems also allow you to connect to the local system and examine the system state. This
is called local kernel debugging. To initiate local kernel debugging with WinDbg, first make sure
the system is set to debug mode (for example, by running msconfig.exe, clicking the Boot tab,
selecting Advanced Options, selecting Debug, and restarting Windows). Launch WinDbg with
admin privileges and open the File menu, choose Kernel Debug, click the Local tab, and then click
OK (or use bcdedit.exe). Figure 1-6 shows a sample output screen on a 64-bit Windows 10
machine. Some kernel debugger commands do not work when used in local kernel debugging mode,
such as setting breakpoints or creating a memory dump with the .dump command. However, the
latter can be done with LiveKd, described later in this section.
FIGURE 1-6 Local kernel debugging.
Once connected in kernel-debugging mode, you can use one of the many debugger extension commands
—also known as bang commands, which are commands that begin with an exclamation point (!)—to
display the contents of internal data structures such as threads, processes, I/O request packets, and
memory management information. Throughout this book, the relevant kernel debugger commands and
output are included as they apply to each topic being discussed. An excellent companion reference is the
Debugger.chm help file, contained in the WinDbg installation folder, which documents all the kernel
debugger functionality and extensions. In addition, the dt (display type) command can format more than
1,000 kernel structures because the kernel symbol files for Windows contain type information that the
debugger can use to format structures.

LiveKd tool
LiveKd is a free tool from Sysinternals that enables you to use the standard Microsoft kernel debuggers
just described to examine the running system without booting the system in debugging mode. This
approach might be useful when kernel-level troubleshooting is required on a machine that wasn’t booted
in debugging mode. Certain issues might be hard to reproduce reliably, so a reboot with the debug option
enabled might not readily exhibit the error.
You run LiveKd just as you would WinDbg or kd. LiveKd passes any command-line options you
specify to the debugger you select. By default, LiveKd runs the command-line kernel debugger (kd). To
have it run WinDbg, use the -w switch. To see the help files for LiveKd switches, use the -? switch.
LiveKd presents a simulated crash dump file to the debugger so you can perform any operations in
LiveKd that are supported on a crash dump. Because LiveKd relies on physical memory to back the
simulated dump, the kernel debugger might run into situations in which data structures are in the middle of
being changed by the system and are inconsistent. Each time the debugger is launched, it starts with a fresh
view of the system state. If you want to refresh the snapshot, enter the q command to quit the debugger.
LiveKd will ask you whether you want to start it again. If the debugger enters a loop in printing output,
press Ctrl+C to interrupt the output and quit. If it hangs, press Ctrl+Break, which will terminate the
debugger process. LiveKd will then ask you whether you want to run the debugger again.