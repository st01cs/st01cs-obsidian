---
title: "5 systemd tweaks that really boost my boot time"
source: "https://www.xda-developers.com/systemd-tweaks-boost-boot-time/"
author:
  - "[[Jeff Butts]]"
published: 2025-09-24
created: 2025-09-30
description: "Speed up your Linux startup with five simple systemd tweaks that cut delays and make booting noticeably faster."
tags:
  - "clippings"
---
Not every Linux user obsesses over how quickly their system boots, but I like seeing a fast and clean startup. Even with a solid-state drive, bottlenecks can sneak in and slow things down. [Systemd provides a variety of tools](https://www.xda-developers.com/why-i-use-systemd-on-linux/) that allow you to track where those delays are occurring and resolve them. With a [bit of tuning](https://www.xda-developers.com/linux-command-line-tricks-everyone-should-know/), I was able to shave a noticeable amount of time off my boot process without sacrificing stability.

The real benefit of these tweaks is not just shaving seconds off a stopwatch. A system that boots quickly feels more responsive and wastes less of your time waiting.

## Identifying slow points in your boot process

### Using systemd-analyze to track boot performance

- ![systemd-analyze critical-chain output](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/systemd-analyze-critical-chain-output.png?q=49&fit=contain&w=750&h=422&dpr=2)

- ![systemd-analyze critical-chain output](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/systemd-analyze-critical-chain-output.png?q=49&fit=crop&w=145&h=80&dpr=2)
- ![An HP Elitebook x360 1030 G2 running Fedora 42 with XFCE and the DesktopPal97 theme](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/08/linux-retro-pc-themes-desktoppal97-2.jpg?q=49&fit=crop&w=145&h=80&dpr=2)
- ![listing start times for all services](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/listing-start-times-for-all-services.png?q=49&fit=crop&w=145&h=80&dpr=2)
- ![This niche Fedora-based Linux distro ‘just works’ and stays out of your way as much as possible -featurd](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/this-niche-fedora-based-linux-distro-just-works-and-stays-out-of-your-way-as-much-as-possible-featurd.jpeg?q=49&fit=crop&w=145&h=80&dpr=2)
- ![systemd-analyze output](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/systemd-analyze-output.png?q=49&fit=crop&w=145&h=80&dpr=2)

- ![systemd-analyze critical-chain output](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/systemd-analyze-critical-chain-output.png?q=49&fit=contain&w=1920&h=1080&dpr=2)
- ![An HP Elitebook x360 1030 G2 running Fedora 42 with XFCE and the DesktopPal97 theme](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/08/linux-retro-pc-themes-desktoppal97-2.jpg?q=49&fit=contain&w=4096&h=2304&dpr=2)
- ![listing start times for all services](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/listing-start-times-for-all-services.png?q=49&fit=contain&w=1920&h=1080&dpr=2)
- ![This niche Fedora-based Linux distro ‘just works’ and stays out of your way as much as possible -featurd](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/this-niche-fedora-based-linux-distro-just-works-and-stays-out-of-your-way-as-much-as-possible-featurd.jpeg?q=49&fit=contain&w=2560&h=1440&dpr=2)
- ![systemd-analyze output](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/systemd-analyze-output.png?q=49&fit=contain&w=1920&h=1080&dpr=2)

- ![systemd-analyze critical-chain output](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/systemd-analyze-critical-chain-output.png?q=49&fit=crop&w=145&h=80&dpr=2)
- ![An HP Elitebook x360 1030 G2 running Fedora 42 with XFCE and the DesktopPal97 theme](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/08/linux-retro-pc-themes-desktoppal97-2.jpg?q=49&fit=crop&w=145&h=80&dpr=2)
- ![listing start times for all services](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/listing-start-times-for-all-services.png?q=49&fit=crop&w=145&h=80&dpr=2)
- ![This niche Fedora-based Linux distro ‘just works’ and stays out of your way as much as possible -featurd](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/this-niche-fedora-based-linux-distro-just-works-and-stays-out-of-your-way-as-much-as-possible-featurd.jpeg?q=49&fit=crop&w=145&h=80&dpr=2)
- ![systemd-analyze output](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/systemd-analyze-output.png?q=49&fit=crop&w=145&h=80&dpr=2)

Before you can speed things up, you need to know what is slowing you down. The command `systemd-analyze` shows how long the kernel and userspace take to initialize, giving you a big-picture view of your boot time. Pair it with `systemd-analyze blame` and you will see a detailed breakdown of services ranked by how long they take to start. This is often where the real culprits hide, whether it is a misconfigured daemon or something you never actually use.

By running this analysis a few times, you get a sense of consistency versus outliers. Some services might occasionally spike due to hardware detection, while others are consistently heavy. Focusing on the worst offenders will give you the most improvement for the least effort. I usually save a copy of the output before making changes so I can measure progress objectively.

It is also worth using `systemd-analyze critical-chain`, which shows how dependencies line up in the boot sequence. Services that block other essential tasks are prime candidates for reordering or disabling. With this tool in hand, you can move from guessing to making informed adjustments that genuinely reduce startup delays.

## Cutting down on background services

### Disabling services you do not actually use

- ![disabling cups service](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/disabling-cups-service.png?q=49&fit=contain&w=750&h=422&dpr=2)

- ![disabling cups service](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/disabling-cups-service.png?q=49&fit=crop&w=145&h=80&dpr=2)
- ![RawTherapee running on a Linux desktop PC on a black desk with a keyboard, mouse, and microphone](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/08/rawtherapee-on-linux-desk-2.jpg?q=49&fit=crop&w=145&h=80&dpr=2)
- ![Not that Linux is hard but it is unforgiving - featured](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/08/not-that-linux-is-hard-but-it-is-unforgiving-featured.jpg?q=49&fit=crop&w=145&h=80&dpr=2)
- ![Running Conky on EndeavourOS ](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/08/linux-conky.jpg?q=49&fit=crop&w=145&h=80&dpr=2)
- ![systemd cups dependencies](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/systemd-cups-dependencies.png?q=49&fit=crop&w=145&h=80&dpr=2)

- ![disabling cups service](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/disabling-cups-service.png?q=49&fit=contain&w=1920&h=1080&dpr=2)
- ![RawTherapee running on a Linux desktop PC on a black desk with a keyboard, mouse, and microphone](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/08/rawtherapee-on-linux-desk-2.jpg?q=49&fit=contain&w=4096&h=2304&dpr=2)
- ![Not that Linux is hard but it is unforgiving - featured](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/08/not-that-linux-is-hard-but-it-is-unforgiving-featured.jpg?q=49&fit=contain&w=5712&h=3213&dpr=2)
- ![Running Conky on EndeavourOS ](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/08/linux-conky.jpg?q=49&fit=contain&w=3840&h=2160&dpr=2)
- ![systemd cups dependencies](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/systemd-cups-dependencies.png?q=49&fit=contain&w=1920&h=1080&dpr=2)

- ![disabling cups service](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/disabling-cups-service.png?q=49&fit=crop&w=145&h=80&dpr=2)
- ![RawTherapee running on a Linux desktop PC on a black desk with a keyboard, mouse, and microphone](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/08/rawtherapee-on-linux-desk-2.jpg?q=49&fit=crop&w=145&h=80&dpr=2)
- ![Not that Linux is hard but it is unforgiving - featured](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/08/not-that-linux-is-hard-but-it-is-unforgiving-featured.jpg?q=49&fit=crop&w=145&h=80&dpr=2)
- ![Running Conky on EndeavourOS ](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/08/linux-conky.jpg?q=49&fit=crop&w=145&h=80&dpr=2)
- ![systemd cups dependencies](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/systemd-cups-dependencies.png?q=49&fit=crop&w=145&h=80&dpr=2)

Once you know what is eating up time, the next step is trimming the fat. [Many Linux distributions](https://www.xda-developers.com/linux-distros-perfect-reviving-pcs-cant-handle-windows-11/) enable services by default that not every user needs. For example, printer daemons or Bluetooth managers often run in the background even on machines without printers or Bluetooth hardware. Disabling these services can free up valuable seconds during startup.

The easiest way to manage this is with `systemctl disable` followed by the service name. This prevents it from launching on boot, while still allowing you to start it manually if you ever need it. For services you are absolutely sure you will never use, `systemctl mask` goes one step further by blocking them entirely. The fewer daemons systemd has to spin up, the quicker your machine will reach a usable state.

Don’t go in disabling services willy-nilly. Be sure to look closely at what they do and what other services might depend on them. Backing up your PC before beginning your tweaks is definitely a great idea.

Of course, this requires a bit of caution. Disabling something essential could break functionality you rely on, so I recommend changing one thing at a time and testing after each tweak. Over the course of a few days, you can build a leaner and faster boot profile without destabilizing your system.

## Taking advantage of systemd parallelization

### Optimizing dependencies for speedier startup

![man page for systemd](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/man-page-for-systemd.png?q=49&fit=crop&w=825&dpr=2)

One of the advantages systemd has over older init systems is its ability to start services in parallel. Instead of waiting for each daemon to load before starting the next, it launches independent ones simultaneously. This means your CPU and disk are used more efficiently, which naturally speeds things up. The key is making sure dependencies are defined properly so services don’t block one another unnecessarily.

You can check dependency relationships with `systemctl list-dependencies` or by looking at unit files directly. If you notice that a service is waiting on something it does not really need, you can adjust its configuration. Adding directives like `After=` or `Requires=` lets you fine-tune when a service starts in relation to others. Removing unnecessary dependencies prevents idle waiting and makes better use of parallelization.

Another trick is enabling socket activation for certain services. With socket activation, systemd only launches a daemon when its socket is accessed, rather than on every boot. This not only shortens startup time but also reduces background resource usage. When tuned correctly, you get a system that feels both faster and lighter.

## Masking services that cause slowdowns

### Ensuring nothing re-enables what you masked

![These 5 Linux distros are perfect for reviving PCs ](https://static0.xdaimages.com/wordpress/wp-content/uploads/2025/07/these-5-linux-distros-are-perfect-for-reviving-pcs.jpeg?q=49&fit=crop&w=825&dpr=2)

Sometimes it is not enough to disable a service, because another package update or dependency might re-enable it. Masking is the stronger solution, as it essentially ties a service to `/dev/null` so it cannot be started by accident. This is especially useful for services you know for sure are irrelevant to your setup. A good example is networking daemons that conflict with your chosen manager.

To mask a service, you use `systemctl mask` followed by the unit name. From then on, even if another process tries to launch it, systemd will refuse. If you ever change your mind, unmasking is as simple as `systemctl unmask`. It gives you peace of mind that unwanted services won’t creep back into your boot sequence.

The catch is that masking the wrong service can cause confusion, especially if something else depends on it indirectly. That is why I always double-check the dependency tree before masking. When done correctly, though, masking ensures your [system stays optimized](https://www.xda-developers.com/these-5-arch-distros-are-worth-checking-out/) over time, even through updates.

## Improving how the desktop session starts

### Adjusting display and login managers for speed

- ![photo of a mx linux desktop on an external display](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/mx-linux-desktop-on-an-external-display.jpg?q=49&fit=contain&w=750&h=422&dpr=2)

- ![photo of a mx linux desktop on an external display](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/mx-linux-desktop-on-an-external-display.jpg?q=49&fit=crop&w=145&h=80&dpr=2)
- ![Snapshot of changing the desktop wallpaper in Kali Linux VMware image](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2023/08/kali-linux-virtual-machine-desktop-wallpaper.jpg?q=49&fit=crop&w=145&h=80&dpr=2)
- ![Snapshot of Kali Linux desktop in a VMware virtual machine](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2023/08/kali-linux-virtual-machine-desktop.jpg?q=49&fit=crop&w=145&h=80&dpr=2)
- ![A screenshot of the main Linux Mint desktop showing the Install Linux Mint option ](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2023/12/screenshot-2023-12-05-115022.png?q=49&fit=crop&w=145&h=80&dpr=2)
- ![A dual monitor desktop PC running Fedora 41 Cinnamon with the B00merang Project Windows XP-inspired theme](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/08/linux-retro-pc-themes-b00merang-windows-xp-desktop.jpg?q=49&fit=crop&w=145&h=80&dpr=2)

- ![photo of a mx linux desktop on an external display](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/mx-linux-desktop-on-an-external-display.jpg?q=49&fit=contain&w=2100&h=1400&dpr=2)
- ![Snapshot of changing the desktop wallpaper in Kali Linux VMware image](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2023/08/kali-linux-virtual-machine-desktop-wallpaper.jpg?q=49&fit=contain&w=1624&h=917&dpr=2)
- ![Snapshot of Kali Linux desktop in a VMware virtual machine](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2023/08/kali-linux-virtual-machine-desktop.jpg?q=49&fit=contain&w=1624&h=917&dpr=2)
- ![A screenshot of the main Linux Mint desktop showing the Install Linux Mint option ](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2023/12/screenshot-2023-12-05-115022.png?q=49&fit=contain&w=1435&h=978&dpr=2)
- ![A dual monitor desktop PC running Fedora 41 Cinnamon with the B00merang Project Windows XP-inspired theme](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/08/linux-retro-pc-themes-b00merang-windows-xp-desktop.jpg?q=49&fit=contain&w=4096&h=2304&dpr=2)

- ![photo of a mx linux desktop on an external display](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/09/mx-linux-desktop-on-an-external-display.jpg?q=49&fit=crop&w=145&h=80&dpr=2)
- ![Snapshot of changing the desktop wallpaper in Kali Linux VMware image](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2023/08/kali-linux-virtual-machine-desktop-wallpaper.jpg?q=49&fit=crop&w=145&h=80&dpr=2)
- ![Snapshot of Kali Linux desktop in a VMware virtual machine](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2023/08/kali-linux-virtual-machine-desktop.jpg?q=49&fit=crop&w=145&h=80&dpr=2)
- ![A screenshot of the main Linux Mint desktop showing the Install Linux Mint option ](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2023/12/screenshot-2023-12-05-115022.png?q=49&fit=crop&w=145&h=80&dpr=2)
- ![A dual monitor desktop PC running Fedora 41 Cinnamon with the B00merang Project Windows XP-inspired theme](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/08/linux-retro-pc-themes-b00merang-windows-xp-desktop.jpg?q=49&fit=crop&w=145&h=80&dpr=2)

For desktop users, the final leg of the boot process is often the graphical session. [Display managers like GDM](https://www.xda-developers.com/mistakes-choosing-linux-distro-pc/), LightDM, or SDDM can each add their own startup time. Tweaking them or switching to a lighter one can make a noticeable difference. For example, LightDM tends to be faster on modest hardware compared to heavier alternatives.

Another thing to look at is autostart applications in your session settings. Many desktop environments launch small helper apps, updaters, or cloud sync clients by default. Trimming these down to only what you actually use not only makes the desktop load faster but also reduces clutter once you log in. It is the same principle as disabling system services, just applied at the user level.

You can also experiment with how your system transitions between multi-user and graphical targets. By delaying certain services until after the desktop is loaded, you prioritize reaching a usable session sooner. Minor adjustments like these often stack up, turning a sluggish startup into a noticeably snappier experience.

### Why systemd tuning pays off in daily use

The real benefit of these tweaks is not just shaving seconds off a stopwatch. A system that boots quickly feels more responsive and wastes less of your time waiting. By analyzing, disabling, masking, and fine-tuning services, you create a smoother experience tailored to your needs. The changes are easy to reverse if something goes wrong, but once dialed in, they tend to stick. For me, those small wins add up every day, and the payoff is a Linux system that feels as fast as it should.

Ubuntu Cinnamon is fast to boot up, but you can shave even more time off the bootup by tweaking the systemd settings.

[Ubuntu Cinnamon Official Site](https://ubuntucinnamon.org/)