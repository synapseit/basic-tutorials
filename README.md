# Random useful Linux commands
The purpose of this page is to provide you with a list of commands that can - at some point - be useful for any specific task you are working on.  
The list is, on purpose, unordered and no specific pattern or theme is followed.

## 1. Manage kernel modules
**Show which kernel modules are currenly loaded**

Use this command to view a list of all modules which are currently loaded.

```
lsmod
```

**Load and unload kernel modules** 

```
modprobe name_of_module
```

For example, to load VMWare file sharing module called vmhgfs, you would use:

```
modprobe vmhgfs
```

To unload a module, use the -r option, as in the following example:

```
modprobe -r vmhgfs
```

## 2. Manage environment variables
**View all environment variables**

Use this command to check if an environment variable is set:

```
env
```

You can also grep for a specific variable (for example the JAVA_HOME environment variable):

```
env | grep JAVA_HOME
```


**Set (and unset) an environment variables**

You can set (called "export") an environment variable using the export command, however this is only relevant to a specific terminal session.

If you want a variable to be available across different logins, you should add the below command at the end of you your .bash_profile or .bashrc file (depending on the specific session - see [this link](https://apple.stackexchange.com/questions/51036/what-is-the-difference-between-bash-profile-and-bashrc) to understand the difference):

```
export VARNAME
```

For example, to use a HTTP and HTTPS proxy:

```
export http_proxy=http://192.168.1.30:8080
export https_proxy=http://192.168.1.30:8080
```

If you want to unset a variable, you can use the following command (keeping in mind that is also only valid for the specific terminal session you are using - see above for a persistent solution):

```
unset VARNAME
```

For example, to stop using the HTTP and HTTPS proxy we set above:

```
unset http_proxy
unset https_proxy
```

## 3. Check return codes
**View the return code of the last executed command**

This is useful when you are not sure if the return code of a program you executed was what you expected. A value of **0** usually means success:

```
echo $?
```

## 4. Create random data
**Generate random words and data**

To generate random string of a specific length, you can read from the virtual /dev/urandom device, and format/truncate the data at a specific length. You then use the head command to limit the number of strings/data you want:

For example, generate 20 alphanumeric passwords of length 8:

```
cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 8 | head -n 20
```

Generate 10 alphanumeric passwords of length 8, including chars # ? !

```
cat /dev/urandom | tr -dc 'a-zA-Z0-9!?#' | fold -w 8 | head -n 10
```

Generate 5 uppercase-only alphanumeric passwords of length 8, including chars # ? !

```
cat /dev/urandom | tr -dc 'A-Z0-9!?#' | fold -w 8 | head -n 5
```

Generate 20 lowercase-only passwords of length 8, including chars # ? !

```
cat /dev/urandom | tr -dc 'a-z0-9!?#' | fold -w 8 | head -n 20
```

Generate 10 numeric-only strings of length 8

```
cat /dev/urandom | tr -dc '0-9' | fold -w 8 | head -n 10
```

**Generate a file full of random data**

To generate a file full of random data you can still use /dev/urandom, combined with dd which will then copy to the file you want. You need to specify block size (i.e. how much data you copy from /dev/urandom) and the number of blocks to copy.  

For example, let's copy 1000 blocks of 1 MB random data to file /home/user/filename:

```
dd if=/dev/urandom of=/home/user/filename bs=1M count=1000
```

## 5. View processes

There are many ways to view the active/current processes, we give examples for htop and ps.  

**htop**

htop is more a process manager than just a process viewer. To start it, just run (install it first via apt-get or dnf/yum if needed):

```
htop
```

htop offers many features, the most important ones can be accessed by pressing:

* **F4**: filter
* **F5**: sort or tree view
* **F9**: kill a process
* **F10**: exit htop

**ps**

ps is a very powerful tool, you can use the following to get a complete view:

```
ps -ef
```

To use a tree-like view:

```
ps auxf
```
## 6. Change timezone

A very reliable way to change timezone is by creating a symlink - this involves the correct timezone file and the /etc/localtime. 

**Step 1. Find the correct timezone**:

Explore which timezone are available, and find the correct one for you. In the below example we check the European timezone:

```
cd /usr/share/zoneinfo/Europe/
ls -l
```

You will get a list of files - each representing a city/timezone. We choose Warsaw timezone.

**Step 2. Link the correct timezone to /etc/localtime**:

```
ln -s /etc/localtime /usr/share/zoneinfo/Europe/Warsaw
```
