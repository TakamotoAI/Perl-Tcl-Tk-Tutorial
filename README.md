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

## Installation
### Windows
- Install [Strawberryperl](http://strawberryperl.com/). Since all modern Windows PC are 64, I would target the 64bit version if no other requirements must be met.
- Install the latest binary Tcl/Tk distribution, for example [BAWT](http://www.bawt.tcl3d.org/). This will install Tcl/Tk in C:
- Install the Perl module Tcl (needed by Tcl::pTk to communicate with the Tcl/Tk installation): I use `cpanm Tcl`
- Install the Perl module Tcl::pTK: I use `cpanm Tcl::pTk`
- Install the Perl module [pp] (https://metacpan.org/pod/pp) in order to create an executable of your Perl program: I use `cpanm pp`

To test that Perl can use Tcl/Tk, simply start the Demo widget. Open a terminal and digit `widgetTclpTk`. If a demo widget is shown, Perl is now using the Tk of the Tcl/Tk installation. For deployment, however, we need 'portable' Tcl/Tk binaries and tell Perl, i.e. the Tcl module, to use it instead of the installed version (which is normally not present on the user's machine). I use a bare bone Tcl/Tk binary. Since I am NOT able to compile Tcl/Tk from source on Windows, I take a pre-compiled binary, for example from [Ashok](https://sourceforge.net/projects/magicsplat/files/barebones-tcl/). 

### macOS
Coming soon...

## Developement
### Organizing the App structure
Create a folder structure as described below (since my application targets both Windows and macOS, I have a single folder for both OS):
1. Main APP folder called 'MyApp':
   - MyApp.pl + modules
   - a folder called 'Files' containing images, configuration files, etc
   - a folder called 'TclTk' containing the bare bone Tcl/Tk binary for Windows
   - a folder called 'Frameworks' containing the Tcl/Tk Frameworks for macOS

### Linking the Application to the desired Tcl/Tk binary
In order to llink pur script (and later our exe) to the Tcl/Tk binaries in our App structure, we need to tell Perl to do this. When the Perl script/executable is run, a `BEGIN` block will take care to link our application to the desired (shipped) Tcl/Tk binary. My `BEGING`block is probably not the best way to achieve this, but it is the only method I found. Unfortunately no explanation is to be found in the Tcl.pm module or on the Web. See script `linkApp2TclTk.pl`. The `BEGIN` blocks takes care of the OS and of the file organisation on Windows and macOS. It will be used also to run all examples of this tutorial. If the block is omitted, the Tcl.pm module will link to the Tcl/Tk binary seen at installation time. I use this Tcl/Tk biniaries also in developement.





