---
title: Pulseaudio Fix for KDE
author: bootlicker
type: post
date: 2018-02-13T05:58:42+00:00
url: /2018/02/13/pulseaudio-fix-for-kde/
categories:
  - Uncategorised

---
There is an issue with the way KDE installs in Arch Linux. This fix I discovered on the internet may help you.

If KDE does not recognise your sound device, but it is clearly being discovered by ALSA and Pulseaudio, it is because the Pulseaudio daemon is not being started at the right time before Plasma loads.

The fix to start the daemon at the right time is very simple. It is this:

<p style="padding-left: 30px;">
  <code>&lt;br />
nano -w /etc/pulse/client.conf</code><br /> <code>&lt;br />
set</code><br /> <code>&lt;br />
autospawn = yes</code>
</p>

You can find the original explanation of this fix at this URL: <https://forum.manjaro.org/t/kde-no-devices-in-audio-volume-settings/11849>

If the above fix produces a pulseaudio which cannot detect your soundcard, and KDE is only showing a Dummy Output, this is the fix:

<div class="codebox">
  <pre style="padding-left: 30px;"><code>pacman -Rsnc fluidsynth</code></pre>
</div>

There is a conflict between pulseaudio and the above package for some reason. The explanation can be found here: <https://bbs.archlinux.org/viewtopic.php?id=154002>