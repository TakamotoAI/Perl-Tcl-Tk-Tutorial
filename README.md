# Perl-Tcl-Tk-Tutorial
Deploy Perl + Tcl/Tk applications on Windows and macOS

This repository collects code snippets and tutorials from my experience with Perl and Tcl/Tk (not to be confused with Perl/Tk) on how to create a Perl+Tcl/Tk application and deploy it on Windows and macOS. 

Let's start with some advantages/disadvantages of Perl + Tcl/Tk over Perl/Tk.

Advantages of Tcl/Tk

- It runs on Windows, macOS, and Linux and it looks modern (native)
- It is actively mantained (look [here] (https://core.tcl-lang.org/tk/reportlist). For example Tk was recently adapted for macOS Mojave/Catalina.
- It is the basic GUI toolkit of Python, so it has a large number of users

Disadvantages of Tcl/Tk

- Binding for Perl (Tcl::pTk) seems not to be used very much, so not a big community to help (but responsibe module mantainer!)
- As a consequence of the previous point, not many info around
- You need to install Tcl/Tk separately (different to Perl/Tk which is just a normal Perl module), and learn how to deploy it in an application if you are gonna to distribute it
