Public download link here:

http://download.haage-partner.de/Amiga/AmigaXL/amigaxl-uae-source.tgz


Working download link and its archive can be found here (checked 28.11.2021):

https://web.archive.org/web/20071222082612/http://download.haage-partner.de/Amiga/AmigaXL/amigaxl-uae-source.tgz





# UAE_0.8.15

This is version 0.8.15 of UAE, the Un*x Amiga Emulator.

Versions numbered 0.8.x are beta versions, to be used for development only.
If you are only a user of UAE, you are better off using the latest 0.7.x
version or waiting for 0.9.0.


License
=======

UAE is available under the terms of the GNU General Public License. This means
that it is free software: you are welcome to distribute copies of it and/or
modify it, under certain conditions. It also means that there is no warranty
for UAE.
See the file COPYING that is included in the top level directory of this
archive for details.

The SCSI code distributed with UAE is also available under the terms of the
GPL and was written by J. Schilling.


Overview
========

An emulator is a program which enables you to run software for a machine
which has non-native hardware and a non-native operating system, on your
computer.  UAE allows you to run most of the available Amiga software. It is a
software emulation, meaning that no extra or special hardware is needed to do
this. The hardware of an Amiga is emulated accurately, so that Amiga software
is tricked into thinking it is running on the real thing, with your computer's
display, keyboard, harddisk and mouse taking the parts of their emulated
counterparts.

UAE was developed for Unixoid systems. Meanwhile, it has been ported to the
Mac, DOS, the BeBox, NextStep, the XFree86/OS2 environment and the Amigas (it
can run itself by now). You should have received several other files along
with this document with details on how to install and use the version for your
operating system.

This section is just what it says: an overview. Please read _all_ of this
file, especially if you have problems. UAE has many, many features and
equally many configuration options. If you don't know about them, it's likely
that UAE doesn't work for you, or doesn't work as good as it could.

Please read also the file "FAQ" which contains some Frequently Asked
Questions (and even the answers!) You should also look for a document
describing the specific port of UAE to the operating system you are using,
for example "BeOS/README" or "DOS/README".

People have complained that the UAE documentation contains only "weird jargon".
Sorry about this. Despite what MessySoft and Tomato tell you, computer
programs aren't always easy to use. UAE does require some assistance from you,
and therefore you should at least understand a bit about computers. After all,
you are an Amiga fan, so you should know what a Workbench is, don't you think?


Features
========

This version of UAE emulates:

- A 68000, 68010 or 68020 CPU, optionally a 68881 FPU
- OCS Graphics Chipset, plus big blits from the ECS Chipset
- Up to 2MB Chip RAM and up to 8MB Fast RAM, or 8MB Chip RAM without Fast RAM
- Up to 64MB Zorro III Fast RAM, independent of Chip RAM setting (68020 only)
- Up to 1MB Slow RAM, for extended compatibility with problem software
- Up to 8MB of graphics card memory, usable by software that supports
  Picasso 96 compatible graphics cards
- 4 x 3.5" floppy disk drives (DF0:, DF1:, DF2: and DF3:). It's not possible to
  read Amiga disks, so these are emulated with disk files.
- A hard-disk: either a harddisk image file or part of the native filesystem
- Joystick support (with option of mapping joystick to numeric keypad)
- Mouse support
- Ability to run in various screen modes (for better display quality or
  better speed)
- Full stereo sound support, consisting of 4 x 8bit channels
- Beta parallel and serial port support
- some other things which don't work well enough to mention them here...

  
Requirements (IMPORTANT! READ THIS!)/Limitations
================================================

Not emulated:
- Sprite to playfield collisions (sprite to sprite collisions work)
- An MMU (part of 68030/040 CPUs except those that Commodore used). This means
  you can't use virtual memory systems or real operating systems like Linux
  or BSD.
- The AGA chipset (A4000/A1200). This chipset has enhanced capabilites for
  up to 256 colors in all resolutions.
- Serial port emulation exists but doesn't work too well.

Since the PC floppy controller can't read Amiga disks (yes, that's a fact), 
floppy access has to be emulated differently: Floppies are emulated by means 
of disk files that contain a raw image of the floppy disk you want to emulate.
A disk file is an image of the raw data on an Amiga floppy disk, it contains
901120 bytes (880K), which is the standard capacity of an Amiga disk.

To actually run the program, you'll need to install the ROM image from your
Amiga. You can't run UAE if you don't have this image. It is not included
because it is copyrighted software. Don't ask me to send you one. I won't.
If you don't have an Amiga and still want to use UAE, you'll have to buy an
Amiga or at least the system software (ROM + Workbench) first.
The Kickstart image can have a size of either 256K or 512K. It must be named
"kick.rom" by default.

