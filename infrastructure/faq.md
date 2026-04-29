
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

## How do I access my Proxmox server?

Once you've installed Proxmox on your target hardware, you'll no longer need any peripherals connected to it, this includes the monitor. In-fact, the installation of Proxmox is usually going to be the only time you'll need anything else connected to your homelab, everything else is done through the web browser on another system on your home network. 

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


## Helper scripts

Throughout my guides, you'll see **helper scripts** both mentioned and utilised to setup various services on our homelab.

But, what exactly are "helper scripts"?

> Community-driven scripts for Proxmox VE

From this little sentence on the [**Proxmox VE Scripts**](https://community-scripts.org/) home page, we can ascertain that these are *unofficial* community created scripts you can use  in Proxmox. Essentially, instead of spending potentially hours setting up a new VM or LXC and researching dependencies and installation methods for the service you want to install, you can instead put your faith into the community and essentially "copy" a setup someone else has already created, and "import" that into your own homelab.

Let's have a quick look at some of the benefits of using a helper script:

 - **Simplicity**  
They can get you up and running within minutes rather than potentially hours.

 - **Easy to update**  
You only need to run the script again from within the shell of your VM/LXC.

 - ***Potentially* more reliable**  
Since it's a community driven endeavour with many users and contributors, there's a greater chance that potential issues can be identified and fixed before you ever experience them.

However, it's not all sunshine and roses. Here's a few potential downsides of using helper scripts:

 - **Unofficial**  
These **are** unofficial, and not officially supported or recommended by the Proxmox VE team.

 - **Security**  
You're putting your faith into the community and contributors, there's a potential for a bad faith actor to compromise the script.
   
 - **Learning**  
Arguably, you're not only depriving yourself of the opportunity to learn the installation processes, but also, how to use Linux.

As you can see, there's both compelling pros and cons to using helper scripts. My personal recommendation is, use helper scripts to setup services you're going to depend on to be reliable. But, also give yourself that learning opportunity. Spin up a new LXC or VM, and try setting it up for yourself.

Why not visit the [**Proxmox VE Scripts**](https://community-scripts.org/)  website and see what services you could potentially run on your homelab? If nothing else, it'll give you a fantastic insight into what people are running on their homelabs.


## What is IPv6?

Before we understand what IPv6 is, we must first understand what an IP address is. 

When we connect to the internet, our router is assigned a unique **public** IP address, and devices connected to your router are assigned a unique (to that network) **private** IP address, usually in the following IPv4 format:

> 192.168.1.1

When you type in a URL, such as *www.google.com*, your device uses a DNS server to lookup what IP that domain points to. Think of DNS like an address book, you lookup the name, in this case it's *Google*, and then you can find what address *Google* lives at.

Traditionally, the internet has solely relied on IPv4, which was developed all the way back in the 1980s! If it ain't broke, don't fix it, right? 

Well, as you can imagine, a lot of components of IPv4 are slightly dated these days, however, the biggest issue is that **we're now running out of IP addresses!**

*The internet is kind of like the universe, it just won't stop growing!*

IPv4, due to it's 32bit address size, has a limit of 4.3 billion potential addresses. Which must've sounded infinite in the 80s, though these days it feels increasingly more finite. 

This is where IPv6 comes in, with its 128 bit address size, allowing for 340 sextillion potential addresses, a number so big my brain can't even begin to process it. IPv6 addresses feel infinite.

As you can imagine, IPv6 addresses are significantly more complex and longer than an IPv4 address, typically using the following format:

> 2001:db8:0000:0000:0000:0000:0000:0000

That honestly looks terrifying. However, we do have a nifty shorthand way of typing out that address, so we don't need to remember "oh yeah, there's six groups of four zeros at the end of my address. Instead of taking the time to write all of that out, we can simply write it as this:

> 2001:db8::

That extra colon at the end of the addresses simply tells the system that everything after that **db8** section is just groups of zeroes.

Longer addresses aren't the only benefit of IPv6, but that's outside the scope of this guide. If you'd like to learn more, I'd highly recommend this article from [**OVHcloud**](https://www.ovhcloud.com/en-gb/learn/what-is-ipv6/).

