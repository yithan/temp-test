NOTE: The following instruction is for runnning MITSIMLab with SCATS
traffic control on Ubuntu 11.10 or 11.04.

### **Cloning the Repository**

Do the following: (Note: Downloading is Slow)

`  cd ~`
`  git clone -b SCATS `<ssh://USERNAME@172.25.184.11/home/git/repositories/mitsim>` view_CL`

...where USERNAME is your FM Server username. Note that you _must_
clone this repository into view_CL; this is one of the quirks of the
mitsim build system.

### '''Installing Required Packages '''

1\) Always work on an up-to-date system:

`  sudo apt-get update`
`  sudo apt-get upgrade`

2\) Most of the necessary packages are already available via apt:

`  sudo apt-get install g++ autoconf xutils-dev patch bison++ pvm-dev libxp-dev libxp6 libxmu-dev libxmu6 libnetcdf-dev libnetcdf6 libxtst-dev libxt-dev x11proto-print-dev libxpm-dev libXext-dev libxtst-dev libmotif-dev`

3\) Double-check your version of gcc (I know 4.5 works; 4.4 and 4.6
probably will too but haven't tried it.)

`  gcc --version`
`  g++ --version`

4\) Double-check your version of flex:

`  flex --version`
`  ...should be 2.5.4. Otherwise you might have to install flex-old (but try compiling it first anyway).`

### **Install XMT**

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

### **Install XBAE**

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

### **Install pvm3 in home directory**

1\) Download pvm3 pacakage pvm3.4.6.tgz from:

`  `<http://netlib2.cs.utk.edu/pvm3/pvm3.4.6.tgz>

2\) Put the pacakage under /home/"username" folder

3\) Extract it:

`  tar zxvf pvm3.4.6.tgz`

4\) Set the PVM_ROOT and compile PVM:

`  cd ~`
`  gedit .bashrc`
`  Add the following at the end of your ~/.bashrc:`
`  export PVM_ROOT=$HOME/pvm3`
`  source .bashrc`
`  cd pvm3`
`  make`

5\) Add the pvm binaries to your path:

`  cd ~`
`  gedit .bashrc`
`  Add the following at the end of your ~/.bashrc:`
`  export PATH=$PATH:~/pvm3/bin/LINUX:~/pvm3/lib/LINUX`
`  source .bashrc`

6\) Set the pvm_hosts:

`  cp ~/view_CL/.pvm_hosts ~/`
`  gedit ~/.pvm_hosts`
`  add the following at the end of .pvm_hosts file`
`  `<your computer name>` ep=$SIMLAB_Linux wd=$SIMLAB_DAT`

6\) Restart pvm:

`  pvm`
`  quit`
`    `

### **Run MITSIM**

1\) Add the following at the end of your \~/.bashrc:

`  export XENVIRONMENT=~/view_CL/lib/ad/xmitsim.ad`
`  export PATH=$PATH:~/view_CL/bin/linux_CL`

`  ...and then do:`
`  source ~/.bashrc`

2\) Start pvm, configure, and push it to the background:

`  pvm`
`  conf`
`  ...make sure that your machine's name appears; you should see something like "1 host, 1 data format"`
`  quit`

4\) Make sure all binaries in \~/view_CL/bin/linux_CL and
\~/view_CL/simlab/bin/linux_CL are executable. If not, chmod 777

5\) Run the Marina Bay example:

`  cd ~/view_CL/data/MarinaBay`
`  check the paths in master.mitsim, master.tms, run_smc.sh are set correctly`
`  change the HOST in run_smc.sh to your host name`

`  To run mitsim with traffic control and GUI, execute:`
`  ./run_smc.sh`