Read the section "tools" below for information how to create ROM images and
disk files.

If you don't have a Kickstart file, you may still be able to boot some games
and demos. The emulator includes some primitive bootstrap code that will try
to read and execute the bootblock of the diskfile you are using, and if that
bootblock only uses the one or two Kickstart functions that are supported by 
the "replacement Kickstart", your program will boot. Don't expect too much, 
though.

You'll also need some other software to run - why else would you want to
emulate an Amiga? There are several ways to make the software accessible to
UAE, either with disk image files or with a harddisk emulation. You should
make an image of your Amiga's Workbench disk and install it as "df0.adf"
(adf = Amiga Disk File) when you use UAE for the first time. More about how
to create these files in the chapter "Transferring software"

To use Picasso96 emulation, you need the Picasso96 libraries, which are also
not included. They can be obtained (e.g.) from Aminet.


Invoking UAE
============

First, read the system-specific documents for information how to set up UAE.
You should have an executable program called "uae". You can simply execute it,
but you can also optionally give it one or more of the following parameters:

 -h              : Print out a help text.
 -f file         : Load a configuration file
 -s opt=val      : Set the emulator's option "opt" to value "val".

Configuration files consist of several lines of the form "opt=val", just as
with the "-s" parameter.  You can use the following options with the "-s"
option, or in a config file.
[Here, "=n" means the option takes a number as value.  "=bool" means the option
takes a value of either "yes" or "no" (or "true", "false", or abbreviations of
any of these).  There are other classes as well.]

General options:
accuracy=n [default=2]
  Set emulator accuracy to n. The default is n = 2, which means the
  emulator will try to be as accurate as possible. This no longer
  does much in this version, and I'll probably remove it.
framerate=n [default=1]
  Sets the frame rate to 1/n. Only every nth screen will be drawn.  Using a
  higher value can speed up the emulator, at the expense of graphics quality.
autoconfig=bool [default=yes]
  If this is enabled, all expansion devices provided by the emulation will be
  automounted. You should only disable this if you have a Kickstart ROM
  earlier than 1.3 which can't cope with this. Some badly written games and
  demos might also be incompatible with this.
kbd_lang=lang [default=us]
  Set the keyboard language. Currently, the following values can be used: "us"
  for U.S. keyboard (default), "se" for swedish, "fr" for french, "it" for
  italian, "es" for spanish, or "de" for german keyboard.
  This setting only affects the X11 version.
floppy0=file [default=df0.adf]
  Try to use the specified file as diskfile for drive 0 instead of df0.adf.
  The options floppy1, floppy2, and floppy3 also exist.
kickstart_rom_file=file [default=kick.rom]
  Use the specified file instead of kick.rom as Kickstart image.
joyport0=mode [default=mouse]
  Specify how to emulate joystick port 0. You can use "mouse", "joy0", or
  "joy1" to use the corresponding input devices of your machine, or you can
  select several different keyboard replacements for a joystick:
    "kbd1" for the numeric pad.  '0' is the fire button.  Three keys on the
           numeric pad act as autofire toggle: '.' (or ',' depending on your
           keyboard language), Enter and the division key.
    "kbd2" for the cursor keys with right control key as fire button and the
           right shift key as autofire toggle
    "kbd3" for T/F/H/B with the left Alt key as fire button and the left Shift
           key as autofire toggle.
  The autofire toggle keys will turn on autofire (25 shots per second), it
  will stay enabled until you hit the autofire toggle again.
joyport1=mode [default=joy0]
  Like joyport0, but for the Amiga's joystick port 1.
use_gui=bool [default=yes]
  Show a user-interface that enables changing these options at run-time.
32bit_blits=bool [default=no]
  If enabled, the blitter emulation will use 32 bit operations where that
  seems profitable (note that this will cause bus errors on most  RISC
  machines)
immediate_blits=bool [default=no]
  If enabled, all blits will finish immediately, which can be nice for speed,
  but may cause incompatibilities.
cpu_speed=speed [default=4]
  This can have a value of "real", "max", or an integer between 1 and 20.
  "real" will try to give the CPU emulation exactly as many cycles, relative
  to the other chips, as on a real A500.  "max" will try to give you the
  maximum CPU emulation speed achievable on your machine.  Numeric values
  specify a fixed relation between CPU and custom chip emulation, where lower
  values prioritize CPU emulation, while higher values prioritize custom chip
  emulation.
