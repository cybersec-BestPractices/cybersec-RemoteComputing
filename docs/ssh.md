
## Keys Generation

### Basic SSH-Keys Generation
#### NIST's standard recommendations for ssh keys encryption algorithms
| Encryption Algorithm  | Key length | Key generation command |
|-----------------------|------------|------------------------|
| ECDSA, EdDSA, DH, MQV | f=224-255 (and above) | `ssh-keygen -t ed25519` |
| RSA                   | k=2048 (and above)    | `ssh-keygen -t rsa -b 4096` |


```sh
# generate keys using ed25519
ssh-keygen -t ed25519

# generate keys using rsa
ssh-keygen -t rsa -b 4096
```

```sh
# copying over keys to remote system
cat $HOME/.ssh/id_ed25519.pub | ssh USERNAME@remote.system.ip "cat >> $HOME/.ssh/authorized_keys"
# alternatively one would use the ssh-copy-id command
ssh-copy-id -i $HOME/.ssh/id_ed25519.pub USERNAME@remote.system.ip
```

A typical output of the process of keys' generation would look like this,
```sh
$ ssh-keygen -t ed25519
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/USERNAME/.ssh/id_ed25519): $HOME/.ssh/system1_id_ed25519
Enter passphrase (empty for no passphrase):  *******************************************
Enter same passphrase again:  *******************************************
Your identification has been saved in system1_id_ed25519.
Your public key has been saved in system1_id_ed25519.pub.
The key fingerprint is:
SHA256:VrKTrH2EX+52KoKVbtIcPnzRlf21jo0vZU/Wf4IysjI local.USERNAME@local.machine
The key's randomart image is:
+--[ED25519 256]--+
|                 |
|                 |
|        . .    o |
|       . *    o o|
|        S.....  =|
|       +++.o.  +=|
|      .O..o...Boo|
|      E @.=.o+oo+|
|       =.* =oooo.|
+----[SHA256]-----+
```

The next step would be to transfer the public part of recently generated key
to the remote system,
```sh
$ ssh-copy-id -i $HOME/.ssh/system1_id_ed25519.pub USERNAME@remote.system.ip
```


## Keys Management
```sh
# transfer/copy keys to remote system
ssh-copy-id  -i $HOME/.ssh/id_ed25519.pub  USERNAME@remote.system.ip

# use of an specific key to access clusterX
ssh -i $HOME/.ssh/USER_clusterX_ed25519 USERNAME@clusterX.IP.address

# use of an specific key to access clusterY
ssh -i $HOME/.ssh/USER_clusterY_ed25519 USERNAME@clusterY.IP.address

# use of an specific key for remote access to clusterZ
ssh -i $HOME/.ssh/USER_clusterZ_ed25519 USERNAME@clusterZ.IP.address
```



#### Adding Comments to your keys
One useful fearure offered by the key generation comamand is the capability to associate comments to key,
so that they can be used to remind us what a given key is being used fo
. Comments can be added to the key when created using the `-C` flag.
For instance,
```sh
# key generation with comments and specified location
ssh-keygen -t ed25519 -C "USER@laptop cluster-X" -f $HOME/.ssh/USER_clusterX_ed25519
```
in this case, both the comment and the name for the keys files is being specified by
the respective `-C` and `-f` flags.
If one would like to modify the comment of an existent key, the `-c` (lower-case "c") flag can be used instead.


#### Using `ssh-agent` to remember your keys
Keys are quite powerful, they can substantially improve security and
efficiency at the moment of connecting to work in remote systems.
One really useful feature to help with productivity is requesting an
ssh-agent program to recall our keys/passphrases combinations,
in this way when a key is used to connect to a given system the
*ssh-agent* will remember the passphrase entered for a given period of time
avoiding to repeatedly prompt for it.
The way to trigger this feature is to use `ssh-add key-file`.
It is also possible to specify a timeout period (lifetime) for how long to remember the passphrase, using the `-t` flag.

#### Some additional ssh-agent commands
| ssh-agent command | description |
|-------------------|-------------|
| `ssh-add -l`      | Lists fingerprints of all identities currently represented by the agent |
| `ssh-add -D`      | Delete all identities from the agent |
| `ssh-add -t life` | Sets the maximum time the agent will keep the given key |


#### Customizing SSH keys names
It is possible to specify the name of the file where to store the keys when generating them.
By default ssh will search for predefined file names, such as `id_ed25519` or `id_rsa`.
But if we are using a different name, then we should indicate ssh which file we are using as keys.
For doing so, we will use the `-i` flag followed by the location (which is also standardized under `$HOME/.ssh`)
and the actual filename. E.g.
```sh
# ssh using specific key file
ssh -i $HOME/.ssh/USER_clusterX_ed25519 USERNAME@clusterX.IP.address
```


#### Configuration Details
The preevious process can be simplified even a bit more, by adding some of theese details to the configuration file used by ssh.
Such a configuration file resides in the `$HOME/.ssh/` directory and is named `config`.
An example of an entry in this file is shown below,

##### Single Host
```sh
HOST clusterX
     HostName clusterX.IP.address
     User USERNAME
     IdentityFile ~/.ssh/USER_clusterX_ed25519
```

