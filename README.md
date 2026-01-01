TL;DR
=====

```
$ ./pvectl --help
usage: pvectl [-h] [--version] [--profile PROFILE] [--config CONFIG] [--host HOST] [--port PORT] [--node NODE] [--user USER] [--token-id TOKEN_ID] [--token-secret TOKEN_SECRET]
              <command> ...

Manage Proxmox VMs and nodes from your local machine.

positional arguments:
  <command>
    list                List VMs
    create              Create an empty VM (no disk/NIC)
    disk                Disk operations
    cdrom               CD/DVD drive and ISO operations
    iso                 Manage ISO images in storage
    nic                 NIC operations
    pci                 PCI device operations
    status              Show VM status
    start               Start a VM
    stop                Hard stop (power off) a VM
    info                Show VM hardware configuration
    remove              Remove a VM (VMID only)
    options             Manage VM options

options:
  -h, --help            show this help message and exit
  --version             show program's version number and exit
  --profile PROFILE     Profile name in ~/.pvectl/profile.ini (default: None)
  --config CONFIG       Path to profiles.ini (override default) (default: None)
  --host HOST           Proxmox host only (no scheme), e.g. pve.example (default: None)
  --port PORT           Proxmox API port (default 8006) (default: None)
  --node NODE           Default Proxmox node name (overrides profile/env) (default: None)
  --user USER           Proxmox user (e.g. root@pam or user@pve) (default: None)
  --token-id TOKEN_ID   Proxmox API token id (default: None)
  --token-secret TOKEN_SECRET
                        Proxmox API token secret (default: None)
```

You will create a profile unless you adore cluttered command-lines in your
scripts:

```
$ cat ~/.pvectl/profile.ini 
[default]

host = pve
port = 8006
node = pve
user = root@pam
token_id = mytoken
token_secret = 0051a50d-6def-40c4-9e8c-711655b474cc
```

Get api tokens in proxmox from Datacenter -> Permissions -> API tokens.
Don't forget to un-check prilege separation when you create your token, unless you want the token to do
nothing much.


Waffle
======

Yet more copilot-generated slop to add to the ether.  Don't use this.  I
mean ever, it's rubbish.

OK, if you're still reading, this is something I created because I was used
to desktop virtualisation with parallels, vmware, VirtualBox etc... but the 
virtualisation world became a little shit once Apple dumped Intel silicon and 
intel no longer can be virtualised on it without massive headaches.

So we must seek free virt on external devices.  ESXi is...well a bit shit
and way too fussy about hardware.  Free Hyper-V is even more shit, not 
very performant, and... well... not really free if you need real Windows to
configure it (no web interface).  So we're left with Proxmox, which is 
arguably the hardest to use.  The ssh shell access is great, but makes things
fiddly to decide just how you want to manage things.  There's qm, pvesh, an
API, you're bouncing back and forth between local commands, and ssh commands
automation (in build pipelines) is fiddly. 

I want one interface just one tool that does all my automation, with the
auth stuff hidden, and a clean scripting interface. I don't 
want to be scripting ssh sessions, I want to use the API, but coding
everything as a series of python requests api calls is hard to follow.  I 
also hate Python libs, because they need VENVs, all the distros got strict
about this, rightly so, but it just adds to the complexity.  So single 
monolithic Python script it is, with minimal deps (requests is usually
included in most OS Pythons, e.g. Linux Mint built-in Python has that,
and easy to wire into a Homebrew setup as they support versions of 
Python in the cellar.  So here is pvectl, use at your own risk, if it 
deletes all your virtual machines it's your own fault, I'm not 
responsible.
