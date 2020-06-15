<center>

<font size="+3">New Developers' Guide</font>

</center>

## **Introduction**

If you are a new developer, welcome to Project DynaMIT\! This page will
help you get started acquiring the code, compiling it, and learning
where to go for information on the various files and classes in the
project.

After you finish the tutorial, you should be able to:

1.  Get the latest DynaMIT source code.
2.  Impoprt the DynaMIT source code into Eclipse IDE.
3.  Compile DynaMIT.
4.  Run DynaMIT-R with one example network.
5.  visualize DynaMIT-R's outputs.

## **Additional Resources**

`Press here `[`for``   ``useful``   ``videos`](Videos "wikilink")

`Press here `[`for``   ``other``   ``useful``
 ``materials`](Materials "wikilink")

## **Operation System**

DynaMIT is designed and implemented on Linux OS.

The source code of DynaMIT, without modifications, may not be be able to
be compiled on other systems. The below platforms have been successfully
tested by our team.

  - Ubuntu 10.10/11.04/11.10/12.04/12.10 (32-bits is suggested)
  - Oracle VirtualBox + Ubuntu.iso + Mac OS
  - Oracle VirtualBox + Ubuntu.iso + Windows 7

Besides:

1.  If you are using other Linux-like OS, I guess you can succeed. (This
    tutorial focus on Ubuntu, so the commands might be different on your
    OS)
2.  If you are using other versions of Ubuntu (higher than 10.04), I
    guess you can succeed.
3.  If you are using other OS, I strongly suggest you to install Oracle
    VirtualBox.
4.  If you are using other Virtual Machines, we do not guarantee, but it
    should be fine.

Below, we give some helps to install Oracle VirtualBox on Mac OS and
Windows7.

If you are using Linux, you can skip to next section.

#### **Install VirtualBox + Ubuntu.iso on Mac OS**

Please follow the guidance in
<http://www.tuaw.com/2009/09/07/how-to-set-up-ubuntu-linux-on-a-mac-its-easy-and-free/>

If you meet with questions, you are welcome to ask questions in
Wiki/General Questions/Questions or send us email.

#### **Install VirtualBox + Ubuntu.iso on Windows 7**

(You can also watch the video [Videos](Videos "wikilink"))

1.  Download VirtualBox
      - <https://www.virtualbox.org/wiki/Downloads>, if the link is not
        valid, please Google "Oracle VirtualBox Download"
      - Select: *VirtualBox 4.1.18 for Windows hosts x86/amd64*
2.  Install VirtualBox
      - install VirtualBox with the default path. You can watch the
        video for more detailed instructions.
        <http://www.youtube.com/watch?v=XajMLO8v65w>.
3.  Download Ubuntu.iso
      - <http://releases.ubuntu.com/natty/>, suggest you to use Ubuntu
        11.04 (natty) \[32-bits OS\]
      - Select: *ubuntu-11.04-desktop-i386.iso*
4.  Setup Linux OS Environment
    1.  Start VirtualBox
    2.  Configure VirtualBox
    3.  Install Ubuntu.iso in VirtualBox.
    <!-- end list -->
      - If you are not familiar with the process, watch the videos,
      - Part 1: <http://www.youtube.com/watch?v=Ffi6cPQCZAE>
      - Part 2: <http://www.youtube.com/watch?v=RYtI3ybng3Q>
      - Part 3: <http://www.youtube.com/watch?v=sxgm0LpTyfQ>
      - Part 4: <http://www.youtube.com/watch?v=NJ5N1GUUpBs>
      - Part 5: <http://www.youtube.com/watch?v=XYpxLnzMjEY>
5.  Notes
      - Suggested configurations of VirtualBox:
        1.  \>= 512MB memory
        2.  \>= 5GB Discspace
      - When you firstly login in Ubuntu, one window will pop up to ask
        for upgrade. **Do Not** upgrade.
6.  Be familiar with Ubuntu in VirtualBox. (It might be very slow)
      - Try commands like: pwd, ls, cd, uname, etc.

## **Get DynaMIT Source Code**

DynaMIT source code now resides in two git servers.

1.  (Deprecated) Internal git server.
      - If you are a developer, you can download the source code from
        Git Server (password required):
          - ` git clone
             `<ssh://USERNAME@137.132.22.82:15011/home/git/repositories/dynamit>
      - If you are not a developer, you have to send email to the
        DynaMIT Project.
2.  Github
      - Run below command to obtain the source code:
          - `git clone https://github.com/smart-fm/dynamit.git
            REPO_NAME`
      - You need to enter the Github account with the password as it
        prompts. You account must also have read permission to DynaMIT
        project under smart-fm organisation.

## **Compile DynaMIT Source Code**

**(You can click here to [Videos](Videos "wikilink") watch the video)**

1.  Open a terminal (We will do everything below in the terminal)
2.  Go to \~/CorbaFreeDynaMIT, command "ls -l", be familiar with the
    folders.
