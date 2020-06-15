NOTE: This fails on Ubuntu 11.04 with the original buffer overflow
error. So it's still 10.10 for now. I'll double-check an library
differences and see what might be causing it.

### *' Cloning the Repository*'

Do the following: (Note: Downloading is Slow)

`  cd ~`
`  git clone `<ssh://USERNAME@172.25.184.11/home/git/repositories/mitsim>` view_CL`

...where USERNAME is your FM Server username. Note that you _must_
clone this repository into view_CL; this is one of the quirks of the
mitsim build system.

### *' Installing Required Packages*'

1\) Always work on an up-to-date system:

`  sudo apt-get update`
`  sudo apt-get upgrade`

2\) Most of the necessary packages are already available via apt:

`  sudo apt-get install xutils-dev  patch   bison++   pvm-dev   pvm  libxp-dev libxp6   libxmu-dev   libxmu6  libnetcdf-dev libnetcdf6   libxtst-dev   libxt-dev    x11proto-print-dev   libxpm-dev   libXext-dev   libxtst-dev   libmotif-dev`

`  Note: Ubuntu 10.10 uses libmotif3, but 11.04 uses libmotif4. By installing "libmotif-dev", you get whichever one your system prefers. I have tested the install on both libmotif3 and libmotif4, and both work fine. `

3\) Double-check your version of gcc (I know 4.5 works; 4.4 and 4.6
probably will too but haven't tried it.)

`  gcc --version`
`  g++ --version`

4\) Double-check your version of flex:

`  flex --version`
`  ...should be 2.5.4. Otherwise you might have to install flex-old (but try compiling it first anyway).`

5\) Now is a good time to run make-depends:

`  cd ~/view_CL/simlab`
`  make clean`
`  make depend_all`

...if this fails, you probably won't get any further.

`  Note: Warnings about standard library includes (like "iostream") are expected.`

### *' Install XMT*'

You'll have to install XMT manually. Reason: The "expected" version of
XMT seems to be xmt200, which is very buggy. Version xmt400 is much more
stable, and only requires a small amount of patching to get to work.

1\) Download the source from:

`  `<http://sourceforge.net/projects/motiftools/files/Xmt/Xmt400/xmt400.tgz>

2\) Extrace it. Assuming you downloaded the source into the default
location, then do something like this to extract it:

`  cd ~/Downloads`
`  tar xvf xmt400.tgz`

3\) Patch it. There is a MAJOR bug in all versions of Xmt which leads to
buffer overflows if you have more than 10 separators in a Menu.

`  cd ~/Downloads/xmt400`
`  chmod 666 Xmt/Menu.c`
`  patch Xmt/Menu.c  < ~/view_CL/simlab/xmt400_patch.diff`

3\) Configure and build it:

`  cd ~/Downloads/xmt400`
`  xmkmf`
`  make World 2>&1 | tee makelog`

`  Note: xmkmf should be installed by default. If not, you'll have to find it somewhere in the repositories. `
`  Note: "tee" means you'll see the output, but you will also have a copy in "makelog" in case you run into any errors. `

4\) Install it:

`  cd ~/Downloads/xmt400`
`  sudo make install`

`  Note: Scan the output and make sure there's nothing which is an obvious error.`

### ''' Install XBAE '''

You'll have to install XBAE manually. Reason: At least on Ubuntu 10.10,
xbae links against an older version of libXm. Since we link to the newer
libXm manually, this leads to symbol conflicts. (You'll get a warning
when you compile, and a crash at runtime.) This is almost definitely the
source of the original crash.

1\) Download the source from:

`  `<http://sourceforge.net/projects/xbae/files/xbae/4.60.4/xbae-4.60.4.tar.gz/download>

2\) Extract it. Assuming the default download location:

`  cd ~/Downloads`
`  tar xvf xbae-4.60.4.tar.gz`

3\) Configure and build it:

`  cd ~/Downloads/xbae-4.60.4`
`  ./configure`
`  make`

4\) Install it:

`  cd ~/Downloads/xbae-4.60.4`
`  sudo make install`

`  Note: Again, check the output. make install runs some checks.`

5\) Make it visible to LD_CONFIG:

`  echo "/usr/local/lib" | sudo tee --append /etc/ld.so.conf`
`  sudo ldconfig`

`  Note: You might want to perform:`
`  cat /etc/ld.so.conf`
`  ...and ensure that "/usr/local/lib" is only listed once. (It won't be there unless you manually set it yourself at some point.) `

### ''' Build and Install MITSim '''

1\) This will take a while:

`  cd ~/view_CL/simlab`
`  make`

`  Note: you may have to "chmod 755" the file "~/view_CL/simlab/Version.pl". (You'll know because you get an error that refers specifically to this file.)`

2\) Install it:

`  cd ~/view_CL/simlab`
`  make install`

`  Note: Install puts everything in your home directory, so you don't need to sudo this.`

3\) Check if the "ad" files were copied correctly:

`  ls ~/view_CL/lib/ad`

`  If the folder is empty, do the following:`
`  cd ~/view_CL`
`  cp simlab/ad/*.ad lib/ad`

### ''' Test It '''

If you've used MITSim before, please ignore this section.

1\) Add the following the end of your \~/.bashrc:

`  export XENVIRONMENT=~/view_CL/lib/ad/xmitsim.ad`
`  export PATH=$PATH:~/view_CL/bin/linux_CL`

`  ...and then do:`
`  source ~/.bashrc`

2\) Start pvm, configure, and push it to the background

`  pvm`
`  conf`
`  ...make sure that your machine's name appears; you should see something like "1 host, 1 data format"`
`  quit`

3\) Run the brunnsviken sample (or just go straight to step 4 if you
prefer the GUI).

`  cd ~/view_CL/data/brunnsviken`
`  mitsim -m master.mitsim`

4\) Run the graphical version:

`  cd ~/view_CL/data/brunnsviken`
`  xmitsim -m master.mitsim`

### '''General Comments '''

1\) I manually set "OSTYPE" and "HOST" in "general.tmpl". This is
because "OSTYPE" is actually a standard environment variable, and is
equal to "linux-gnu" on GNU-based systems (like Ubuntu), so make would
fail --and setting this in your .bashrc doesn't seem right (again,
becasue the default value is already set).

2\) The standard-library include \<generic.h\> hasn't been around in
forever. The functionality there (intended to do fancy things before
templates were available in C++) was moved into \<netcdfcpp.h\>; I
replaced these includes in two files in the Xmw/ directory. (This is
another change that I feel is more stable to make then to simply work
around; feel free to play around with includes if you think this
introduces breaking changes.)