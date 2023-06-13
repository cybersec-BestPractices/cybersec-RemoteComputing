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


# Other Remote Accessible Protocols
VNC is one protocol used to remotely access computational resources but there are many other ones.
For instance, communication applications may use their own ones to give users access to control remote resources, or specialized applications may entitle users to control remote computers using proprietary protocols.
Another example of such is the *Remote Desktop Protocol* (RDP) mostly used in Windows machines.

Independently of the specific protocol used, one should note that these are a liability form cyber-security considerations.
Extreme caution must be followed when using these type of tools, and awareness that they may weaken the cybersecurity perimeter of an organization or device by enabling weak or blind spots when accessing the remote resource.


---

References:
  - https://datatracker.ietf.org/doc/html/rfc6143

---
*Last Modified: Jun. 13, 2023*  --  v 1.0
