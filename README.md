# NASA Operational Simulator for Small Satellites 
The NASA Operational Simulator for Small Satellites (NOS3) is a suite of tools developed by NASA's Katherine Johnson Independent Verification and Validation (IV&V) Facility to aid in areas such as software development, integration & test (I&T), mission operations/training, verification, and validation (V&V), and software systems check-out. NOS3 provides a software development environment, a multi-target build system, an operator interface/ground station, dynamics and environment simulations, and software-based models of spacecraft hardware. 

## Documentation  
To get started with NOS3, you can visit the official NOS3 website, [nos3.org](http://www.stf1.com/NOS3Website/Nos3MainTab.php), or the GitHub repository maintained by NASA.  

### Prerequisites  
Each of the applications listed below is required prior to performing the installation procedure: 
* [Git 2.41.1+](https://git-scm.com/)
* [Vagrant 2.3.7+](https://developer.hashicorp.com/vagrant/downloads?ajs_aid=af56936c-70e3-4313-b622-5a95140eee93&product_intent=vagrant)
* [VirtualBox 7.0.8+](https://www.virtualbox.org/wiki/Downloads)

## Getting Started 

### Clone  
1. Open a terminal and Navigate to the desired location for the repository 
2. Clone the repository `git clone https://github.com/nasa/nos3.git` 
3.`cd nos3`  
4. `git checkout dev` 
5. Clone the submodules `git submodule init` and `git submodule update`  

### Provision  
1. Run `vagrant up` and wait to return to a prompt  
    * This can take a few minutes to hours depending on internet speeds host PC specs
    * The VM may reboot multiple times to finish installing packages for you automatically, so wait for that prompt. 
    * Sometimes ansible does not seem to install and there is an error like "Could not get lock /var/lib/apt/lists/lock". If this happens, run `vagrant provision` to 	 
      install ansible and provision. 
    * Vagrant will automatically load the virtual machine to Virtual Box, and it will be ready for use 
2. Login to the NOS3 VM with `nos3` as the user and the password `nos3123!` 

## Build  
1. Access the nos3 repository on the host machine. (This may already be done if you do `vagrant up`. Vagrant mounts the nos3 repository in the VM at `/home/nos3/Desktop/github-nos3`). From the guest VM:
1. Add Virtual Box Guest Additions:
	1. Go to Virtual Box menu -> Devices -> Insert Guest Additions CD image...
	2. Click `Run` in the resulting dialog box
2. Add a shared folder with the nos3 repository code:
	1. Go to Virtual Box menu -> Devices -> Shared Folders -> Shared Folders Settings...
	2. Add a new Shared Folder (folder with + sign) and select the location of the nos3 repository on the host
	3. Check `Auto-mount` and `Make Permanent`
	4. Reboot the VM 

## Run  
1. In a terminal, navigate to the nos3 shared folder after the VM reboot above 
2. Run `make`  
3. Run `make launch`
   
## Reset  

1. To exit the simulation, run `make stop` in the nos3 directory from the terminal  
2. To build NOS3 from the repository baseline, first run `make clean` and then run `make launch`  

### Directory Layout
* `components` contains the repositories for the hardware component apps; each repository contains the app, an associated sim, and COSMOS command and telemetry tables
* `fsw` contains the repositories needed to build cFS FSW
	- /apps - the open source cFS apps
	- /cfe - the core flight system (cFS) source files
	- /nos3_defs - cFS definitions to configure cFS for NOS3
	- /osal - operating system abstraction layer (OSAL), enables building for linux and flight OS
	- /psp - platform support package (PSP), enables use on multiple types of boards
	- /tools - standard cFS provided tools
* `gsw` contains the nos3 ground station files, and other ground based tools
	- /ait - Ammos Instrument Toolkit (Untested for 1.05.0)
	- /cosmos - COSMOS files
	- /OrbitInviewPowerPrediction - OIPP tool for operators
	- /scripts - convenience scripts
* `sims` contains the nos3 simulators and configuration files
	- /cfg - 42 configuration files and NOS3 top level configuration files
	- /nos_time_driver - time syncronization for all components
	- /sim_common - common files used by component simulators including the files that define the simulator plugin architecture
	- /sim_terminal - terminal for testing on NOS Engine busses
	- /truth_42_sim - interface between 42 and COSMOS to provide dynamics truth data to COSMOS

### Versioning
We use [SemVer](http://semver.org/) for versioning. For the versions available, see the tags on this repository.

### License
This project is licensed under the NOSA (NASA Open Source Agreement) License. 

# Issues and Features
Please report issues and request features on the GitHub tracking system - [NOS3 Issues](https://www.github.com/nasa/nos3/issues).

## Support
If this project interests you or if you have any questions, please feel free to contact any developer directly or email `support@nos3.org`.
