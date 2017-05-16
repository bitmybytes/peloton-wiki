# Requirement
Eclipse NEON  [Download](http://www.eclipse.org/downloads/packages/eclipse-ide-cc-developers/neonm1)

# Setup
1. [Setup Peloton](https://github.com/cmu-db/peloton/wiki/Installation) in your Virtual Machine / Remote Server.
2. Turn on sshd service on Virtual Machine / Remote Server, setup your publickey for connection. 
3. Install [Direct Remote C++ Debugging](https://marketplace.eclipse.org/content/direct-remote-c-debugging) in Eclipse
4. Open `Debug Configurations`, select `C/C++ Remote Application`, right click and click `New`. From the bottom of the page click `Select other..`, click `Use configuration specific settings`, then select `Direct C++ Remote Launcher` from launchers list.
5. Select `Main` tab, set Remote C/C++ exe file path, E.g `/usr/local/bin/peloton`
6. Enter remote source-code path into `Remote Workspace Directory`, E.g `/home/username/peloton/`
7. Enter `export LD_LIBRARY_PATH=/usr/local/lib/` into Prerun commands

# Synchronize Code

* Modify and save following shell script:
```bash
#!/bin/sh
eval "$(ssh-agent -s)" > /dev/null 2>&1
ssh-add ~/.ssh/your_private_key > /dev/null 2>&1
rsync -rtvu path_to_local_dir username@remote_address:path_to_remote_dir $@
```
* Run the script when you want to synchronize

Have fun!