cpu_type=type [default=68000]
  Controls which CPU is emulated. This can be "68000", "68010", "68020" or
  "68020/68881".  In some cases, you may need to use "68ec020" or
  "68ec020/68881" to emulate a crippled variant of the 68020 that has only a
  24 bit address bus.  Some software, including some Kickstart versions, does
  not work with a normal 68020 that has a 32 bit address bus.
  Careful: using an "ec" variant has harmful side effects, and should be
  disabled unless absolutely needed (you lose Z3 memory and Picasso
  emulation).
cpu_compatible=bool [default=no]
  If enabled, a slower but slightly more accurate variant of the CPU emulation
  will be used.  This is needed for some types of copy protection, among other
  things. This is only meaningful for a CPU type of "68000".
nr_floppies=n [default=4]
  The emulator will emulate this many external floppy drives.  Some very old
  games apparently have problems if this is larger than 1, but for all normal
  programs the default is good enough.

Emulating external devices (harddisk, CD-ROM, printer, serial port):
filesystem=access,volume:path [default=no filesystems mounted]
  Mount the host's file system at "path" as an Amiga filesystem with volume
  name "VOLUME:".  "access" can be either "ro" (for readonly), or "rw" (for
  read-write).  If you want to mount a CD-ROM, you should use a readonly
  mount.  You can mount multiple file systems.
  See below.
hardfile=access,secs,heads,reserved,bsize,file [default=no hardfiles mounted]
  Mount the hardfile "file" as an emulated harddisk, using a geometry of
  "secs" sectors per track, "heads" surfaces and "nr" reserved blocks.
  Each sector should have "bsize" bytes. This can be abused to mount
  floppy images.  You can mount multiple hardfiles.
  See below.

Sound options:
sound_output=type [default=none]
  The type of sound output can be "none" (no sound at all), "interrupts"
  (emulated for the internal side effects that can be noticed by programs,
  but no sound output), "normal" (emulated, and sound output), "exact" (a
  slightly more accurate emulation that may be necessary in some cases, but
  can also be slower).
sound_channels=type [default=mono]
  Can be "mono" or "stereo".
sound_bits=n [default varies across UAE versions on different OS types]
  Common values are 8 (low quality) or 16 (high quality)
sound_frequency=n [default varies across UAE versions on different OS types]
  Common values are 22050 or 44100. The quality of sound output increases with
  the frequency.
sound_min_buff=n
sound_max_buff=n [default varies across UAE versions on different OS types]
  You can specify the minimum and maximum size of the sound buffer.
  Smaller buffers reduce latency.  Usually only the minimum size is used.
sound_interpol=type [default none]
  Normally, sound samples are output exactly as they are computed, without
  any post-processing.  This can generate errors in the sound output when the
  output frequency isn't an even multiple of the input frequency.  These
  errors are usuable perceived as a high-frequency noise.
  There are currently two types of interpolation available, both under
  experimentation.  You can use either "rh" or "crux" as value for this
  option.  Note that no interpolation is supported for 8 bit output; you need
  to use 16 bit output to hear a difference.  If you have any comments about
  the effects of either method on audio quality, I'd be very interested to
  hear them.

Memory options:
bogomem_size=n [default=0]
  Emulate n*256K slow memory at 0xC00000. Some demos/games need this.
fastmem_size=n [default=0]
  Emulate n megabytes of fast memory as an expansion board.
z3mem_size=n [default=0]
  Emulate n megabytes of Zorro III fast memory as an expansion board.
chipmem_size=n [default=4]
  Emulate n*512K chip memory. Some very broken programs need specific amounts
  of chip mem to work properly. The largest valid value is 16, which means 8MB
  chip memory.

Display options:
gfx_width=n [default=800]
  Use a window that is n pixels wide for displaying the Amiga screen.
gfx_height=n [default=300]
  Use a window that is n pixels high for displaying the Amiga screen.
gfx_lores=bool [default=no]
  Enable this option if you use a very small window width (320 to 400 pixels)
  to shrink the display horizontally.
gfx_linemode=type [default=none]
  The type can be none (every line is drawn once), "double" (every line is
  drawn twice), and "scanlines" (every line is drawn once, but the image is
  stretched vertically by inserting a black line every other line to simulate
  the display on an old monitor).
  The "double" mode gives best results, but slows down the emulation quite a
  lot. Don't use the "none" mode if you want a decent interlace emulation.
  If you use "double" or "scanlines", your window needs to be twice as high
  as when using the "none" mode.
gfx_correct_aspect=bool [default=none]
  Try to fit the image into the specified window dimensions by leaving out
  certain lines.  Useful if you want to fit a 640x512 Amiga display in a
  640x480 window.
