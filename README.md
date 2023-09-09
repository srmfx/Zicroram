# Zicroram
Official Shareware Binary Repository for Zicroram

### ABOUT:
Zicroram is a CLI for the LINUX TMPFS Filesystem that adds up the following functionalities:

1 - Adding(Synchronously and Assynchronously) Data to RAM(--add or --addc)

2 - Removing Data from RAM(--remove-all or --remove)

3 - Restoring Data from DISK Back into RAM (--restore)

4 - Backing up data from RAM Into disk (--mmbackup and --mtbackup)

5 - Copying programs on system bootup (--boots or --bootsc)

6 - More instructions & commands (--help, --help-setup, --help-program, --help-info)

7 - Troubleshooting (--troubleshooting)

The program also includes a man page, but only after installing the program on the system.
  $man zicroram

### HOW IT WORKS:
The program works by creating and mounting a TMPFS device called /zicroram/ and allowing the user to add any data through a simple command, like for example:

'zicroram --add ~/Pictures ~/Music ~/Downloads'

After this the program will symlink the real path where the data was located to the newly created TMPFS mounted device allowing the user to call on his data as if it were still on the disk. The real data will be renamed to keep it safe from power blackouts and system crashes until either a --remove or --restore command is used.

In case of system crash or power blackout, once your system reboots, data can be easily restored to real data path using "zicroram --restore" which will put the original files back in place where the symlinks were created.

Many more commands can be found by typing: "zicroram --help" (after installation) or "./zicroram --help" (before installation); the --help command will list and thoroughly explain each of the commands.

### USE LICENSE:

Upon program installation using "zicroram --install-wizard" the user must agree with the displayed use license;
if the user doesn't agree with one or more terms the installation will be cancelled and the user should 
give up installation of the program at once.

The sole developer doesn't take any lyability for the mistakes that may arise from using a RamDisk(or RamDrive) software;
since RAM Storage isn't a persistent type of storage, important data may be permanently lost forever with no means of recover.

If you don't agree with the USE LICENSE of this system, do not use this system.

### OPERATING SYSTEM SUPPORT:

Zicroram should work on all GNU Linux Distributions out-of-box as long as they support:

1 - GLIBC 2.34

2 - TMPFS Enabled kernel.

Zicroram runs as an administrative tool on your system, so root access through 'sudo' is required. 

'doas' still not supported in the current version of this program.

It's advisable not to run this program under Windows' WSL; last time I checked WSL didn't support real TMPFS Filesystem and instead uses the Hard Drive as TMPFS device instead of the Ram Memory thus making the program developed in here pointless.

### INSTALLATION:

Installation can be initialized through it's commandline interface(CLI): "./zicroram --install-wizard"

The program will automatically request root authorization for the user as necessary.

### AUTHOR:

The program in here was sole developed by a single dev,

get in contact with him on the email provided in the binary release of this program and also the one in here:

###### Author: Sebastião Ribeiro Monteiro Filho
###### Email: srmfsrmf@hotmail.com

### BUGS:

If you've found a bug, you're welcome to open an issue and report it in this github.
DO NOT SEND bugs or problems over email, they'll be automatically ignored and treated as junk.

### TROUBLESHOOTING:

The binary program offers a quickhand page on troubleshooting: ./zicroram --troubleshoot

This is important as it describes most common issues users may have to deal with and how to either solve or avoid those issues.