##### Multiple Hosts
One could even envision the possibility of including mutliple hosts by adding
entries in the `~/.ssh/config` file.
```sh
HOST clusterX
     HostName clusterX.IP.address
     User USERNAMEonclusterX
     IdentityFile ~/.ssh/USER_clusterX_ed25519

HOST clusterY
     HostName clusterY.IP.address
     User USERNAMEonclusterY
     IdentityFile ~/.ssh/USER_clusterY_ed25519

HOST clusterZ
     HostName clusterZ.IP.address
     User USERNAMEonclusterZ
     IdentityFile ~/.ssh/USER_clusterZ_ed25519
```
in this way, the user would just use the commands `ssh clusterX` or `ssh clusterY` for connecting to any of the corresponding remote systems.


## Troubleshooting Keys Configurations
A couple of options to consider when finding troubles with the keys setup in a remote system can be generically considered.

Firstly, if for what ever reason the ssh-copy-id command is not found or available in the local system where the keys were generated, an alternative way to transfer the public key to the remote system could be achieved by using the following command,
```sh
cat $HOME/.ssh/id_ed25519.pub | ssh USERNAME@remote.system.ip "cat >> $HOME/.ssh/authorized_keys"
```
this assumes that the public key named `id_ed25519.pub` is located at `$HOME/.ssh/` directory and it will be placed in the `remote.system.ip` space of a user named `USERNAME`.


### Permission Attributes
Another issue that may arise when transferring the private keys, is related to an improper setup of the file permissions. The `$HOME/.ssh` directory must only be accessible by the owner, and the various key files must not be writable (or in some cases, readable) by anyone else. This is how the `$HOME/.ssh` directory should look like,

```sh
# look at ~/.ssh permissions
ls -ld $HOME/.ssh

drwx------ 2 USERNAME GROUPNAME 7 Aug  9 15:43 /home/USERNAME/.ssh
```

To fix improper set permissions, the following command may be used:
```sh
# fix permissions in ~/.ssh
chmod -R go= $HOME/.ssh/
```


## Debugging/Verbose Mode
Additionally, if we find problems when trying to ssh into a system which we either know the authentication procedure (either keys, password, or MFA) is not behaving or working as expected, we can use the following options when using the ssh command to obtain more verbose detail of the connections,
```sh
# -v activates the "verbose mode": resulting in printing debugging messages
# helpful in diagnosing connection, authentication, and configuration problems
# Multiple -v options increase the verbosity, the maximum is 3.

ssh -v USERNAME@remote.system.ip
ssh -vv USERNAME@remote.system.ip
ssh -vvv USERNAME@remote.system.ip
```


##  Multiplexing: `ControlMaster`
Multiplexing is the ability to send more than one signal over a single line or connection. In OpenSSH, multiplexing can re-use an existing outgoing TCP connection for multiple concurrent SSH sessions to a remote SSH server, avoiding the overhead of creating a new TCP connection and **reauthenticating each time**.

ssh has an option called `ControlMaster` that enables the sharing of multiple sessions over one single network connection.
This means that you can connect to the remote system once, enter your credentials, and have all other subsequent ssh sessions utilizing the initial connection without need for re-authentication.
It is possible to establish this `ControlMaster` setup manually each time on the command line, but instead it's easiest to put it in the ssh client configuration file so that it applies every time that a connection is launched to the corresponding system.

```sh
HOST clusterX
     HostName clusterX.IP.address
     User USERNAMEonclusterX
     IdentityFile ~/.ssh/USER_clusterX_ed25519
     ControlMaster auto
     ControlPath ~/.ssh/controlmasters/%r@%h:%p
```

When ssh is instructed to use `ControlMaster`, it will look for the special file (a socket) in the `~/.ssh/controlmasters/` directory that is maintaining a connection to the cluster. If it already exists and is open, it'll use it to create a connection without re-authenticating; if it doesn't exist, it'll authenticate and create the file for subsequent use.

Note that all subsequent connections are dependent on the initial connection — if you exit or kill the initial connection all other ones die, too.
This can obviously be annoying if it happens accidentally. It's easily avoided by setting up a master connection in the background:
```sh
ssh -CX -o ServerAliveInterval=30 -fN remoteServer
```
in this case the `-fN` flag puts the process in background and sit idle, after authenticating;
`-C` is for using compression and `X` for X-forwarding,
`ServerAliveInterval` is used to specify a time interval to keep the sessions open when inactive.


## Tunneling
In tunneling, or port forwarding, a local port is connected to a port on a remote host or vice versa. So connections to the port on one machine are in effect connections to a port on the other machine.

Typically the options `-f` (go to background), `-N` (do not execute a remote program) and `-T` (disable pseudo-tty allocation) can be useful for connections that are used only for creation of tunnels.

In regular port forwarding, connections to a local port are forwarded to a port on a remote machine.
This is a way of **securing an insecure protocol or of making a remote service appear as local**.

```sh
ssh -L localPortNbr:localhost:remotePortNbr -l username remote.server.ip
```

In that way connections on the local machine made to the forwarded port will in effect be connecting to the remote machine.

An application of this is the usual utilization of ssh-tunnels to establish VNC connections to remote locations.



---

# References:
  - https://en.wikibooks.org/wiki/OpenSSH

---
