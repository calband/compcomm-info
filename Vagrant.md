# Vagrant

In many of our projects, we use the Vagrant package that will setup a virtual machine (VM) for us to use. This is advantageous for us, since we all have different computers and Vagrant will provide a common environment that will be set up the same for all of us.

## Usage

Some common Vagrant commands that you might use frequently include:

- `vagrant up [--provision]`: Boots up the VM. Use the --provision flag when first booting up the server. The --provision flag tells the VM to call a script that will set it up a certain way; without it, the server will be completely empty and won't be setup to run Django.
- `vagrant ssh`: Lets you ssh into the VM. The files in our project can be found in the `/vagrant` directory, which automatically syncs with the local directory.
- `vagrant halt`: Shuts down the VM. Can be woken up again with vagrant up.
- `vagrant destroy`: Destroys a created virtual server completely.
- `vagrant status`: Displays the current status of the Vagrant machine.

## Overview

As an overview of what Vagrant is, Vagrant is a command line interface for interacting with a VM. A virtual machine (VM) is basically a mini-computer inside of your computer, that can run a different OS like Linux. The VM is hosted by Virtualbox, which you should have downloaded also when you installed Vagrant. If you open the Virtualbox app, you can actually see the different VM's ("mini-computers") set up on your computer and open up a GUI for them, to interact with like an actual computer display.

Vagrant allows us to talk to this other computer and make it do things. For example, instead of opening the Virtualbox app and starting a computer in the app, we can just run `vagrant up`. Instead of `ssh`-ing into the VM like `ssh vagrant@localhost -P 2222` with the gritty details of `ssh`, you can just run `vagrant ssh`.

Throughout our projects, sometimes we will refer to "ssh into Vagrant" or "run on Vagrant". While this is technically inaccurate, as Vagrant is just the interface for communicating with a VM, it's often easier to say "run in Vagrant" just because of our constant interaction with it via `vagrant` and we don't have to explain the concept of a VM to everyone. But congratulations, you now understand what a VM is!
