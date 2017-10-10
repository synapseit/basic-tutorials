# Basic tutorials
Some basic Linux administration tutorials
We will go through some basic but useful tasks, which can help you in your daily system administration.

**Show which kernel modules are currenly loaded**
Use this command to view a list of all modules which are currently loaded.

```
lsmod
```

**Add and remove kernel modules** 

```
modprobe name_of_module
```

For example, to add VMWare file sharing module called vmhgfs, you would use:

```
modprobe vmhgfs
```

To remove a module, use the -r option, as in the following example:

```
modprobe -r vmhgfs
```


