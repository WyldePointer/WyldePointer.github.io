---
layout: post
title: "Dual-booting a root-encrypted OpenBSD and Void Linux"
date: 2017-09-11 06:05:32 +0430
tags: [security,void,gnu,linux,openbsd,crypto,disklabel,encryption,dual-boot]
---

Scenario: You want to have `OpenBSD` as your main desktop but you have 2x4TB
 external HDDs that are formatted as `ext4`. Oops!

Problem: `OpenBSD` does not support `ext4` and for accessing your files, you
 have to either run a `GNU/Linux` on a USB stick or dual-boot your laptop.

Solution: Installing `Void Linux` on 1st partition, having your `swap` as the
 2nd one, having a "shared" partition(`FAT32`) as 3rd one and finally having
 the `OpenBSD` partition as the last primary partition.(e.g, `/dev/sda4`)

The fun part: `OpenBSD`'s `disklabel` is a totally unknown world for those
 who are coming from `GNU/Linux` but no worries, it will be all clear for ya.

### Step 0: Preparing the installation media

I used a 2GB USB stick as the installation media for `Void` and for doing so,
 you need to run only one command:

```sh
# dd if=/path/to/void.iso /dev/sdb
```

And that's it! No need for `unetbootin` or any extra stuff.

My `OpenBSD 6.1` was already on CD but of course you can have it on a USB
 stick as well. Check their website for more information.

### Step 1: Partitioning the disk

Since `OpenBSD`'s `fdisk` is pretty "unique" in some ways, I'd like to suggest
 you to use the `cfdisk` that's coming with your `Void` install disk.

My laptop had a ~92GB HDD and I decided to use ~35GB for `GNU/Linux`, 3.2 for
 its `swap`, a 20GB "shared" partition(that `FAT32` dude) and ~35GB for
 `OpenBSD`. (No wonder if the numbers are not matching, I'm not really good
 at math!) 

All I did was running `cfdisk` as root and after creating the partitions,
 I marked the 1st one(`/dev/sda1`) as bootable. The types are `83`, `82`, `0B`
 and `A6`. (Linux, Linux swap, FAT32, OpenBSD)

When you're done, choose `write`, then  `quit` and then `# reboot` your
 machine and make it get into the `OpenBSD` installer. (`ESC`, `TAB`, `F2`,
 `F8`, `F10`, etc.)

### Step 2: OpenBSD disk encryption

Choose (S)hell and run the following command:

```sh
# disklabel -E wd0
```

Now it's time to add a new label(slice, partition, whatever you prefer) inside
 that "OpenBSD area"(`/dev/sda4`) and for doing so, we use `a a` and choose
 the `RAID` as its FS type:

```sh
> a a
..
..
RAID

> w
> q
```

Now it's time to enable the crypto device(aka encrypted partition) and for
 doing so, we use:

```sh
# bioctl -c C -l /dev/wd0a softraid0
```

Now it's ready and during the installation, instead of choosing `wd0`, you can
 choose `sd0` or `sd1`, depends on your internal HDD type and SATA
 implementation of your BIOS and so on.

### Step 3: Installing Void

Believe me or not, it was the easiest `GNU/Linux` installation that I've ever
 done. Pretty straightforward and human-friendly.

### Step 4: Adding OpenBSD to GRUB

Now when you're done installing the `Void`, you should be able to boot into
 that and after doing so, we need to add the `OpenBSD` to our GRUB menu: 

```sh
# vi /etc/grub.d/40_custom
```

So we append the following lines **AFTER** all those comments:

```
menuentry "OpenBSD"{
  set root=(hd0,4)
  chainloader +1
}
```

Then we run:

```sh
# update-grub
```

That's it! I'm writing this post from a machine that's configured the same way
 that I've explained in this post.

