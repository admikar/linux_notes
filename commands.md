# Linux Tools

## Utilities

**rsync**

Used to copy files and directories to a destination, similar to the  `cp`  command. However, it also allows copying to remote locations and can provide a progress bar, as is often used for backups

**# Example Usage**  
**$** rsync -vap --ignore-existing <source_file> <destination_file>**#  Key flags:**  
v = verbrose, r = recursive, p = preserve permissions, g = group, o = owner, a = archive, --progress = progresss bar

**mkpasswd**

`mkpasswd`  is a simple but very useful command, it generates a complex random password at the specified length.

**$** mkpasswd -l 8  
> iwF1g2Lo

**screen**

Screen is a full-screen window manager; it creates a single window with a shell running and allows **multiple screen  _windows_** _to run_  inside a single session. It’s most beneficial when you’re running a long task remotely and worried about your SSH session dropping and ruining everything.  **Screen will continue through disconnection**  and continue to run your commands even when the window is not visible to you.

**# Example Usage**  
**$** screen # Start a screen session  
**$** screen -ls # List running services  
**$** screen -r # Attach to session

**Ldapsearch**

If you regularly work with LDAP databases, then Ldapsearch is a must. The tool opens a connection to an LDAP server and allows you to search, find and debug entries in your database.

**# Example Usage**  
**$** ldapsearch -x -W -D <username | less**# Key Flags**  
-x = simple authentication, -W = prompt for password, -D = Use distinguished _binddn_ name to bind to LDAP directory

## Monitoring Tools

**Uptime**

Uptime returns metrics on how long a server has been running, the current time, the number of users and memory usage averages. If something goes wrong on your server, this is often the first port of call.

_‘w’ — yes, one letter. This is a fantastic combination of uptime and who commands run one after another._ `**_$_** _w_`

**Wall**

Wall is a handy command for any system administrator; it allows you to send a message to everybody’s terminal who’s currently logged into the system. This can be very useful for system-wide announcements.

**$** wall "Maintenance scheduled for 13:30"_Broadcast message from Joel@localhost: Maintenance scheduled for 13:30_

**Top**

Displays an auto-refreshing list of processes for the CPU and critical memory use and CPU usage metrics.

**$** top

**Ncdu**

The ncdu command provides a quick, convenient view for disk usage. You can use it to see what directories are using the most disk space quickly and easily.

**$** ncdu

**lsof**

lsof is a single command used for one fundamental purpose:  **L**i**S**t  **O**pen  **F**iles. This is especially useful when experiencing mounting problems that say files are being used. This command quickly identifies which files are in use by which processes.

**$** lsof

## Networking tools

**Netcat**

Netcat or  `nc`  is primarily used for port scanning but is actually a great utility networking tool for system administrators to have in their back pocket for any task. Netcat can support portscanning, file copying, port forwarding, proxy servers, and hosting servers … safe to say, it’s incredibly versatile.

**# Example Usage:**  
**$** nc -vz <host> <port> # Checks the connection between two hosts on a given port  
**$** nc -l 8080 | nc <host> 80 # Creating a proxy server

Netcat is so customisable that I can’t include all the possibilities in one post, so if you would like to see more, I’ll link my favourite Medium article on the subject below written by  [@sahityamaruvada](http://twitter.com/sahityamaruvada).

[](https://medium.com/100-days-of-linux/7-fundamental-use-cases-of-netcat-866364eb1742)

## 7 Fundamental Use-cases of Netcat

### A guide to Netcat — TCP/IP Swiss Army knife

medium.com

**NetStat**

Netstat returns various network details such as routing tables, network connections, memberships, stats, flags etc.

**# Example Usage**   
**$** netstat -a _# List all network ports_  
**$** netstat -tlpn _# List all listening ports_**# Key Flags**  
-s = Show statistics, -v = verbrose, -r = show routing tables, -i display interface table, -g = show group memeberships

**Nslookup**

Used to get information about servers on the internet or your local network. It queries DNS to find the name server information and can be useful for network debugging.

**# Example Usage**  
**$** nslookup medium.com/tags/devops**# Key Flags**  
-port = Change port number for connection, -type = Change type of query. -domain = Sets search list to _name_

**TCPDump**

Used to capture and analyse traffic coming to and from your system. It is a potent and versatile tool that specialises in debugging and troubleshooting network issues but can also be used as a security tool.

**# Example Usage**  
$ tcpdump  
$ tcpdump -i <interface> <ipaddress or hostname> <port>

# Ad-Hoc Commands

## Pretty printing API Responses

Reading JSON data from the terminal can be highly frustrating when working with APIs. As you can see below, even a small data set quickly becomes a mess when displayed to the command line making it very difficult to read.

**$** **cat** test.json  
**{**"title":"Person","type":"object","properties":**{**"firstName":**{**"type":"string"**}**,"lastName":**{**"type":"string"**}**,"age":**{**"description":"Age in years","type":"integer","minimum":0**}}**,"required":**[**"firstName","lastName"**]}**

Luckily Python has an answer. By piping your output to python we can invoke the JSON tool module. This will  _pretty print_  out JSON document which is so much easier to read and nicer on the eye.

$ **cat** test.json **|** python -m json.tool  
**{**  
    "properties": **{**  
        "age": **{**  
            "description": "Age in years",  
            "minimum": 0,  
            "type": "integer"  
        **}**,  
        "firstName": **{**  
            "type": "string"  
        **}**,  
        "lastName": **{**  
            "type": "string"  
        **}**  
    **}**,  
    "required": **[**  
        "firstName",  
        "lastName"  
    **]**,  
    "title": "Person",  
    "type": "object"  
**}**

Also worth referencing  [JQ](https://stedolan.github.io/jq/), which is a command-line JSON interface

**$** jq . file.json

## Searching through apt for available packages

**$** apt-cache seach <keyword>

## Diff the Output of any two commands

# Example usage of comparing output of two ls commands**$ diff -u <(ls -l /directory/) <(ls -l /directory/) | colordiff**

## Convert a Unix timestamp to human-readable format

**# Convert Unix timestamp to human readable**  
**$** date -d 1656685875  
F_ri, 01 Jul 2022 14:31:15 +0000_**# Current time as UNIX timestamp**  
**$** date "+%s"

## Squashing Git commits

**$** git log # See how many commits you've made  
**$** git rebase -i HEAD~x # x = number of commits you've made_# Make changes on the text editor, keeping the last commit as pick and changing the rest to sqash__# Edit the commit messages as you'd like, preferbly removing ones from previous commits_**$** git push --force-with-lease

## List all Systemd services

**$** systemctl -l -t service | less
