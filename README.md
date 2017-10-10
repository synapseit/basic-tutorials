# Random useful Linux commands
Some random (but useful) Linux commands

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
**View the exit code of the last executed command**

This is useful when you are not sure if the return code of a program you executed was what you expected. A value of **0** usually means success:

```
echo $?
```

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
