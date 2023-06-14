# SSH Summary

## Connections, forwarding and tunneling

| Connections, forwarding and tunneling   |                           |
|-----------------------------|---------------------------------------|
| connection to remote system | `ssh username@remote.system.IP`       |
|                             | `ssh username@remote.system.IP -p PORTnbr` |
| with graphics-forwarding    | `ssh -X username@remote.system.IP`    |
|                             | `ssh -Y username@remote.system.IP`    |
| tunneling                   | `ssh -R remPort:remote_host:locPort username@remote.system.IP` |
|                             | `ssh -L locPort:remote_host:remPort username@remote.system.IP` |
|                             | `ssh -fN -[R _or_ L] port:remote_host:port username@remote.system.IP` |
| remote execution            | `ssh username@remote.system.IP "remote_cmd_to_exec"` |


## Keys
### Generation
```
ssh-keygen -t ed25519

ssh-keygen -t rsa -b 4096

# key generation with comments and specified location
ssh-keygen -t ed25519 -C "USER@laptop cluster-X" -f $HOME/.ssh/USER_clusterX_ed25519

# ssh using specific key file
ssh -i $HOME/.ssh/USER_clusterX_ed25519 USERNAME@clusterX.IP.address
```

### Transfer
```
ssh-copy-id  -i $HOME/.ssh/id_ed25519.pub  USERNAME@remote.system.ip

# copying over keys to remote system
cat $HOME/.ssh/id_ed25519.pub | ssh USERNAME@remote.system.ip "cat >> $HOME/.ssh/authorized_keys"
```

### Agent to recall key
```
ssh-add key-file
ssh-add key-file -t life
```


## Troubleshooting

### Debugging (verbose mode)
```
# -v activates the "verbose mode": resulting in printing debugging messages
# helpful in diagnosing connection, authentication, and configuration problems
# Multiple -v options increase the verbosity, the maximum is 3.

ssh -v  USERNAME@remote.system.ip
ssh -vv USERNAME@remote.system.ip
ssh -vvv USERNAME@remote.system.ip
```


---
*Last Modified: Oct. 12, 2022*  --  v 0.1