3.  read README.txt.
4.  Installing Third-Party Libraries
      - You will need the following libraries to compile DynaMIT:
        1.  gcc/g++ (4.\*) \[should be already available\], but if not,
            use command: **sudo apt-get install gcc**, **sudo apt-get
            install g++**
        2.  make \[should be already available\], but if not, use
            command: **sudo apt-get install make**
        3.  bison++: Version 1.21-8 or above. use command: **sudo
            apt-get install bison++** (the command should install both
            bison++ and flex)
5.  Compile DynaMIT
      - ./M3O3 clean
      - ./M3O3
      - It will cost around 5 minutes. And there will be some warnings
        (because: some codes are not used). Do not wary. WAIT\!
6.  If there is no Error, then you have succeed to compile DynaMIT.
7.  Go to \~/CorbaFreeDynaMIT/DynaMIT, you will find DynaMIT
    (DynaMIT-R);
8.  Congratulations\!\!\!, you have done a wonderful thing. (About 6
    months ago, we need 1-2 days to compile DynaMIT)

## **Import DynaMIT to Eclipse IDE**

If you are an Eclipse fan, I guess you perfer to edit and compile the
source code using Eclipse IDE. This section introduce you how to do
this.

  - Install Eclipse and C/C++ plugin.
      - You can download "Eclipse IDE for C/C++ Developers" from
        <http://www.eclipse.org/downloads/>
      - If you succeed to install Eclipse IDE, you should be able to see
        C/C++ in Windows -\> Open Perspective
  - Import DynaMIT Source Code in Eclipse
      - In the Git folder, there is a sub-folder named "SourceCode". It
        is the code you need to import.
      - Start Eclipse and switch to the C/C++ Perspective. (Note: I am
        using Eclipse 3.8 for a demo)
      - Click: File -\> Import -\> C/C++ -\> Exsiting Code As Makefile
        Project.
      - Give a Name "DynaMIT_Project" and Find the code path in your
        computer, and then click Finish.
      - Then, you can see a new project imported.
  - Compile DynaMIT in Eclipse
      - You should use the DynaMIT Make file to compile.
      - Right click the Project -\> Properties -\> C/C++ Build
      - Disable the default "use default build command"
      - Import the build comamnd in the source code foler, such as: M3O3
        or M3O3_NO_DEBUG
      - Click Apply and OK
      - Now, you should be able to compile the source code in Eclipse
        IDE.

## **Configure MCR for DynaMIT**

The only thing you need to do is "Copy MCR folder to your $HOME folder"

**Note: This below section is optional (only if you have problems when
using MCR).**

You need to add in some symbolic links to make MCR work. Please do the
following steps:

1.  Open the terminal
2.  Go to folder /MCR/v72/bin/glnx86$
3.  Create following symbolic links:
      - ln -s libicui18n.so.24.0 libicui18n.so
      - ln -s libicui18n.so.24.0 libicui18n.so.24
      - ln -s libicuuc.so.24.0 libicuuc.so
      - ln -s libicuuc.so.24.0 libicuuc.so.24
      - ln -s libustdio.so.24.0 libustdio.so
      - ln -s libustdio.so.24.0 libustdio.so.24
      - ln -s libxerces-c.so.21.0 libxerces-c.so.21

<!-- end list -->

1.  Go to folder MCR/v72/sys/os/glnx86
2.  Create following symbolic links:
      - ln -s libg2c.so.0.0.0 libg2c.so.0
      - ln -s libstdc++.so.5.0.3 libstdc++.so.5

## **Demo DynaMIT-R**

1\. Download marina_demo.tar.gz from \[link removed\] and extract it
\[Please send email to Melani to get the demo\].

2\. We assume you already have a DynaMIT executable from compiling
DynaMIT (check \~/CorbaFreeDynaMIT/DynaMIT/)

3\. Copy the DynaMIT executable from \~/CorbaFreeDynaMIT/DynaMIT/ and
paste in marina_demo/bin/

4\. Run the following command (while you are in the path marina_demo/)
to clear files generated by previous runs of DynaMIT

`  ./backupToDir`

Note: For subsequent runs of DynaMIT, this command will leave
__pathTopoly.dat, which you will have to remove if you modified the
network, origins or destinations

5\. Then run DynaMIT with the inputs using the following command:

`  ./bin/DynaMIT dtaparam.dat`

6\. On another terminal type the following command (while you are in the
path marina_bay/jRNE/) to view the output

`  java –Xmx1024m –jar jRNE.jar`

7\. This is open the visualizer. You can select Window-\>Bottom Panel

8\. From the Bottom Panel, select Load. This will open up a dialog box,
from which you can choose xdtaBinary.ini

9\. Once the network is displayed on the visualizer, select Run

10\. If everything's in order you should see DynaMIT running on the
network with the rolling horizon\!

## **DynaMIT-MPI**

**Follow this section, only if you want to run DynaMIT in parallel.**

1\. Compile DynaMIT-MPI

  - Use M3O3P to compile the source code, like: ./M3O3P. The file will
    automatically load in libs for MPI and compile the source code
    related with MPI.
  - You might have a problem about libmetis. If so, please download
    metis-4.0.3.tar.gz from
    <http://glaros.dtc.umn.edu/gkhome/fsroot/sw/metis/OLD> and compile
    it locally.

2\. Test Open-MPI

3\. Test DynaMIT-MPI