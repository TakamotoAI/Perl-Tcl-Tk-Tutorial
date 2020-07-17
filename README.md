# Perl-Tcl-Tk-Tutorial
## Deploy Perl + Tcl/Tk applications on Windows and macOS

This repository collects code snippets and tutorials from my experience with Perl and Tcl/Tk (not to be confused with Perl/Tk) on how to create a Perl+Tcl/Tk application and deploy it on Windows and macOS. I use the wrapper module [Tcl::pTk](https://metacpan.org/release/Tcl-pTk).

Let's start with some advantages/disadvantages of Perl + Tcl/Tk over Perl/Tk.

Advantages of Tcl/Tk

- It runs on Windows, macOS, and Linux and it looks modern (native)
- It is actively mantained (https://core.tcl-lang.org/tk/reportlist). For example Tk was recently adapted for macOS Mojave/Catalina.
- It is the basic GUI toolkit of Python, so it has a large number of users

Disadvantages of Tcl/Tk

- Binding for Perl (Tcl::pTk) seems not to be used very much, so not a big community to help (but responsibe module mantainer!)
- As a consequence of the previous point, not many info around
- You need to install Tcl/Tk separately (different to Perl/Tk which is just a normal Perl module), and learn how to deploy it in an application if you are gonna to distribute it

## Installation
### Windows
- Install [Strawberryperl](http://strawberryperl.com/). Since all modern Windows PC are 64, I would target the 64bit version if no other requirements must be met.
- Install the latest binary Tcl/Tk distribution, for example [BAWT](http://www.bawt.tcl3d.org/). This will install Tcl/Tk in C:
- Install the Perl module Tcl (needed by Tcl::pTk to communicate with the Tcl/Tk installation): I do `cpanm Tcl`
- Install the Perl module Tcl::pTK: I do `cpanm Tcl::pTk`

To test that everything works fine, simply start the Demo widget. Open a terminal and digit `widgetTclpTk`. 
![demo Widgets](screenshots/demoWIN.png?raw=true "demo Widgets")
