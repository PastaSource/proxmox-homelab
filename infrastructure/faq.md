
# FAQ

## What is Proxmox?

> **Proxmox Virtual Environment** is a complete, open-source server management platform for enterprise virtualization.

That's what they say on their website, but what does that mean in *English*?

Proxmox VE allows you to essentially turn a single physical computer into multiple *virtual* computers which can run different operating systems and services in isolation from one another. 

It also provides many super handy features which I'll delve into in the next section.

## Why use Proxmox?

Why would anyone want to use Proxmox when you could just do something like run an Ubuntu server with Docker installed on it? 
- **Separation**  
Every service you run can be completely separate from each other. Broke something in your Jellyfin LXC? No matter. None of your other services are affected, and you can just restore your Jellyfin LXC using a backup (which I'm certain you have). This is also really beneficial when it comes to security, especially if you need both privileged and unprivileged containers

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
Say you have a modest system with budget oriented hardware in it, running multiple VMs will quickly burn through those resources, as assigned CPU and RAM is treated as dedicated. LXC containers, on the other hand, use shared resources with limits, so they can only take what they need and leave unutilized resources available for other services.

- **Flexibility**  
Continuing on from the previous point, a LXC container provides greater flexibility when it comes to hardware. A VM will usually take exclusive control of a GPU, whereas LXC containers can be configured to share access to it. Meaning hardware can be utilized by various different containers.

- **Efficiency**  
Since a LXC container can just rely on the host kernel, there's less overhead compared to running a VM, as you're not running multiple full operating systems. Meaning not only will your services be up and running faster, but you're also getting more efficient use of your hardware.

- **Simplicity**  
LXC containers are quick and easy to deploy, especially with helper scripts. You can literally be up and running within minutes. Whereas with a VM you'll need to go through the entire process of setting up the VM, installing the operating system, etc.

So, now the question is: why would anyone want to use a VM? They seem so clunky and inefficient by comparison. In a lot of ways, they are. However, here are a few reasons why you might want to consider using one:

- **Security**  
While an unprivileged LXC container is already very secure, a VM has a higher level of isolation, due to not sharing the host Linux kernel.

- **OS Flexibility**  
Due to running their own kernel, you have a significantly greater level of flexibility of which operating system you'd like to run. As mentioned previously, you could even run a Windows VM.

- **Compatibility**  
Some software might expect full access to the system or the kernel. Not only can you provide that, but going back to the point of security you can do so securely without compromising your Proxmox server.

- **Hardware control**  
You might not want hardware to be accessible by other services, instead being dedicated to a single workload. In this case, the *limitation* of hardware exclusivity becomes a positive, as you can ensure no other services can access it.

At the end of the day, it comes back to identifying your needs and what you want to achieve. I'd say that the majority of the time a LXC container will be the better choice, because of its efficiency, simplicity, and flexibility. However, you will find edge case scenarios where a VM will be the superior choice.