gfx_center_vertical=bool [default=no]
gfx_center_horizontal=bool [default=no]
  If you use a smaller window than 800x300 (400x300 with "gfx_lores" option or
  800x600 with a gfx_linemode other than "none"), not all parts of the display
  will fit on the screen. By enabling the necessary centering options, you can
  ask the emulator to try and move the screen contents so that the relevant
  parts are displayed. If you are unlucky, this can cause the contents to jump
  around a bit in certain cases.
gfx_fullscreen_amiga=bool [default=no]
  Enable if you want to use the full screen, not a window on the desktop, for
  the Amiga display.  Some ports (DOS, SVGAlib) always use fullscreen mode.
gfx_fullscreen_picasso=bool [default=no]
  Like gfx_fullscreen_amiga, but for the Picasso graphics card display.
gfx_color_mode=mode [default=8bit]
  Select a color mode to use.
  Color modes: 8bit (256 colors), 15bit (32768 colors), 16bit (65536 colors),
	       8bit_dithered (256 colors, with dithering to improve quality),
	       4bit_dithered (16 colors, dithered); 32bit (16 million colors)
gfxcard_size=n [default=0]
  Emulate a Picasso 96 compatible graphics card with n MB graphics memory.
  This requires that you use set the CPU type to "68020" or higher, and that
  you do not use 24 bit addressing.

Debugging options (not interesting for most users):
use_debugger=bool [default=no]
  If enabled, don't start the emulator at once, use the built-in debugger.
log_illegal_mem [default=no]
  If enabled, print illegal memory accesses


Whew. You'll probably have to experiment a little to get a feeling for it.


You can also put these options into a configuration file in your home
directory. Simply create ~/.uaerc and put some of these options in it. On
non-Unix systems, the file is called uae.rc and should be located in the
current directory.


Choosing color and screen modes
===============================

As described in the previous paragraph, UAE can run in many different 
resolutions and color modes. However, few of the color mode options are
available if you use the X11 version of UAE, since the X server determines
how many colors are available. If you are running a 256 color X server, you
can use "-H3" to tell UAE to dither the colors for better results.

You will have to experiment which mode gives the best results for you at a
satisfying speed. Note that the dithering process consumes time, so even if
256 colors with dithering look better than 256 colors without, remember that
UAE will be slower in that mode.

The recommended resolution is 800x600. In the lower resolution modes, some
overscan pictures the Amiga tries to display may not fit entirely on the
screen, others may be off-center and some graphical effects may look weird.
For best results, use 800x600 with at least 32768 colors.
For speed, use 400x300 lores with 256 colors.

_Don't_ use 24 bit or 32 bit screen modes, unless you absolutely have to.
These are way too slow to be usable.


Harddisk emulation
==================

Since using diskfiles is awkward, it is necessary to emulate harddisks. There
are two ways how you can use large amounts of data with UAE: harddisk files
and mounted directories.

1. Harddisk files

Harddisk files are large files that contain the image of an Amiga filesystem.
They work much the same way as a disk file. You can simply create a large
empty file and tell UAE to use it as a hardfile, but you will need to format
it from the emulation before you can actually use it.

Under Unix, You can create a (unformatted) harddisk file with
  dd if=/dev/zero of=hardfile bs=512 count=16384
That will create an 8MB file. Other ports of UAE may come with a utility
called "makedisk" or other ways to create such a file.

To tell the emulator that you want to use a certain file as a hardfile, use
the "-W" option, for example
  uae -W 32:1:2:hardfile
The first three numbers are geometry information which tell the AmigaOS how
the file is organized. The first number (32) is the number of sectors per
track, the second number (1) is the number of heads or surfaces, the third
number (2) is the number of reserved blocks. If you use "normal" sizes
(powers of two, like 32MB), then you should be OK using the same numbers as
in the above example. Using different numbers can make sense if you transfer
the image of a real Amiga harddisk which uses a different geometry. The last
field of the argument to the "-W" option is the name of the harddisk file.

If you are using Kickstart 1.3 or earlier, hardfiles can't currently be
mounted at boot time, and therefore you can't boot from it either. You will
have to boot either from a floppy disk image or from a filesystem (see below),
and mount the hardfile.device later. To do this, add the following to
"DEVS:mountlist":

UAE0:	   Device = uaehf.device
	   Unit   = 0
	   Flags  = 0
	   Surfaces  = 1
	   BlocksPerTrack = 32
	   Reserved = 1
	   Interleave = 0
	   LowCyl = 0  ;  HighCyl = 511
	   Buffers = 5
	   DosType = 0x444F5300
	   BufMemType = 1
