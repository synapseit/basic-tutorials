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

Explore which timezone are available, and find the correct one for you. In the below example we check the European timezone list:

```
cd /usr/share/zoneinfo/Europe/
ls -l
```

You will get a list of files - each file represents a city/timezone. In this example, we want to change to Warsaw timezone, and we notice that a file named **Warsaw** exists in folder /usr/share/zoneinfo/Europe:

```
usr@notebook [/usr/share/zoneinfo/Europe] ls -l
total 252
-rw-r--r--. 1 root root 2949 28 mar  2017 Amsterdam
-rw-r--r--. 1 root root 1751 28 mar  2017 Andorra
-rw-r--r--. 1 root root 1183 28 mar  2017 Astrakhan
-rw-r--r--. 1 root root 2271 28 mar  2017 Athens
-rw-r--r--. 7 root root 3687 28 mar  2017 Belfast
-rw-r--r--. 6 root root 1957 28 mar  2017 Belgrade
-rw-r--r--. 1 root root 2335 28 mar  2017 Berlin
-rw-r--r--. 2 root root 2272 28 mar  2017 Bratislava
-rw-r--r--. 1 root root 2970 28 mar  2017 Brussels
-rw-r--r--. 1 root root 2221 28 mar  2017 Bucharest
-rw-r--r--. 1 root root 2405 28 mar  2017 Budapest
-rw-r--r--. 3 root root 1918 28 mar  2017 Busingen
-rw-r--r--. 2 root root 2445 28 mar  2017 Chisinau
-rw-r--r--. 1 root root 2160 28 mar  2017 Copenhagen
-rw-r--r--. 2 root root 3559 28 mar  2017 Dublin
-rw-r--r--. 1 root root 3061 28 mar  2017 Gibraltar
-rw-r--r--. 7 root root 3687 28 mar  2017 Guernsey
-rw-r--r--. 2 root root 1909 28 mar  2017 Helsinki
-rw-r--r--. 7 root root 3687 28 mar  2017 Isle_of_Man
-rw-r--r--. 3 root root 2152 28 mar  2017 Istanbul
-rw-r--r--. 7 root root 3687 28 mar  2017 Jersey
-rw-r--r--. 1 root root 1518 28 mar  2017 Kaliningrad
-rw-r--r--. 1 root root 2097 28 mar  2017 Kiev
-rw-r--r--. 1 root root 1153 28 mar  2017 Kirov
-rw-r--r--. 2 root root 3453 28 mar  2017 Lisbon
-rw-r--r--. 6 root root 1957 28 mar  2017 Ljubljana
-rw-r--r--. 7 root root 3687 28 mar  2017 London
-rw-r--r--. 1 root root 2974 28 mar  2017 Luxembourg
-rw-r--r--. 1 root root 2637 28 mar  2017 Madrid
-rw-r--r--. 1 root root 2629 28 mar  2017 Malta
-rw-r--r--. 2 root root 1909 28 mar  2017 Mariehamn
-rw-r--r--. 1 root root 1356 28 mar  2017 Minsk
-rw-r--r--. 1 root root 2953 28 mar  2017 Monaco
-rw-r--r--. 2 root root 1544 28 mar  2017 Moscow
-rw-r--r--. 2 root root 2016 28 mar  2017 Nicosia
-rw-r--r--. 3 root root 2251 28 mar  2017 Oslo
-rw-r--r--. 1 root root 2971 28 mar  2017 Paris
-rw-r--r--. 6 root root 1957 28 mar  2017 Podgorica
-rw-r--r--. 2 root root 2272 28 mar  2017 Prague
-rw-r--r--. 1 root root 2235 28 mar  2017 Riga
-rw-r--r--. 3 root root 2692 28 mar  2017 Rome
-rw-r--r--. 1 root root 1239 28 mar  2017 Samara
-rw-r--r--. 3 root root 2692 28 mar  2017 San_Marino
-rw-r--r--. 6 root root 1957 28 mar  2017 Sarajevo
-rw-r--r--. 1 root root 1183 28 mar  2017 Saratov
-rw-r--r--. 1 root root 1490 28 mar  2017 Simferopol
-rw-r--r--. 6 root root 1957 28 mar  2017 Skopje
-rw-r--r--. 1 root root 2130 28 mar  2017 Sofia
-rw-r--r--. 1 root root 1918 28 mar  2017 Stockholm
-rw-r--r--. 1 root root 2187 28 mar  2017 Tallinn
-rw-r--r--. 1 root root 2098 28 mar  2017 Tirane
-rw-r--r--. 2 root root 2445 28 mar  2017 Tiraspol
-rw-r--r--. 1 root root 1267 28 mar  2017 Ulyanovsk
-rw-r--r--. 1 root root 2103 28 mar  2017 Uzhgorod
-rw-r--r--. 3 root root 1918 28 mar  2017 Vaduz
-rw-r--r--. 3 root root 2692 28 mar  2017 Vatican
-rw-r--r--. 1 root root 2237 28 mar  2017 Vienna
-rw-r--r--. 1 root root 2199 28 mar  2017 Vilnius
-rw-r--r--. 1 root root 1153 28 mar  2017 Volgograd
-rw-r--r--. 2 root root 2705 28 mar  2017 Warsaw
-rw-r--r--. 6 root root 1957 28 mar  2017 Zagreb
-rw-r--r--. 1 root root 2115 28 mar  2017 Zaporozhye
-rw-r--r--. 3 root root 1918 28 mar  2017 Zurich
```

**Step 2. Link the correct timezone to /etc/localtime**:

```
ln -s /etc/localtime /usr/share/zoneinfo/Europe/Warsaw
```

## 7. Change hostname

A very easy way to change hostnames is by using the hostnamectl command, which also allows to view what the current configuration is.

**Step 1. View the current hostname configuration**:

```
hostnamectl
```

This will show something like this:

```
usr@notebook [~] hostnamectl
   Static hostname: notebook
         Icon name: computer-laptop
           Chassis: laptop
        Machine ID: ard4070e15fe4d059fe493bfe14e8285
           Boot ID: 8efd3b6a96c0ef7fa65e02aef8c485aa
  Operating System: Fedora 26 (Twenty Six)
       CPE OS Name: cpe:/o:fedoraproject:fedora:26
            Kernel: Linux 4.12.13-300.fc26.x86_64
      Architecture: x86-64
```

**Step 2. Change the hostname**:

```
hostnamectl set-hostname MY_NEW_HOSTNAME
```

