---
published: true
---
## New (to me) HP Z600 Workstation!

Although I got this dual Xeon 12 core / 24 thread beast about a year ago, it was mostly used as a Window 10 Pro machine running an Ubuntu Virtualbox VM to control Ansible development, and other things that needed Windows e.g. gaming. However, I soon ran into the fact that Virtualbox only supports passthrough virtualization with AMD processors, meaning that I wouldn't be able to use `docker-machine` to create docker hosts without losing the convenience of Virtualbox by going with Hyper-V... at least without rebooting.

After some [research](https://www.reddit.com/r/docker/comments/7xvlye/docker_for_macwindows_performances_vs_linux/) on Docker performance in various OSs, it became apparent that I needed to go native Linux. Installing Ubuntu 18.04 on a separate SSD was trivial, but some finangling was required to configure GRUB and ensuring it was connected to the primary SATA port. I also had some fun installing [drivers](https://github.com/abperiasamy/rtl8812AU_8821AU_linux) for a WiFi adapter but other than that having a native Linux is so worth it! I always maintained that using a VM as a development environment was the way to go, but the difference between this and my [Hackintosh laptop](https://github.com/daliansky/XiaoMi-Pro-Hackintosh) with its 8th generation Intel CPU and NVMe drive is very noticeable.