#

(You may need to adjust the values if you specified a different geometry,
and/or your hardfile has a different size than 8MB, and/or the hardfile is not
mounted as UAE0: because you mounted other harddisks before it.)

Then, type "mount UAE0:" (or put that command in your startup-sequence), and
you should be able to access it. Don't forget to format it with the AmigaDOS
format command:

  format drive uae0: name Mister_Willwink

b) Accessing native filesystems from the emulator

This has some major advantages:
 - It has no problems with Kickstart 1.3
 - It is more convenient.
 - It is much faster.

If you specify the -M or -m command line arguments, you your native filesystem 
from the emulator. If you start UAE with

  uae -m sound:/usr/amiga/modules

you can access all the files in /usr/amiga/modules by reading from the
AmigaDOS volume "SOUND:".
(DOS users: try "uae -m dh0:C:\" to mount your drive C:\ as DH0:)

You can mount up to 20 devices, either hardfiles or filesystems, by giving
either of these options multiple times. The volumes will be named UAE0:,
UAE1:, etc. UAE will boot from UAE0: if no diskfile is found for floppy
drive 0.
You can also use native filesystems to mount Amiga CD-ROMs, and you can
abuse the hardfile emulation to mount floppy disks: "uae -W 11:2:2:wb13.adf"
will mount the diskfile "wb13.adf".


Tools / Transferring files
==========================

As you should know by now, you need to transfer files between your Amiga and
the machine you run UAE on. There are several ways how to do this.

- Using a null modem cable, and a terminal package running on each machine,
  you can transfer the file(s) via Zmodem upload/download. 68000 equipped
  Amigas can normally attain around 3000cps through the null modem cable,
  using the standard Commodore serial.device.  However, by using the device
  replacement BaudBandit.device, anything up to 5500cps can be attained.
  BaudBandit can be obtained from Aminet.  A second alternative is to use
  the BASIC program adfi.bas (included with UAE) to transfer a file from the
  Amiga to the PC via the null modem cable.
  
- If you're using CrossDOS on your Amiga, you can compress the disk or
  kickstart image using LhA or similar PC compatible archiver and copy it to
  a 720KB floppy disk.  You can now take the disk over to the PC, copy the
  compressed file to the UAE directory and uncompress it.
  If you don't have CrossDOS on the Amiga, there is a similar freeware tool
  called Msh, which can be found on Aminet or on Fish disk 382 or 327.

In either case, you ought to read the documentation for the programs that
you use for the transfer. These programs can't be explained here.

In the "amiga" subdirectory you'll find two small Amiga programs that will
help you to generate the necessary image files. These are called transrom 
and transdisk. Copy them to your Amiga and make them executable (by typing
"protect transrom rwed" and "protect transdisk rwed" in the Amiga shell
window).
transrom will dump the contents of your Kickstart ROM, and transdisk will 
dump an image of a floppy in one of the drives. Both programs write to the
standard output (read: the screen), so you'll want to redirect that. Do

   transrom >ram:kick.rom
   
to create a file called "kick.rom" in the RAM disk, and

   transdisk >ram:df0.adf
   
to create a file called "df0.adf" in the RAM disk. These files are pretty
big, 262144 or 524288 bytes for the ROM image and 901120 bytes for a disk 
image.

NEVER run either of these programs from the Workbench. Always open a Shell
or CLI window to do this.

transdisk understands the following arguments:

    -d device unit: Use this device instead of DF0:
    -s n:           Begin transfer at track n (default: 0)
    -e n:           End transfer at track n (default: 79)
    -w file:        don't read from the floppy, instead write the contents
                    of "file" to the floppy
    -h:             Treat the disk as high-density disk. HD images aren't
                    supported by UAE yet, though. Note that the resulting
		    file will be twice as big.

So, to transfer the disk in drive DF1:, you'd give the command:

  transdisk >ram:df1.adf -d trackdisk 1

If you don't have much RAM and can't fit all of a disk image in the RAM disk,
you can split up the transfer into multiple parts with the "-s" and "-e"
parameters. To transfer the disk in four parts, you'd use the following 
commands:
  
  transdisk >ram:df0_1.adf -s 0 -e 19
  transdisk >ram:df0_2.adf -s 20 -e 39
  transdisk >ram:df0_3.adf -s 40 -e 59
  transdisk >ram:df0_4.adf -s 60 -e 79

Of course, you should save each of the four files to another place before
transferring the next one with transdisk to make space in your RAM disk. 
If you have all the files on your PC, you can do the following under Unix:
  cat df0_1.adf df0_2.adf df0_3.adf df0_4.adf >df0.adf
or, under DOS:
  COPY /B df0_1.adf+df0_2.adf+df0_3.adf+df0_4.adf df0.adf
I've been told there are the following tools for the Mac to join binaries:
"ChunkJoiner 2.1.2" found under Info-Mac's <disk> directory or 
"JoinFiles 1.0.1" under Info-Mac's <text>.

The current transdisk can only read the standard AmigaDOS format. This means
that most games that rely on some form of copy-protection cannot be
transferred (more about disk formats in the file "FAQ")

****************************************************************************
If you transfer commercial software, you must not distribute the resulting
image files, since that would be a violation of copyright law. The Kickstart
ROM has to be considered commercial software. You may only use the Kickstart
from your own Amiga, and you may not distribute Kickstart ROM files.
Please read the license that came with your software for details.
****************************************************************************


Retrieving files from a disk image
==================================

If you have a disk image file, and you want to retrieve the files from it, you
can use the "readdisk" tool. It is automatically built by "make". If you have
a disk image of a disk called "Workbench1.3D" as df0.adf, and you do
   readdisk df0.adf
the whole directory structure of the disk image will be stored in a newly
created subdirectory called "Workbench1.3D". You can optionally give a second
parameter to specify a directory where to create the output other than the
current directory.
readdisk only understands about the OFS right now. FFS disks will cheerfully
be regarded as being unreadable. Use the unixfs.device from within the
emulator if you want to transfer files from FFS disks.


Picasso 96 graphics card emulation
==================================

To use this feature, you must select 68020 emulation with a 32 bit address
space. You also need a Kickstart 3.x ROM.

To specify how much graphic memory you want to emulate, use the "-U" option,
e.g. "-U 4" for 4 megabytes. Then, you need the Picasso 96 software which
is not distributed with UAE (There will be a link to the Picasso 96 home page
on the UAE Web page soon). Version 1.31 or higher is recommended.
Install the Picasso software, and make sure you enable the "uaegfx" driver.
After that is complete, reboot, and you should be able to select the new
modes from the ScreenModes program.


UAE SCSI device
===============

To enable SCSI support, use --enable-scsi-device when running configure.
The emulator provides a uaescsi.device. This device only supports
direct SCSI, which is sufficient to run applications like MakeCD. The
device does not support reading or writing with the normal Exec commands,
so you cannot mount filesystems on it right now.

The unit numbers of the uaescsi.device follow the Amiga SCSI
conventions: unit number "xyz" maps to the lun y of target z on bus
x. Wide SCSI busses can have targets with numbers larger than 9. In
this case the uaescsi.device pretends that there is another SCSI
bus. To avoid confusion, all available SCSI targets are listed
together with their unit number when starting UAE. Devices cannot be
added while the emulator is running.  Reseting it is not sufficient
either for technical reasons.

The implementation of the uaescsi.device uses cdrecord's libscg as
interface to the native SCSI system. The Linux implementation of this
library used to be included into UAE, but now the library as generated
by the cdrecord source package (ftp://ftp.fokus.gmd.de/pub/unix/cdrecord/)
is used. As the library is not distributed seperately, you will have
to get the whole cdrecord sources, compile it and then make several
header and lib files available to the compiler if (and only if) building
UAE with SCSI support. The script "src/install_libscg" copies the files
required for the libscg in cdrecord 1.8.1.

Using threads is strongly recommended, because some SCSI commands can
run for extended periods of time and would block the whole emulation
during this time without threads. Use --enable-threads when starting
configure.

Depending on the hosts capabilities the uaescsi.device may be limited
compared to other Amiga SCSI devices. The Linux kernel by default only
allows 32KB of data per SCSI command and does not always perform SCSI
requests in parallel.

Setting the chunk size in MakeCD to 30KB is already too much and
causes an IO error -4 (IOERR_BADLENGTH), because the setting is only
used as a guideline. You can work around this by setting the Tooltypes
BUFFER_CHUNK_XXX to 29. On a Pentium II 350MHz with Adaptec UW SCSI
controller on board on-the-fly copying was possible from a Philips
CDD2600 (SCSI) to a Yamaha CRW4416E (IDE) at 4x.


The UAE_CONTROL program
=======================

In the "amiga" subdirectory, you will find two programs, uae_control and
uaectrl that provide the same functionality as the X11 GUI. uaectrl is
shell-based and works with any Kickstart, while uae_control needs the
gadtools.library and a recent version of reqtools.library, so it only works
with Kick 2.0 and upwards. Copy these two programs to the directory that you
use for harddisk emulation. They should be self-explanatory.


The timehack
============

Another tool in the "amiga" subdirectory, timehack, synchronizes the
emulated Amiga's system time with the host's time every second. This
is useful when the emulation is not done in real-time or is suspended
completely.


Quick overview of the debugger commands
=======================================

Some (window-system based) ports of UAE have a built-in debugger. You can
press ^C at any time to enter this debugger.
Each debugger command consists of a single letter and occasionally some
parameters.

g:                    Start execution at the current address. 
c:                    Dump state of the CIA and custom chips.
r:                    Dump state of the CPU
m <address> <lines>:  Memory dump starting at <address>
d <address> <lines>:  Disassembly starting at <address>
t:                    Step one instruction
z:                    Step through one instruction - useful for JSR, DBRA etc.
f <address>:          Step forward until PC == <address>
q:                    Quit the emulator. You don't want to use this command.
M:                    hunt for sound modules
S <filename> <address> <len>:
                      save a sound module
C <value>:            Search for values like energy or lifes in games
W <address> <value>:  Write into Amiga memory


Sound
=====

If your version of UAE supports sound, you can pass parameters like frequency
or number of bits to use on the commandline; if you don't specify any, sane
defaults will be used. If graphics output is enabled while sound is output,
the emulator will be much too slow on most systems. The sound will not be
continuous. Therefore, a hack to turn off screen updates is provided: Press
ScrollLock to disable graphics, press it again to enable them.

The quality of the emulation depends on the setting of the "-S" commandline
option. With "-S 3", all of the sound hardware is emulated; and some programs
(e.g. AIBB) won't run with other settings. "-S 2" should sound just as good as
"-S 3" and will be much faster for some programs. "-S 1" tries to emulate most
of the sound hardware, but doesn't actually output sound. "-S 0" completely
turns off sound.


Pointers
========

There are a few sites in the Internet that contain helpful information about
UAE.

The new "official" UAE page is located at

  http://www.freiburg.linux.de/~uae

thanks to Stefan Reinauer who is now maintaining it.

There, you will find links to other UAE pages. One which is especially useful
is the "UAE Discussion Board" set up by Gustavo Goedert, the address is

  http://amiga.nvg.org/uaeboard

There is supposedly a newsgroup named "alt.emulators.amiga", but I don't get
it here.
The newsgroup "comp.sys.amiga.emulations" appears to be a proper place to
discuss Amiga emulation, but, strictly speaking, it is _not_ the right place.
More appropriate places are "comp.emulators.misc", and, of course, Gustavo's
discussion board.

Petter Schau has written another Amiga emulator named "Fellow".  It's mostly
written in x86 assembly and only runs under DOS.  It's quite compatible and
generally faster than UAE.  The Fellow homepage is at

  http://www.geocities.com/SiliconValley/Peaks/5244/


Thanks & Acknowledgements
=========================

Thanks to all who have written me so far with bugreports and success/failure
reports when trying to run the emulator on various hardware with different
Kickstart versions. A list of everyone who has contributed to the source code
can be found in the CREDITS file (this was getting too big to keep it here).

Special thanks to:
  - Jay Miner, Dale Luck, R.J. Mical and all the others who built the Amiga.
  - Felix Bardos, whose HRM I "borrowed".
  - Hetz Ben Hamo mailed Peter Kittel from Commodore asking for permission to
    give Kick 1.3 away. Unfortunately, the response was negative :-(
  - Stefan Reinauer, for hosting the UAE Web page after the RWTH decided it's
    too dangerous to let students have their own Web pages.
  - Bruno Coste, Ed Hanway, Alessandro Soldo and Marko Nippula provided useful
    documentation about the Amiga
  - Fabio Ciucci gets the "Best bug reports" award for his help with the
    blitter line emulation and other problem areas.
  - Michael C. Battilana and Cloanto Software, for all their support.
  - Julian Eggebrecht of Factor 5, for providing several F5 games and a lot
    of valuable input.
    Factor 5 has made Katakis, one of their classic Amiga games, freely
    available for download. There are still some good people left in the
    world...
  - Jens Schönfeld, inventor of the Catweasel controller, donated one
    controller card.
  - Jürgen Beck, maintainer of the Amiga emulation web site "Back to the
    Roots" (http://back2roots.emuunlim.com) and everyone else who spends
    time writing to software companies asking for permission to distribute
    old Amiga games.
  - all the software companies who allow distribution of their Amiga games on
    sites like "Back to the Roots".


Authors/Maintainers
===================

My address is (please read the section "Before you send email" below):

crux@pool.informatik.rwth-aachen.de

or, via snailmail

Bernd Schmidt
Schlossweiherstrasse 14
52072 Aachen
Germany

Email is more likely to be answered, and will definitely be answered much
faster. Please avoid phonecalls if you can.
I won't distribute software, neither PD or commercial. Don't send me floppy
disks without at least asking first, you will not get them back.

The following people have ported UAE to different platforms; you should
direct system-specific questions to them:

DOS port:
  Gustavo Goedert <ggoedert@netrunner.com.br>
  Available: http://www.netrunner.com.br/dosuae
  Sourecode: available on the above Web page, most of it included in the
             main source (with some delay)

Mac port:
  Originally: Ernesto Corvi <someone@imagina.com>
  Currently: Arnaud Blanchard <jblancha@pratique.fr>
  Available: http://www.pratique.fr/~jblancha/
  Sourcecode: extra package available. Bits and pieces in the main source,
              but nothing you could get to compile.

BeBox port:
  Christian Bauer <bauec002@goofy.zdv.uni-mainz.de>
  Available: The main UAE web page (use the Unix sources)
  Sourcecode: Included in the main source. Should compile OK.
  Notes: Christian says he doesn't have much time to spend on UAE, so if
         anyone is willing to help maintain this port, please speak up.

NextStep port:
  Ian Stephenson <ians@cam-ani.co.uk>
  Available: The main UAE web page (use the Unix sources)
  Sourcecode: Included in the main source. Should compile OK.
  Notes: Ian says he doesn't have much time to spend on UAE, so if
         anyone is willing to help maintain this port, please speak up.

Amiga port:
  Originally: Olaf 'Olsen' Barthel <olsen@sourcery.han.de>
  Currently: Samuel Devulder <devulder@info.unicaen.fr>
  Available: Not quite sure yet. Paul Liss' Web page has binaries.
  Sourcecode: Included in the main source. Should compile OK.

pOS port:
  Samuel Devulder <devulder@info.unicaen.fr>
  Available: Not quite sure yet.
  Sourcecode: Included in the main source. Should compile OK.

OS/2 port:
  Pressenna Sockalingasamy <deathlok@cww.de>
  Available: ftp://hobbes.nmsu.edu/pub/os2/apps/emulator/uae2_0810_a1.zip
  Sourcecode: working on including it

XFree86/OS2 port:
  Krister Bergman <bellman@kuai.se>
  Available: http://www.kuai.se/~bellman/html/xfreeapps.html
  Sourcecode: nothing special, apparently the Unix stuff compiles cleanly (?)

Win32 port:
  Originally: Mathias Ortmann <ortmann@informatik.tu-muenchen.de>
  Currently: Brian King <Brian_King@codepoet.com>
  Available: http://www.codepoet.com/uae
  Sourcecode: bits merged into the main source, the rest available from the
              URL above. Still trying to merge more of it...

Acorn RISC PC port:
  Peter Teichmann <sol@Space.WH1.TU-Dresden.De>
  Available: http://www.wh1.tu-dresden.de/~sol/acorn.shtml
             http://www.wh1.tu-dresden.de/~sol/acorne.shtml
  Sourcecode: Some of it is included in the main source, but since Acorn's OS
              apparently doesn't have decent file handling, you can't even
	      use the same source layout. Also needs lots of additional files.
	      
Since I generally don't have the possibility to test or improve these ports,
it is a good idea to contact their respective authors if you have questions.


Before you send email...
========================

Before you contact me with a problem that you have, make sure you have read
_all_ of the above. Please read also the file "FAQ", which contains a lot of
helpful information, and the README file for your specific system. 

I can't answer _every_ question. If you have trouble understanding this
README, either because you don't speak English very well or because you have
no clue at all about computers, please try to find some friend of yours who 
does understand this file and who can translate/explain it for you. I simply
can't explain (for example) how to use terminal programs or CrossDOS because
I don't use either, and it would be much too time-consuming anyway. This file
and the file FAQ contains about every piece of information I can give you. I 
try to help people who have questions, but sometimes it takes too much time.

Please don't ask for Kickstart ROM files or other copyrighted software. Don't
_send_ me stuff like this either. If you want to send me something else which
is big (>= 50K), ask me before or put it somewhere in Webspace.
If I get 3MB of screen shots or a core dump ("it doesn't work, it generates
this file"), I'm very likely to get extremely angry, I might complain to your
sysadmin, and you might lose your account. Think twice.

I'm also going to be extremely annoyed if you send email in HTML format.
Fight this disease!

Oh, and another thing: If I promise to do things (like implement new
features), and forget about them, pester me. That happens occasionally, it's
a known bug in my brain. I'll have it replaced.
