# Zicroram
Official Shareware Binary Repository for Zicroram

Zicroram is a CLI for the LINUX TMPFS Filesystem that adds up the following functionalities:
1 - Adding(Synchronously and Assynchronously) Data to RAM(--add or --addc)
2 - Removing Data from RAM(--remove-all or --remove)
3 - Restoring Data from DISK Back into RAM and Vice-versa(--restore)
4 - Backing up data from RAM Into disk.(--mmbackup and --mtbackup)
5 - Copying programs on system bootup(--boots or --bootsc)

It achieves this by creating and mounting a TMPFS device called /zicroram/ and allowing the user to add any data through a single command,
like for example: "zicroram --add ~/Pictures ~/Music ~/Downloads"

After this the program will symlink the original data to the TMPFS mounted device allowing the user to use his data as if it were on the disk.

Furtherover, you don't have to worry about things like system crashes and power blackouts, once your system reboots, 
data can be easily restored using "zicroram --restore" which will put original files back in place where the symlinks were created.

Many more commands can be found by typing: "zicroram --help" (after installation) or "./zicroram --help" (before installation).
the --help command will list and thoroughly explain each of the commands.

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

It's advisable not to run this program under Windows' WSL, since last time 
I checked WSL didn't support real TMPFS Filesystem and instead uses the Hard Drive as TMPFS 
device instead of the Ram Memory thus making the program developed in here pointless.

### INSTALLATION:

Installation can be initialized through it's commandline interface(CLI): "./zicroram --install-wizard"
The program will automatically request root authorization for the user as necessary.

### AUTHOR:

The program in here was sole developed by a single dev,
get in contact with him on the email provided in the binary release of this program and also the one in here:

###### Author: Sebastião Ribeiro Monteiro Filho
###### Email: srmfsrmf@hotmail.com

### TROUBLESHOOTING:

If you've found a bug, you're welcome to open an issue and report it in this github.
DO NOT SEND bugs or problems over email, they'll be automatically ignored and treated as junk.
