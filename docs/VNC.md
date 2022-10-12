# Virtual Network Computing (VNC)
  - is a graphical desktop-sharing system that uses the Remote Frame Buffer protocol (RFB) to remotely control another computer
  - more efficient and selective way to display graphics from a remote connection
  - it requires the implementation of a *tunnel* or the remote host to allow connections to given ports.

## Set up a VNC connection 

 1. ssh into the remote server, e.g.
    ```sh
    ssh userName@remote.server.ip
    ```
2. launch a VNC server in the remote host, e.g. `vncserver`
3. Check with `vncserver -list` , and take note of the port number, usually denoted as `:XXXX`
3. set a password using `vncpasswd` -- **do NOT leave a password-less VNC setup**!!!
4. ssh into remote server creating a *tunnel to the local machine*, i.e.
   ```sh
   ssh -fN -L5904:localhost:XXXX userNAME@remote.server.ip
   ```
5. in your local machine launch a VNC client, eg. remina, tigervnc, etc.
   In MacOS, you can type in the terminal,
      `open vnc://localhost:5904`

---

References:
  - https://datatracker.ietf.org/doc/html/rfc6143
