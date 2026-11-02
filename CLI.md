# CLI Notes

- man = manual (shows the help page of command)

- cd = change directory
  - cd .. = step back
  - cd ~ = root directory

- mkdir = make directory (mkdir filename)
- mv = move or rename of files and folders
- cp = copy files cp-r (recursive)

- ls = list command
  - ls -a = hidden files
  - ls -l = details of directory
  - ls -h = readable sizes
  - ls -t = sort by time
  - ls -r = reverse
  - ls -lahtr

- pwd = currernt working directory

- rm = remove files
  - rm -R = remove files from directory
  - rm -f = remove there is no undo

- chmod = changing permisssions
  1. numeric
  2. aplhabetic
  - syntax chmod 755 file

- chown = changing ownership
- sudo = admin runs
- apt = pacakge manager
- touch = creating file or updating its timestamp
- cat = display files content
- less = scroll(q=quit)
- more = page oilder simpler more forward

- tail = print last n numebr of lines
  - tail -n 4 filename

- head = print first number of lines
- rsync = instead of copy whole content again and again it only copies the difference one

---

- grep = search. finds matching lines in a files
  - grep -i = ignore case sensitive
  - grep -r = recursive
  - grep -c count

- find = locate. searches the file system by name ,type or size
  - find ~ -name "*java*"

- sort = sorting (-n numeric,-r reverse)
- date = showing date
- tree = shows directoris as a tree

- wc = word count lines
  - wc -l = counts lines
  - wc - w = words
  - wc -c = charcaters

- ps = shows processes , list running processes
- ps = shows all processes
- ps aux = show all processes
- top = monitor live view of processes ,cpu and memory

---

- df = shows disk space per file system
  - df -h = disk space readable size

- uname = shows os and kernel info
  - uname -a = for all
  - uname =m = shows system architecture

- free = memory , show ram and swap usage

- lspci = hardware info
  - lspci | grep -i audio

- kill = kill -9 pid
- pipg = rweachability of host
- ifconfig = interfaces , shows network interface and ip adresses
- ssh = remote securely logs into another machine
- xargs = turns piped input into arguments for another command
- nano = terminal text editor(ctrl + o for saves , ctrl + X for exit)
- | pipe = sends one command output as another command input
- sed = it like find and replace syntax : sed 's/old/new' filename
- awk = separates data into columns (awk '{print $1}' file.txt)
