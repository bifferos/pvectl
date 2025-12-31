README
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
Pythin in the cellar.  So here is pvectl, use at your own risk, if it 
deletes all your virtual machines it's your own fault, I'm not 
responsible.
