---
title: Installing Kali Linux
date: 2025-04-02
categories: [tutorial]
tags: [kali, linux]
---

In this first tutorial we're gonna be installing Kali Linux! In cybersecurity and pentesting it's recommended to have some VMs (*Virtual Machines*) to use as labs, so we can perform certain actions without compromising our own personal PC.

I've chosen [Kali Linux](https://www.kali.org/) because it's the go-to distro for pentesting. There are other distros like [ParrotOS](https://www.parrotsec.org/) or [BlackArch](https://www.blackarch.org/), but Kali Linux performs just as well as the other two and it's somewhat the easiest one.

I'm assuming that you have some knowledge creating and using VMs because I will not cover that in this tutorial or in future ones. That being said, you can use whatever virtual machine manager you want, whether it's [VMware](https://www.vmware.com/), [VirtualBox](https://www.virtualbox.org/) or [QEMU](https://www.qemu.org/); it doesn't matter.

In order to begin the installation process, we need to download the ISO file from the official Kali Linux website.

- [link](https://www.kali.org/get-kali/#kali-installer-images).

## Virtual Machine Specs
Before the installation process, we need to set up the specs for the virtual machine.

|         |  Minimum   | Recommended |
| ------- | :--------: | :--------: |
|   CPUs  |      2     |      4     |
|   RAM   |   4096 MB  |   8192 MB  |
| Storage |   100 GB   |    100 GB   |

## Installation
Once we have our virtual machine created and the ISO file, we can begin the installation process.

In this first section, we'll choose **Graphical install**.

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402202637.png)

Choose **English** as the main language for the system and press **Continue**.

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402202911.png)

Choose your location; in my case, **Europe/Spain**.

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402203532.png)

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402203640.png)

Now we need to select the preferences from the available locales for the selected language. In our case, it will be **United States - en_US.UTF-8**.

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402204336.png)

Next, we choose the keyboard configuration.

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402204455.png)

We need to enter the **hostname** for the system. In my case, I'm going to choose the **default hostname**.

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402205250.png)

We can skip the **Domain name**.

Now, it's time to set up the **user** and **password**. Make sure to choose a strong password.

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402205553.png)

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402205621.png)

Select your time zone:

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402205739.png)

For the disk partitioning, we have different options. Choose the first one.

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402205947.png)

Then, choose the disk that will be used. There should be only one option here.

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402210044.png)

Now, the installer is asking us which partitioning scheme we want. We will choose the first option.

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402210339.png)

Once that is done, we can confirm the changes by selecting the option **Finish partitioning and write changes to disk**.

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402210510.png)

Now, we wait.

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402210614.png)

At some point, the installer will ask us which desktop environment and collections of tools we want. Feel free to choose; I'm going to select the default options.

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402211121.png)

We're almost there! Now, we have to install GRUB. Select **Yes** and press **Continue**.

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402213755.png)

Lastly, select **/dev/vda**.

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402213852.png)

Once the installation is complete, we will have to reboot the system.

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402214030.png)

Welcome to Kali Linux!

![](../assets/pictures/2025-04-02/Pasted%20image%2020250402214128.png)