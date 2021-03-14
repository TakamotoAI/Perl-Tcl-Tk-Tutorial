# Perl-Tcl-Tk-Tutorial
## Deploy Perl + Tcl/Tk applications on Windows and macOS

This repository collects code snippets and tutorials from my experience with Perl and Tcl/Tk (not to be confused with Perl/Tk) on how to create a Perl+Tcl/Tk application and deploy it on Windows and macOS. I use the wrapper module [Tcl::pTk](https://metacpan.org/release/Tcl-pTk).

Let's start with some advantages/disadvantages of Perl + Tcl/Tk over Perl/Tk.

Advantages of Tcl/Tk

- It runs on Windows, macOS, and Linux and it looks modern (native)
- It is actively mantained (https://core.tcl-lang.org/tk/reportlist). For example Tk was recently adapted for macOS Mojave/Catalina.
- It is the basic GUI toolkit of Python, so it has a large number of users
- Similar/Same syntax as Perl/Tk

Disadvantages of Tcl/Tk

- Binding for Perl (Tcl::pTk) seems not to be used very much, so not a big community to help (but very responsive module mantainer!)
- As a consequence of the previous point, not many info around
- You need to install Tcl/Tk separately (different to Perl/Tk which is just a normal Perl module), and learn how to deploy it in an application if you are gonna to distribute it

In a nutshell, the GUI application will be packed in an executable using [pp](https://metacpan.org/pod/pp) and will be distributed/shipped togheter with the Tcl/Tk binary. In developement we mimick the structure of the final App. For developement th structure of our App will be the same for Windows and macOS. The deployment will require a slighlty adaptation of the folder structure.

## Installation
### Windows
- Install [Strawberryperl](http://strawberryperl.com/). Since all modern Windows PC are 64, I would target the 64bit version if no other requirements must be met.
- Install the latest binary Tcl/Tk distribution, for example [BAWT](http://www.bawt.tcl3d.org/). This will install Tcl/Tk in C:
- Install the Perl module Tcl (needed by Tcl::pTk to communicate with the Tcl/Tk installation): I use `cpanm Tcl`
- Install the Perl module [Tcl::pTk](https://metacpan.org/release/Tcl-pTk): I use `cpanm Tcl::pTk`
- Install the Perl module [pp](https://metacpan.org/pod/pp) in order to create an executable of your Perl program: I use `cpanm pp`

### macOS
- Install a recent version of Perl. I use: [Perlbrew](http://www.perlbrew.pl)
- Tcl/Tk (obsolete version) is already installed on most macOS. For the purpose of the next steps, this old version will suffice
- Install the Perl module Tcl (needed by Tcl::pTk to communicate with the Tcl/Tk installation): I use `cpanm Tcl`
- Install the Perl module [Tcl::pTk](https://metacpan.org/release/Tcl-pTk): I use `cpanm Tcl::pTk`
- Install the Perl module [pp](https://metacpan.org/pod/pp) in order to create an executable of your Perl program: I use `cpanm pp`

### Explore Tcl/Tk from Perl
To test that Perl can use the installed version of Tcl/Tk, simply start the Demo widget. Open a terminal and digit `widgetTclpTk`. If a demo widget is shown, Perl is now using Tk of the Tcl/Tk installation. 

## Developement
### Organizing the App structure
Create a folder structure as described below (since my application targets both Windows and macOS, I have a single folder for both OS):
1. Main APP folder called 'MyApp':
   - MyApp.pl + modules
   - a folder called 'Files' containing images, configuration files, etc
   - a folder called 'TclTk' containing the bare bone Tcl/Tk binary for Windows
   - a folder called 'Frameworks' containing the Tcl/Tk Frameworks for macOS

### Download/Compile a Tcl/Tk installation to integrate and ship with the APP
For deployment we need a 'portable' Tcl/Tk installation (since we want to ship it with our APP) and tell Perl, i.e. the Tcl module, to use it instead of the installed version (which is normally not present on the user's machine). I use a bare bone Tcl/Tk binary. 

#### Windows
Since I am NOT able to compile Tcl/Tk from source on Windows, I take a pre-compiled binary, for example from [Ashok](https://sourceforge.net/projects/magicsplat/files/barebones-tcl/). Download it, rename the containing folder 'TclTk' and put it in the APP structure indicated above

#### macOS
Compilation of the Tcl/Tk Frameworks is super easy on macOS. Download the [Tcl/Tk Sources](https://www.tcl.tk/software/tcltk/download.html). In Terminal:
`````
export ver="8.6.10"
make -C tcl8.6.10/macosx embedded CFLAGS_OPTIMIZE="-O2 -mmacosx-version-min=10.11"
make -C tk8.6.10/macosx embedded CFLAGS_OPTIMIZE="-O2 -mmacosx-version-min=10.11"
`````

(Detailed information are available in the README file of macOS directory of distribution)
This will generate a `Tcl.framework` and a `Tk.framework`. Put them in a folder 'Frameworks' inside our APP structure indicated above.

### Linking the Application to the desired (portable) Tcl/Tk installation
In order to link the Perl MyApp.pl script (and later our exe) to the Tcl/Tk binaries in our App structure, we need to tell Perl to do this. When the Perl script/executable is run, Tcl.pm will link to the Tcl/Tk that has been used during installation. Since we want to deploy the APP on other machines, in a self-contained environment (i.e. shipping the Tcl/Tk binaries togheter with our APP), we need to explicitely tell our script, i.e. our executable where to search for Tcl/Tk. A `BEGIN` block will take care to link our application to the desired (shipped) Tcl/Tk binary. My `BEGING`block is probably not the best way to achieve this, but it works. Unfortunately no explanation is to be found in the Tcl.pm module or on the Web. See script `linkApp2TclTk.pl`. The `BEGIN` block takes care of the OS and of the APP file organisation on Windows and macOS. It will be used also to run all examples of this tutorial. If the block is omitted, the Tcl.pm module will link to the Tcl/Tk binary seen at installation time. I use this Tcl/Tk biniaries also in developement to be sure to develop the application with the same Tcl/Tk binaries that will be shipped with the APP.





