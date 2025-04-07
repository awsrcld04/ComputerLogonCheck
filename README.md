
# ComputerLogonCheck

DESCRIPTION: 
- Finds and disables inactive computers
- Finds computers that have not logged in within a certain number of days
- Disables computers that have not logged in within a certain number of days
- Optional: Find and disable computers that have not been used (no login datetimestamp)

> NOTES: "v1.0" was completed in 2011. ComputerLogonCheck was written to work in on-premises Active Directory environments. The purpose of ComputerLogonCheck was/is to keep Active Directory environments "clean" for computer accounts and to help facilitate upgrades/migrations as a "clean AD" will lessen the chance for unexpected impact due to computer accounts.

## Requirements:

Operating System Requirements:
- Windows Server 2003 or higher (32-bit)
- Windows Server 2008 or higher (32-bit)

Additional software requirements:
Microsoft .NET Framework v3.5

Active Directory requirements:
One of following domain functional levels
- Windows Server 2003 domain functional level
- Windows Server 2008 domain functional level

Additional requirements:
Domain administrative access is required to perform operations by ComputerLogonCheck


## Operation and Configuration:

Command-line parameters:
- run (Required parameter)
- all (All Windows computers in the domain, servers & workstations)
- allservers (All Windows servers in the domain)
- allworkstations (All Windows workstations in the domain)

Configuration file: configComputerLogonCheck.txt
- Located in the same directory as ComputerLogonCheck.exe

Configuration file parameters:

DaysSinceDateCreated: Number of days to use to exclude computers that may have been recently created; This parameter is only used if the DisableUnusedComputers parameter is set to yes
- If not specified and the DisabledUnusedComputers parameter is set to yes, the default is 7 days

DaysSinceLastLogon: Number of days after a 14-day period (2 weeks) to use to search for computers that are not being used
- For example, specifying 16 days would add up to a total of 30 days
- If not specified, the default is a total of 21 days

DisableUnusedComputers (yes | no): Determines if ComputerLogonCheck will disable accounts that have not been used
- If yes, the DaysSinceDateCreated parameter is used.
- If not specified, the default is no

Exclude: Exclude one or more computers by specifying the desired computer on a separate line

ExcludePrefix: Exclude one or more computers using a prefix that will match the desired computers(s)

ExcludeSuffix: Exclude one or more computers using a suffix that will match the desired computers(s)

Output:
- Located in the Log directory inside the installation directory; log files are in tab-delimited
format
- Path example: (InstallationDirectory)\Log\

Additional detail:
- ComputerLoginCheck also references the date that the computer’s password was changed. ComputerLoginCheck checks to ensure the password has been set within the last 45 days. Changing the computer password (technically called the machine account password) is an automatic process that does not and should not require manual intervention.
- ComputerLoginCheck will automatically exclude all Domain Controllers in the domain.
- The DisableUnusedComputers parameter refers to computers that do not have the lastLogonTimestamp and operatingSystem attributes.
