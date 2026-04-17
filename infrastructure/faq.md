# FAQ

## Why use Proxmox?

Why would anyone want to use Proxmox when you could just do something like run an Ubuntu server with Docker installed on it? 
- **Separation**  
Every service you run can be completely seperate from each other. Broke something in your Jellyfin LXC? No matter. None of your other services are affected, and you can just restore your Jellyfin LXC using a backup (which I'm certain you have). This is also really benefitial when it comes to security, especially if you need both priviledged and unpriviledged contaniers

- **Snapshots**  
Snapshots are invaluable. I cannot begin to tell you the amount of times I've tried something, only to break something fundamental and have to rollback to a snapshot. As someone who loves to tinker, being able to do so, *risk-free*, is a saving grace.

- **Learning**  
Expanding on my previous point, with the ability to do whatever you want in your VMs and LXC completely risk-free opens the door to endless opportunities to learn. You'll also learn things like resource management, networking, Linux, etc.

- **Ease of use**  
The UI might seem daunting at first, but once you actually dive into using it, you'll be surprised at how intuitive everything is. Setting up a VM or LXC can be done in a few minutes. And with the aid of "helper scripts" you can even get entire services up and running with a matter of minutes.

There are countless other reasons why Proxmox is a great choice for your first homelab, but these are the most important ones for me.

## VMs vs LXC

Proxmox containers (LXC) and virtual machines (VM), both have very different use cases. A LXC container will use the same underlying kernel that Proxmox is using. In plain English, this means you'd never be able to create something like a Windows Server LXC as Windows Server uses the Windows NT kernel, whilst Proxmox uses the Linux kernel. So, what do you do if you want to run Windows Server? That's when you'd want to create a VM. You can think of a VM like a completely separate computer, except virtualized and living inside of your Proxmox server. It doesn't share the host kernel, meaning you can install almost any operating system you'd like on it.

It sounds like using a VM is so much simpler, right? You don't need to worry about kernels or anything like that. Just spin up a VM, install what you want, Bob's your uncle. *Why would anyone want to use a LXC container?*

Here are a few reasons why you'd choose a LXC container over a VM:
- **Resource management**  
Say you have a Proxmox server running a Ryzen 5 3600 (6 cores / 12 threads) and 16GB of RAM. Running many VMs would soon burn through all of those resources. Resources assigned to a VM are typically exclusive to that VM, meaning if 4 cores and 4GB of RAM were assigned to a VM, nothing else can touch those resources.  
With a LXC container, you're more of setting a limit. If you set it to use 4 cores and 4GB of RAM, it'll use up to 4 cores and 4GB of RAM *if it needs to*. If the machine is idle, those resources are free to be used by other services.  
This applies to hardware like GPUs too. A VM will usually take exclusive control of a GPU, whereas LXC containers can be configured to share access to it. Allowing hardware to be utilized by various different containers.

- **Efficiency**  
Since a LXC container can just rely on the host kernel, so there's less overhead when compared to running a VM. Meaning not only will your services be up and running faster, but you're also getting more efficient use of your hardware, as you're not running multiple full operating systems.

- **Simplicity**  
LXC containers are quick and easy to deploy, especially with helper scripts. You can literally be up and running within minutes. Whereas with a VM you'll need to go through the entire process of setting up the VM, installing the operating system, etc.

So, now the question is: why would anyone want to use a VM? They seem so clunky and inefficient by comparison.
