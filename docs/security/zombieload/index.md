---
author:
  name: Linode
  email: docs@linode.com
description: "Intel recently disclosed two vulnerabilities that affect processors in most devices over the last 23 years. Here's how that affects you and what you can do about it."
keywords: ["zombieload", "mds", "vulnerability", "kernel"]
license: '[CC BY-ND 4.0](https://creativecommons.org/licenses/by-nd/4.0)'
published: 2019-05-29
modified: 2019-05-29
modified_by:
  name: Linode
title: "What You Need to Do to Mitigate MDS/Zombieload"
external_resources:
  - '[ZombieLoad Attack](https://zombieloadattack.com/)'
  - '[How to Install Software Updates](/docs/getting-started/#install-software-updates)'
  - '[Reboot Survival Guide](/docs/uptime/reboot-survival-guide/)'
  - '[Linode Blog: Intel’s MDS (ZombieLoad) CPU Vulnerabilities & Linode](https://blog.linode.com/2019/05/15/intels-mds-zombieload-cpu-vulnerabilities-linode/)'
---

## Summary

Microarchitectural Data Sampling – MDS, or "Zombieload" – is a group of CPU vulnerabilities that affects most Intel CPUs released since 2011. Linode is working to implement patches on the physical machines that host Linodes, and we'll communicate maintenance times to you in a support ticket. In order to fully mitigate MDS/Zombieload, you'll need to also update your Linode's kernel.

## FAQ   
  
### Can this maintenance be postponed or rescheduled?

No. Due to the critical nature and logistical requirements of these updates, we aren’t able to reschedule or push back the provided maintenance windows. Our team is working around the clock to have our infrastructure patched against the Meltdown and Spectre vulnerabilities as quickly as possible.

### Can I start this maintenance early?

No. Since this maintenance is for the underlying host on which your Linode resides, it can't be started early.


### Is there anything that I need to do?

Yes. If you're running a Linode kernel, be sure to select either 4.14.120, or any kernel version that's 5.1.2 and newer. If your Linode’s Configuration Profile is set to utilize our latest kernel, your kernel will automatically be updated to the patched version upon rebooting.

### Can I reboot my Linode with the new kernel to avoid the maintenance?

No – while rebooting with an updated kernel will help prepare your Linode for the upcoming maintenance and help protect you against MDS/ZombieLoad, it will not replace the need for this maintenance. In order to fully address the vulnerabilities, we will need to perform maintenance on our infrastructure as scheduled. We'll provide maintenance status updates in the Linode Manager (both Cloud and Classic).

## What Should I Do?


* Visit our [Reboot Survival Guide](/docs/uptime/reboot-survival-guide/) to prepare for a graceful reboot.
* [Update your kernel](#how-to-reboot-into-an-updated-linode-kernel) and reboot.
* [Follow our blog for updates](https://blog.linode.com/2019/05/15/intels-mds-zombieload-cpu-vulnerabilities-linode/).


### How to Reboot into an Updated Linode Kernel

1.  Go to your Linode's dashboard and edit your configuration profile.

2.  Under **Boot Settings**, select **Latest 64 Bit**.

3.  Reboot your Linode and verify your kernel version:

        root@localhost:~# uname -r
        4.14.12-x86_64-linode92

### How to Update a Distribution-Supplied or Custom-Compiled Kernel

If you boot your Linode using the **GRUB** or **Direct Disk** boot setting, your kernel is supplied by your distribution’s maintainers, not Linode. If you’ve compiled your own kernel, you’ll need to recompile using the 5.1.2 or later source code.

1. Update your kernel to the latest available version using the distribution's package manager:

    **CentOS**

        sudo yum update kernel

    **Debian**

        sudo apt-get update
        sudo apt-get upgrade linux-base

    **Ubuntu**

        sudo apt-get update
        sudo apt-get upgrade linux-generic

2. Reboot your system. When it comes back up, use the command `uname -r` to verify you are running the new kernel against the patched version given in your distribution's security bulletin (see links below). This is also the recommended mitigation path for any hardware you use at home: your laptop, network hardware, and home servers.

    [CentOS 6](https://access.redhat.com/errata/RHSA-2018:0007) (see the *Overview* tab), [CentOS 7](https://access.redhat.com/errata/RHSA-2018:0007), [Debian](https://security-tracker.debian.org/tracker/CVE-2017-5754), [Ubuntu](https://people.canonical.com/~ubuntu-security/cve/2017/CVE-2017-5754.html).


## How can I stay updated with Linode’s progress?

The [Linode status page](https://status.linode.com/) will be updated with our progress of the fleet reboot, patches, and other related issues.
