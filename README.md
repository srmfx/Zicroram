# Zicroram
Zicroram's Official Shareware Github.

## TOPICS

[ABOUT](#about)

[ABOUT THIS SHAREWARE VERSION](#about-this-shareware-version)

[CURRENT LIMITATIONS](#current-limitations)

[DOWNLOADING](#downloading)

[INSTALLATION](#installation)

[UNINSTALLATION](#uninstallation)

[UPDATE](#update)

[HOW IT WORKS](#how-it-works)

[CREATING ZICRORAM FILES](#creating-zicroram-files)

[RESTORING DATA FROM POWER BLACKOUTS, SYSTEM CRASHES OR FREEZES](#restoring-data-from-power-blackouts-system-crashes-or-freezes)

[ADDING PROGRAM/DATA TO RAM ON SYSTEM STARTUP](#adding-programsdata-to-ram-during-system-startup)

[USE LICENSE](#use-license)

[OPERATING SYSTEM SUPPORT || SYSTEM REQUIREMENTS](#operating-system-support--system-requirements)

[AUTHOR](#author)

[BUGS](#bugs)

[TROUBLESHOOTING](#troubleshooting)


## ABOUT:
Zicroram is a C/C++ Ramdisk Command-Line Tool for Linux TMPFS/RAMFS that adds further ramdrive capabilities:

1 - Adding(Synchronously and Assynchronously) Data to RAM(**--add** or **--addc**)

2 - Checking Status (**--usage** or **--usagel**)

3 - Removing Data from RAM(**--remove-all** or **--remove**)

4 - Restoring Data from DISK Back into RAM (**--restore**)

5 - Backing up data from RAM Into disk (**--mmbackup** and **--mtbackup**)

6 - Copying programs on system bootup (**--boots** or **--bootsc**)

7 - More instructions & commands (**--help**, **--help-setup**, **--help-program**, **--help-info**)

8 - Troubleshoot (**--troubleshoot**)

The program also includes a man page, you can read it once the program is installed on the system: 

    $ man zicroram
    
## ABOUT THIS SHAREWARE VERSION
The use of the shareware version here available is limited to 15GB of RAM. You can keep using this program indefinitely, by simply removing programs and freeing up space. Full version features no limitations, however full version isn't yet available to public use.

The shareware limitation is only imposed on the tool(zicroram) side; which means no limitation is ever set on the Linux Operating System nor on the TMPFS/RAMFS Kernel Modules and none of it's configuration files.

## CURRENT LIMITATIONS

- Reflink file support is non-existent; currently, neither TMPFS nor RAMFS supports CoW/Reflink data; in other words as of this date it'd be impossible to give it support today. However, this is only a problem when doing DATA BACKUPS using '--mmbackup', '--mtbackup', '--mmremove' after changing/editing/updating the reflinked file in RAM. If no editing of reflinked files takes places, then doing DATA BACKUPS isn't a problem and should be fine. When a reflinked file is copied to RAM using this program and a DATA BACKUP is realized on the reflinked file due to changes/moddifications, then reflinking/cow on the file will be lost when copied to disk.
- When adding directories to RAM using this program, Hard Linked files located inside the given directory tree will only keep their Hard Link reference for hard linked files located inside this same directory tree structure when doing DATA BACKUPS with either '--mmbackup', '--mtbackup', '--mmremove'. This means hard linked files that are located outside the directory tree structure will lose their hard link reference upon backup; HOWEVER, none of the files are actually lost and the hard link reference loss only happens if the hard linked file is updated/changed/edited in RAM and only for the file located outside the directory tree structure; Hard Link References for files inside the same directory tree structure will be kept after a DATA BACKUP; If NO hard-linked files are changed AT ALL, then doing DATA BACKUPS should be 100% safe.
- If a single hard-linked or reflinked/cow'd file is added to RAM(instead of an entire directory), either hard link or reflink reference will be lost upon doing backups using '--mmbackup', '--mtbackup', '--mmremove' and only after it has been edited/changed/updated in RAM. If the file hasn't been edited/changed/updated while in RAM, doing backups shouldn't be a problem since no data differences will be found and nothing will be backed up to DISK in this case.

**About Current Limitations:** About reflinks/CoW'd files not being supported on TMPFS/RAMFS, there's nothing that can currently be done.

**Workaround:** If you really need to work with reflinked/cow'd files, you can still write your own backup tool(s) for it, creating and reflinking wherever necessary.

## DOWNLOADING
At the far right side of the screen - at the top of this page - you'll find a 'RELEASE' section and once you click in it, you'll then be taken to a page describing the version and changes made to the program on that version. At the 'Assets' section of that page, you can download the program under the name " zicroram.x86-64.glibc.tar.gz "; the '.tar.gz' is a tar compressed file and after downloading it, it'll need to be uncompressed using the 'tar' tool:

Extracting into current directory:

    $ tar xvf ./zicroram.tar.gz;

or, extracting in a new directory:

    $ mkdir ./new_dir;
    $ tar xvf ./zicroram.tar.gz -C ./new_dir;

## INSTALLATION

Installation can be realized through it's commandline interface(CLI) through any terminal emulator installed on your linux distribution : 

    $ ./zicroram --install-wizard

The program will automatically request root authorization for the user if necessary.

## UNINSTALLATION

Uninstallation can only be done once after the program is fully installed :

    $ zicroram --uninstall

If you go through problems during uninstallation, make sure you close any programs that you might be running after adding them to RAM using zicroram.

## UPDATE

Program can easily be updated whenever a new version exists server-side:

    $ zicroram --update

## HOW IT WORKS
The program works by creating and mounting a TMPFS device called /zicroram/ and allowing the user to add any data through a simple command, like for example:

    $ zicroram --add ~/Pictures ~/Music ~/Downloads

After this the program will symlink the real path where the data was located to the newly created TMPFS mounted device allowing the user to call on his data as if it were still on the disk. The real data will be renamed to keep it safe from power blackouts and system crashes until either a --remove or --restore command is used.

In case of system crash or power blackout, once your system reboots, data can be easily restored to real data path using

    $ zicroram --restore
The above command will put the original files back in place where the symlinks were created.

Many more commands can be found by typing: 

    $ zicroram --help    
The --help command will list and thoroughly explain each of the commands.

## CREATING .ZICRORAM FILES

A file with a .zicroram extension can be optionally created to make it easy adding programs and/or group of programs into ram in such a way the user doesn't have to worry about creating a shell(bash/zsh) script.

To do this, simply create a file with an extension called '.zicroram', then make sure each line corresponds to a directory or file of your choice; you can then add as much data(ex.: pictures, songs, etc..) as you want in this single file. example:

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
    
## RESTORING DATA FROM POWER BLACKOUTS, SYSTEM CRASHES OR FREEZES
With the --restore instruction it's possible to recover previously existing data that is still located on the disk;
however, it's important to understand that changes that might have been made while data was into ram is now permanently lost at this point:

    $ zicroram --restore

Restore is only possible, because zicroram renames the original data before creating a symlink and copying the desired program(or data) into ram;
the **--restore** instruction will simply remove the symlink(s) that have been created then it'll move and rename the original data back to where it originally was.

because of this, do not forget to use **--mmbackup** or **--mtbackup** if you need to.

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

## USE LICENSE

Upon program installation using **zicroram --install-wizard** the user must agree with the displayed use license;
if the user doesn't agree with one or more terms the installation will be cancelled and the user should 
give up installation of the program at once.

The sole developer doesn't take any lyability for the mistakes that may arise from using a RamDisk(or RamDrive) software;
since RAM Storage isn't a persistent type of storage, important data may be permanently lost forever with no means of recover.

If you don't agree with the USE LICENSE of this program, do not use it! You've been warned.

## OPERATING SYSTEM SUPPORT || SYSTEM REQUIREMENTS

Zicroram should work on all GNU Linux Distributions out-of-box as long as they support:

**1 - GLIBC 2.34 or greater version**

**2 - TMPFS Enabled kernel.**

Zicroram runs as an administrative tool on your system, so administrator/root access will be required.

It's advisable not to run this program under Windows' WSL; last time I checked WSL didn't support real TMPFS Filesystem and instead uses the Hard Drive as TMPFS device instead of the Ram Memory thus making the program developed in here pointless.


## AUTHOR

The program in here was sole developed by a single dev,

get in contact with him on the email provided in the binary release of this program and also the one in here:

###### Author: Sebastião Ribeiro Monteiro Filho
###### Email: srmfsrmf@hotmail.com

<p align="center">
  <img src="https://github-profile-trophy.vercel.app/?username=srmfx&theme=onedark&rank=SECRET,SSS,SS,S,AAA,AA,A&row=1&column=-1"/>
</p>

## BUGS

If you've found a bug, you're welcome to open an issue and report it in this github.
DO NOT SEND bugs or problems over email, they'll be automatically ignored and treated as junk.

## TROUBLESHOOTING

The binary program offers a quickhand page on troubleshooting that you can read regardless if the program is installed on the system:

    $ ./zicroram --troubleshoot

This command is important as it describes most of the common issues users may have to deal with and how to either solve or avoid those problems.
