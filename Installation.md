## Supported Platforms

Peloton is known to work on the following platforms. Please note that it will not compile on 32-bit systems.

* Ubuntu Linux 14.04+ (64-bit)
* <s>Mac OS X 10.9+ (64-bit)</s>

## Ubuntu Quick Setup

1. Install the packages in the [package list](https://github.com/cmu-db/peloton/blob/master/script/installation/packages.sh) using this script.

    ```sh
    sudo bash ./script/installation/packages.sh
    ```

2. Now, go to the [Build Peloton](https://github.com/cmu-db/peloton/wiki/Installation#build-peloton) step.

## OSX/Windows Quick Setup

1. Install Git, Virtualbox, and Vagrant (if needed).

    [Git Download](https://git-scm.com/)
    [Virtualbox Download](https://www.virtualbox.org/wiki/Downloads)  
    [Vagrant Download](https://www.vagrantup.com/downloads.html)  
    [Getting Started with Vagrant on OSX Yosemite](https://web.archive.org/web/20160309165307/http://coolestguidesontheplanet.com/getting-started-vagrant-os-osx-10-9-mavericks)   
    [Getting Started with Vagrant on Windows](http://www.sitepoint.com/getting-started-vagrant-windows/)

2. Clone Peloton repo

    ```sh
    git clone --recursive https://github.com/cmu-db/peloton.git
    ```

3. Initialize the vagrant box

    ```sh
    cd peloton/script/installation
    vagrant up
    ```

   NOTE: Actual VM is managed by VirtualBox, not stored in the local Peloton repo you just cloned.

4. Connect to the vagrant box

    ```sh
    vagrant ssh
    ```

5. Now, go to the [Build Peloton](https://github.com/cmu-db/peloton/wiki/Installation/#build-peloton) step.

### Vagrant Reload

In case you wish to [reload](https://docs.vagrantup.com/v2/cli/reload.html) the virtual machine so that any changes made in the Vagrantfile take effect, use this command:

```sh
vagrant reload --provision
```

## Build Peloton

Before building `peloton`, make sure that you have installed all its software dependencies by following the instructions given above in `Ubuntu Quick Setup` or `OSX/Windows Quick Setup` depending on your machine. 

Enter the `build` directory and run `cmake`:

* Ubuntu:

	```sh
	mkdir -p build
	cd build
	cmake -DCMAKE_BUILD_TYPE=Release ..
	```

* Vagrant VirtualBox VM:

	`/peloton` on VM is automatically created as a shared folder linked to the repo on host. This might not support building directly in the repo, so a separate build dir needs to be created:
	
	```sh
	mkdir -p ~/build
	cd ~/build
	cmake -DCMAKE_BUILD_TYPE=Release /peloton
	```

If your system reports error then please try the following alternative instead (it is caused by code coverage not being supported under release mode):

```sh
cmake -DCMAKE_BUILD_TYPE=Release -DCOVERALL=False ..
```

For building a debug mode binary, please run the following command:

```sh
cmake -DCMAKE_BUILD_TYPE=Debug .. 
```

Build and install Peloton

```sh
make -j4
make install
```

Update paths in `.bashrc` or `.zshrc` or your favorite shell's startup file :

```sh
export PATH=$(BUILD_DIR)/bin:$PATH
export LD_LIBRARY_PATH=$(BUILD_DIR)/lib:$LD_LIBRARY_PATH
```
