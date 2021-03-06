---
title: bash.cheatsheet

date: 2020-11-14T19:07:13+01:00
---#-#
#-# Variables
#-#

#-# String manipulation

Command                                    Description
-------                                    -----------
${varname:-word}                           If varname exists and isn't null, return its value; otherwise return word
${varname:=word}                           If varname exists and isn't null, return its value; otherwise set it word and then return its value
${varname:?message}                        If varname exists and isn't null, return its value; otherwise print varname, followed by message and abort the current command or script
${varname:+word}                           If varname exists and isn't null, return word; otherwise return null
${varname:offset:length}                   Performs substring expansion. It returns the substring of $varname starting at offset and up to length characters

${variable#pattern}                        If the pattern matches the beginning of the variable's value, delete the shortest part that matches and return the rest
${variable##pattern}                       If the pattern matches the beginning of the variable's value, delete the longest part that matches and return the rest
${variable%pattern}                        If the pattern matches the end of the variable's value, delete the shortest part that matches and return the rest
${variable%%pattern}                       If the pattern matches the end of the variable's value, delete the longest part that matches and return the rest
${variable/pattern/string}                 The longest match to pattern in variable is replaced by string. Only the first match is replaced
${variable//pattern/string}                The longest match to pattern in variable is replaced by string. All matches are replaced

${#varname}                                Return the length of the value of the variable as a character string

*(patternlist)                             Match zero or more occurences of the given patterns
+(patternlist)                             Match one or more occurences of the given patterns
?(patternlist)                             Match zero or one occurence of the given patterns
@(patternlist)                             Match exactly one of the given patterns
!(patternlist)                             Match anything except one of the given patterns


#-# Arrays




#-#
#-# Functions
#-#



#-#
#-# Input/Output Redirection
#-#

Command                                    Description
-------                                    -----------
cmd1|cmd2                                  Pipe; takes standard output of cmd1 as standard input to cmd2
> file                                     Directs standard output to file
< file                                     Takes standard input from file
>> file                                    Directs standard output to file; append to file if it already exists
>|file                                     Forces standard output to file even if noclobber is set
n>|file                                    Forces output to file from file descriptor n even if noclobber is set
<> file                                    Uses file as both standard input and standard output
n<>file                                    Uses file as both input and output for file descriptor n
<<label                                    Here-document
n>file                                     Directs file descriptor n to file
n<file                                     Takes file descriptor n from file
n>>file                                    Directs file description n to file; append to file if it already exists
n>&                                        Duplicates standard output to file descriptor n
n<&                                        Duplicates standard input from file descriptor n
n>&m                                       File descriptor n is made to be a copy of the output file descriptor
n<&m                                       File descriptor n is made to be a copy of the input file descriptor
&>file                                     Directs standard output and standard error to file
<&-                                        Closes the standard input
>&-                                        Closes the standard output
n>&-                                       Closes the ouput from file descriptor n
n<&-                                       Closes the input from file descripor n


#-#
#-# Process management
#-#

Process Management

Command                                    Description
-------                                    -----------
ps                                         Show snapshot of processes
top                                        Show real time processes
kill <pid>                                 Kill process with id pid
pkill <name>                               Kill process with name name
killall <name>                             Kill all processes with names beginning name



#-#
#-# Filesystem
#-#

#-# System directories

Directory                                  Description
---------                                  -----------
/bin                                       Binaries (executables). Basic system programs and utilities (such as bash).
/usr/bin                                   More system binaries.
/usr/local/bin                             Miscellaneous binaries local to the particular machine.
/sbin                                      System binaries. Basic system administrative programs and utilities (such as fsck).
/usr/sbin                                  More system administrative programs and utilities.
/etc                                       Systemwide configuration scripts.
/etc/rc.d                                  Boot scripts, on Red Hat and derivative distributions of Linux.
/usr/share/doc                             Documentation for installed packages.
/usr/man                                   The systemwide manpages.
/dev                                       Device directory. Entries (but not mount points) for physical and virtual devices. See Chapter 29.
/proc                                      Process directory. Contains information and statistics about running processes and kernel parameters. See Chapter 29.
/sys                                       Systemwide device directory. Contains information and statistics about device and device names. This is newly added to Linux with the 2.6.X kernels.
/mnt                                       Mount. Directory for mounting hard drive partitions, such as /mnt/dos, and physical devices. In newer Linux distros, the /media directory has taken over as the preferred mount point for I/O devices.
/media                                     In newer Linux distros, the preferred mount point for I/O devices, such as CD/DVD drives or USB flash drives.
/var                                       Variable (changeable) system files. This is a catchall "scratchpad" directory for data generated while a Linux/UNIX machine is running.
/var/log                                   Systemwide log files.
/var/spool/mail                            User mail spool.
/lib                                       Systemwide library files.
/usr/lib                                   More systemwide library files.
/tmp                                       System temporary files.
/boot                                      System boot directory. The kernel, module links, system map, and boot manager reside here.


#-# System files

File                                       Description
----                                       -----------
/etc/fstab (filesystem table)
/etc/mtab (mounted filesystem table)
/etc/inittab files.



#-#
#-# Package management
#-#

#-# Advanced Packaging Tool (apt)

Command                                    Description
-------                                    -----------
apt-get install <package-name>             Install specified package(s), along with any dependencies.
apt-get remove <package-name>              Removes specified package(s), but don't remove dependencies.
apt-get autoremove                         Remove 'orphaned' dependencies which are installed but are not used by any apps.
apt-get clean                              Remove downloaded package files (.deb) for software that is already installed.
apt-get purge [package-name]               Remove and clean a specific package. (also removes configuration files)
apt-get update                             Read /etc/apt/sources.list and update the system’s database of available packages.
apt-get upgrade                            Upgrade all packages if there are updates available.
apt-cache search <package-name>            Find out the name of a package that you know is in the system.
apt-cache show <package-name>              Show details about a package, including description, dependency info and version numbers.
apt-cache depends <package name(s)>        List the packages that the specified packages depends upon in a tree.
apt-cache rdepends <package name(s)>       Generate and output the list of packages that depend upon the specified package.
apt-cache pkgnames                         Generate a list of the currently installed packages on your system.


#-# Debian Package Manager (dpkg)

Command                                    Description
-------                                    -----------
dpkg -i <package-file-name.deb>            Install a .deb file.
dpkg --list [search-pattern]               List packages currently installed on the system.
dpkg --configure                           Run a configuration interface to set up a package.
dpkg-reconfigure                           Run a configuration interface on an already installed package.


#-# Yellow Dog Updater, Modified (yum)

Command                                    Description
-------                                    -----------
yum install <package-name(s)>              Install the specified package(s) along with any required dependencies.
yum erase <package-name(s)>                Remove the specified package(s) from the system.
yum search <search-pattern>                Search the list of package names and descriptions for packages that match the search pattern.
yum deplist <package-name>                 Listing all the libraries and modules that the named package depends on.
yum check-update                           Refreshe the local cache of the yum database.
yum info <package-name>                    Display information about the specified package.
yum reinstall <package-name(s)>            Erase and re-install the specified package on your system.
yum localinstall <local-rpm-file>          Check the dependencies of an .rpm file and then install it.
yum update <optional-package-name>         Download and install all updates including bug fixes, security releases, and upgrades.
yum upgrade                                Upgrade all packages installed in your system to the latest release.


#-# RPM package manager (rpm)

Command                                    Description
-------                                    -----------
rpm --install --verbose --hash <file.rpm>  Install an rpm from the file. (rpm -ivh [filename].rpm)
rpm --erase <packag-name>                  Removes the given package. (rpm -e)
rpm --query --all                          List the names of all packages currently installed. (rpm -qa)
rpm --query <package-name>                 Confirm or deny if a given package is installed in your system. (rpm -q)
rpm --query --info <package-name>          Display information about an installed package. (rpm -qi)
rpm --query --list <package-name>          List files installed by a given package. (rpm -ql)
rpm --query --file                         Check to see what installed package “owns” a given file.



#-#
#-# Job Scheduling
#-#

#-# Crontab command

Command                                    Description
-------                                    -----------
crontab -e <file>                          Edit a crontab, or create it if it doesn’t exist.
crontab -u <user> -e <file>                Edit a crontab as the specified user.
crontab -l <file>                          Display crontab on standard output.
crontab -r <file>                          Remove crontab.
crontab -v <file>                          Display the last time the crontab was edited.


#-# Syntax

* * * * * <command-to-be-executed>
│ │ │ │ │
│ │ │ │ └─ day of the week (0-6) (sunday = 0)
│ │ │ └─ month (1-12)
│ │ └─ day of month (1 - 31)
│ └─ hour (0 - 23)
└─ min (0-59)


#-# Special characters

Character             Example              Description
---------             -------              -----------
*                     *                    Specify any occurrence of the field.
,                     0,15                 Specify 2 or more times of execution.
-                     0-59                 Specify any time within a range.
/                     */15                 Can be used with a range or wild card to run at a specified interval.


#-# Examples

Crontab                                    Description
-------                                    -----------
* * * * *             <command>            Every minute of every day.
*/15 * * * *          <command>            Every 15 minutes of every day.
03-59/5 02 * * *      <command>            Every 5 minutes of the 2 am hour starting at 2:03.
0 * * * *             <command>            Every day at midnight.
0 */12 * * *          <command>            Twice a day.
02 * * * 1-5          <command>            Every weekday at 2 am.
02 * * * 6,7          <command>            Weekends at 2 am.
0 02 15 * *           <command>            Once a month on the 15th at 2 am.
0 02 */2 * *          <command>            Every 2 days at 2 am.
0 02 1 */2 *          <command>            Every 2 months at 2 am on the 1st.



