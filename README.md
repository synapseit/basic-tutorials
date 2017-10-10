# Basic tutorials
Some basic Linux administration tutorials

We will go through some basic but useful tasks, which can help you in your daily system administration.

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


**Set an environment variables**

You can set an environment variable using the export command, however this is only relevant to a specific terminal session.

If you want a variable to be available across different logins, you should edit your .bash_profile or .bashrc file (depending on the specific session - see [this link](https://apple.stackexchange.com/questions/51036/what-is-the-difference-between-bash-profile-and-bashrc) to understand the difference:

```
export VARNAME
```

For example, to use a HTTP and HTTPS proxy:

```
export http_proxy=http://192.168.1.30:8080
export https_proxy=http://192.168.1.30:8080
```
