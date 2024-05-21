# Zicroram
Official Shareware Binary Repository for Zicroram

## ABOUT:
Zicroram is a CLI for the LINUX TMPFS/RAMFS Filesystem that adds up Ramdisk/Ramdrive features:

1 - Adding(Synchronously and Assynchronously) Data to RAM(**--add** or **--addc**)

2 - Removing Data from RAM(**--remove-all** or **--remove**)

3 - Restoring Data from DISK Back into RAM (**--restore**)

4 - Backing up data from RAM Into disk (**--mmbackup** and **--mtbackup**)

5 - Copying programs on system bootup (**--boots** or **--bootsc**)

6 - More instructions & commands (**--help**, **--help-setup**, **--help-program**, **--help-info**)

7 - Troubleshoot (**--troubleshoot**)

The program also includes a man page, you can read it once the program is installed on the system: 

    $ man zicroram

## HOW IT WORKS:
The program works by creating and mounting a TMPFS device called /zicroram/ and allowing the user to add any data through a simple command, like for example:

    $ zicroram --add ~/Pictures ~/Music ~/Downloads

After this the program will symlink the real path where the data was located to the newly created TMPFS mounted device allowing the user to call on his data as if it were still on the disk. The real data will be renamed to keep it safe from power blackouts and system crashes until either a --remove or --restore command is used.

In case of system crash or power blackout, once your system reboots, data can be easily restored to real data path using

    $ zicroram --restore
The above command will put the original files back in place where the symlinks were created.

Many more commands can be found by typing: 

    $ zicroram --help    
The --help command will list and thoroughly explain each of the commands.

## CREATING .ZICRORAM FILES:

A .zicroram file can be created to make it easier adding programs and/or group of programs into ram in such a way the user doesn't have to worry about creating a shell(bash/zsh) script for it.

To do this, simply create a file with an extension called '.zicroram', then make sure each line corresponds to a directory/path on your disk; finally, you can then add as much programs and data(ex.: pictures, songs, etc..) as you want in this single file. example:

    [file: ~/my_programs.zicroram]
        /usr/share/gimp
        /usr/share/gvim
        ~/Music
        ~/Pictures
        ~/Documents
    [/file]

*Note that you do not have to use the notation for file that is located between brackets: '[' and ']'.
The brackets are only meant here so that the user understands this is the contents of a file.*

Now you can add all programs using a single command:

    $ ./zicroram --add ~/my_programs.zicroram

## ADDING PROGRAMS/DATA TO RAM DURING SYSTEM STARTUP
Adding programs into ram in this specific case can be achieved by adding **'zicroram --boots ..'** inside your .bash_profile( for bash users )
or .zprofile ( for zsh users ) file:

for ZSH users:
- system wide configuration file:

        [file: /etc/zsh/zprofile]
            zicroram --boots ~/my_programs.zicroram
        [/file]

- user configuration file:

        [file: ~/.zprofile]
            zicroram --boots ~/my_programs.zicroram
        [/file]

for BASH users:
 
- system wide configuration file:

        [file: /etc/profile]
            zicroram --boots ~/my_programs.zicroram
        [/file]

- user configuration file:

        [file: ~/.bash_profile]
            zicroram --boots ~/my_programs.zicroram
        [/file]

*Note that you do not have to use the notation for file that is located between brackets: '[' and ']'.
The brackets are only meant here so that the user understands this is the contents of a file.*

The **--boots** instruction outputs to screen a copy-to-ram progress and makes the user wait for the whole process to finish,
however depending on the program and/or how fast your hard drive is, it's possible to bypass this step and avoid all the 'waiting' during system startup; 
if such is the case, then use **--bootsc** instead of **--boots** - However, currently it's not possible to check copy progress after bypassing it with such option.

Check the manual after installing for more information on --boots and --bootsc:

    $ man zicroram
        or
    $ zicroram --help-program

#### Note for non-bash and non-zsh users:
If you use something other than 'bash' and 'zsh', like 'tcsh' you'll have to search for it's system/user configuration file(s)
and do the same described here.


## USE LICENSE:

Upon program installation using **zicroram --install-wizard** the user must agree with the displayed use license;
if the user doesn't agree with one or more terms the installation will be cancelled and the user should 
give up installation of the program at once.

The sole developer doesn't take any lyability for the mistakes that may arise from using a RamDisk(or RamDrive) software;
since RAM Storage isn't a persistent type of storage, important data may be permanently lost forever with no means of recover.

If you don't agree with the USE LICENSE of this system, do not use this system.

## OPERATING SYSTEM SUPPORT:

Zicroram should work on all GNU Linux Distributions out-of-box as long as they support:

**1 - GLIBC 2.34**

**2 - TMPFS Enabled kernel.**

Zicroram runs as an administrative tool on your system, so root access through 'sudo' is required. 

'doas' still not supported in the current version of this program.

It's advisable not to run this program under Windows' WSL; last time I checked WSL didn't support real TMPFS Filesystem and instead uses the Hard Drive as TMPFS device instead of the Ram Memory thus making the program developed in here pointless.

## INSTALLATION:

Installation can be initialized through it's commandline interface(CLI): 

    $ ./zicroram --install-wizard

The program will automatically request root authorization for the user as necessary.

## AUTHOR:

The program in here was sole developed by a single dev,

get in contact with him on the email provided in the binary release of this program and also the one in here:

###### Author: Sebastião Ribeiro Monteiro Filho
###### Email: srmfsrmf@hotmail.com

## BUGS:

If you've found a bug, you're welcome to open an issue and report it in this github.
DO NOT SEND bugs or problems over email, they'll be automatically ignored and treated as junk.

## TROUBLESHOOTING:

The binary program offers a quickhand page on troubleshooting that you can read regardless if the program is installed on the system:

    $ ./zicroram --troubleshoot

This command is important as it describes most of the common issues users may have to deal with and how to either solve or avoid those problems.
