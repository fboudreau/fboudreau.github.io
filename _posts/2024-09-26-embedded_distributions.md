---
title: "Embedded Linux: building blocks"
categories:
    - blog
tags:
    - Embedded
    - Linux
    - Kernel
    - Bootloader
---

Linux is an operating system (OS). It manages the hardware and provides an
interface for applications to use the hardware. The OS is often referred to as
the Linux kernel. 

Often, when we discuss Linux, we mean a Linux distribution. A Linux
distribution is a combination of the Linux kernel (OS) and a file system that
contains a set of applications, libraries and services that are specific to
that distribution.

There are hundreds of Linux distributions, some more popular than others. Each
distribution is maintained by a community for a given purpose. Some
distributions are built for Desktop and include applications for word
processing, managing emails, browsing the web, watching videos, etc. Others are
for building servers and contain web servers, scripting languages and libraries
to construct web applications and database systems for storing data. Yet others
are for people who work in network security and contain tools for monitoring,
intrusion detection, etc.

In addition to readily available distributions like Ubuntu, Rehat, Mint or the
multitude listed on sites like [Distro Watch](https://distrowatch.com/){:target="_blank"}[^1],
many custom distributions exist for embedded devices. So called embedded Linux
is a custom distribution built to serve the purpose of the device that it
runs on.

Embedded Linux distributions are made and maintained by the developers of the
embedded device. Each is custom built to include a kernel and a set of
applications, libraries and services that support the requirements of the
embedded device. 

Embedded linux distributions are normally built using tools developed by the
embedded device developers and hardware component vendors. Popular tools like
Busybox, Buildroot, and Yocto are the bread and butter of embedded software
developers. These tools maintained by communities of developers, and the
hardware component vendors that provide the chips and modules that embedded
devices are made of.

# The building blocks of a distribution

A Linux distribution is typically made up of a bootloader(s), the operating
system ([Linux kernel](https://kernel.org){:target="_blank"}) and at least one
file system. The file system contains the set of libraries, applications,
utilities, etc. that are needed by the developers using the distribution. For
embedded devices, it's the software that is needed to implement the features of
the devices.

The following diagram depicts how the Linux kernel manages the hardware and how
it makes the hardware's services available to the applications.

![Linux Distribution](/assets/images/Linux Distribution Block diagram.drawio.png)

Things that reside on the file system interact with the kernel through the
system call interface (or the pseudo file systems[^2]).


# Summary of Boot Sequence

The basic boot sequence of a Linux distribution:

1. Bootloader
2. Linux kernel
3. User mode applications

The bootloader is the first user application that is executed. The bootloader
is not a Linux application. It is a standalone or sometimes named "bare metal"
application that is used to load the operating system[^3].

Once the bootloader has loaded the kernel, the kernel goes through it's own
initialization sequence where it initializes it's own subsystems and built-in
drivers. The final step of the kernel initialization is to pass control to user
space applications.

When the kernel is loaded, the bootloader tells it where the root file system
is located and the path to the first appliation to execute. Traditionally, the
first application is named init. The job of the init application is to begin
the initialization of user space. It does this by launching all the services
and applications defined by the maintainers of the distribution.

The following sequence diagram desribes a typical sequence:

<!--
Need a seperate article about bootloaders and why that are useful:
- Setup DDR to allow to load the kernel
- Networking facility to fetch kernel/application (ethernet, ftp, for example)
- Facility to store kernel boot parameters
- Facility to do over air upgrades
- Facility for programming NAND/eMMC, etc.
-->


![Boot Sequence](/assets/images/distro_boot_sequence_simple.png)

----


[^1]: List of some distributions
    - [Wikipedia Linux Distributions](https://en.wikipedia.org/wiki/Linux_distribution)
    - [Wikipedia - Linux Distributions Examples](https://en.wikipedia.org/wiki/Linux_distribution#Examples)
    - [Distrowatch](https://distrowatch.com/)

[^2]: There are various methods for interacting with the kernel and drivers:
    - The system call interface (ioctl)
    - The sysfs:
        - man -s 5 sysfs
        - https://en.wikipedia.org/wiki/Sysfs
    - The procfs: 
        - man proc
        - https://en.wikipedia.org/wiki/Procfs
 
[^3]: Bootloaders have other uses:
    - Store kernel parameters
    - Networking facility for fetching params, kernels and applications
    - Storage device facilities for storing the operating system/distribution
      files onto storage devices such as NAND, eMMC, etc.

<!--

Notes:

One sentence premise: Bootloaders, kernel, user space application (init).

System call interface?

-->
