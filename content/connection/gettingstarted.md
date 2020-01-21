---
title: "Getting Started"
date: 2020-01-06T17:22:32Z
---

This section presents some ways to connect and interact with the cluster.

## Login Nodes
You can connect to Bob using the public login node. Please note that only incoming connections are allowed in the whole cluster. The login node is:

```bash
ul-01.bob.macc.fct.pt
```

## SSH

Secure Shell (SSH) is a cryptographic network protocol designed for network services securely over an unsecured network. Typical applications include remote command-line, login, and remote command execution. This is the protocol used to access the HPC cluster.

### Checking if you have an SSH key

If you don't already have an SSH key, you must generate one. If you don't know whether you have already have one, you can check by using the following command to check if existing SSH keys are present:

```bash
# Lists the files in your .ssh directory, where by default are the SSH keys
$ ls -la ~/.ssh
```

Check if you already have a public SSH key. By default, the filenames of the public keys are appended with '.pub'.

### I do have an SSH key

In case that you already have an SSH key, you can follow to the next chapter where you will learn to [connect yourself to the cluster](#head1234).

### I don't have an SSH key

The obvious first step is to create an SSH key. Use the following command to create it:

```bash
$ ssh-keygen -t rsa -b 4096
```

The options -t and -b where respectively used for specifying the type of key to create, and the key size in bytes.

This command will prompt you with "Enter a file on which to save the key". Press Enter, to accept the default file location.

After, you will be prompted to type a password. Choose a strong password, type it and you are done. In the next chapter you will learn how to [connect yourself to the cluster](#head1234)).


## SCP

Secure Copy Protocol (SCP) is a protocol created to securely transfer files between a local host and a remote host. SCP uses Secure Shell (SSH) for data transfer and authentication, thus, ensuring the authenticity and confidentiality of the data in transit.


### From a local directory to a remote directory

In case you want to transfer a dataset or a program to the remote host, you can use the following syntax:

```bash
$ scp /path/to/your/file user@ul-01.bob.macc.fct.pt:remoteDirectory/targetFile
```

An example where the user (_'johnDoe'_) would transfer a file named _'parameters.csv'_ to a remote host (with the address _'ul-01.bob.macc.fct.pt'_ as the user _'John'_) would result in the following command:

```bash
$ scp /home/johnDoe/Desktop/parameters.csv John@ul-01.bob.macc.fct.pt:/home/John/parameters.csv
```

### From a remote directory to a local directory

Suppose that you just finished running your application on the cluster and want to transfer the results from it to your laptop. The syntax would be almost the same of the previous command:

```bash
$ scp user@ul-01.bob.macc.fct.pt:remoteDirectory/sourceFile /path/to/your/location
```

Using the same parameters as the previous example, a file transfer from a remote directory to your machine would be such as:

```bash
$ scp John@ul-01.bob.macc.fct.pt:/home/John/parameters.csv  /home/johnDoe/Desktop/parameters.csv 
```

### Useful flags

**-r**
 - Sometimes you want to copy a whole directory instead of a single file. This can be achieved using the '-r' flag. Copying a remote directory to your laptop would follow the syntax below:

```bash
$ scp -r user@ul-01.bob.macc.fct.pt:/directoryToCopy  /path/to/your/location
```

**-P**
 - If the remote host uses another port other than the default of 22, you can specify which port to use with the flag '-P'. For example: when copying a file from a remote directory:

```bash
$ scp -P 2222 user@ul-01.bob.macc.fct.pt:/directory  /path/to/your/location
```

**-i**
 - If you have multiple identity files you can choose which one to use with the flag _-i_:

```bash
$ scp -i /path/to/identity/file user@ul-01.bob.macc.fct.pt:/directoryToCopy  /path/to/your/location
```

## RSync

In case you are connected through an slow and unreliable network and you want to transfer a big file, you should opt for RSync. This protocol is used for efficiently transfer and synchronize files between your computer and an external host. It follows the same syntax as SCP, being is generic syntax:

```bash
$ rsync  /path/to/your/file user@host:/directoryTarget 
```

### From a local directory to a remote directory

An example on how to transfer a local file to a remote directory:

```bash
$ rsync /home/johnDoe/Desktop/parameters.csv John@ul-01.bob.macc.fct.pt:/home/John/parameters.csv
```

### From a remote directory to a local directory

Now, the opposite case from the previous example, where you want to transfer a remote file to your laptop
```bash
$ rsync John@ul-01.bob.macc.fct.pt:/home/John/parameters.csv  /home/johnDoe/Desktop/parameters.csv 
 ```

### Useful flags

**-r**
 - As in SCP, you can use the '-r' flag to transfer a folder instead of a single file. A small example using this flag would use the following syntax:

```bash
$ rsync -r John@ul-01.bob.macc.fct.pt:/home/John/results/  /home/johnDoe/Desktop/ 
```

This utility has a more flags that can be found on is [documentation](https://download.samba.org/pub/rsync/rsync.html).

## Repository management (GIT/SVN)

There’s no outgoing internet connection from the cluster, which prevents the use of external repositories directly from our machines. To circumvent that, you can use the “sshfs” command in your local machine.

Doing that, you can mount a desired directory from our Lustre filesystem in your local machine. That way, you can operate your Lustre files as if they were stored in your local computer. That includes the use of git, so you can clone, push or pull any desired repositories inside that mount point and the changes will transfer over to Lustre.

### Setting up sshfs
Create a directory inside your local machine that will be used as a mount point.

Run the following command below, where the local directory is the directory you created earlier. Note that this command mounts your Lustre home directory by default.

```bash
$ sshfs -o workaround=rename <yourHPCUser>@ul-01.bob.macc.fct.pt: <localDirectory>
```

From now on, you can access that directory. If you access it, you should see your home directory of the Lustre filesystem. Any modifications that you do inside that directory will be replicated to the Lustre filesystem inside the HPC machines.

Inside that directory, you can call “git clone”, “git pull” or “git push” as you please.