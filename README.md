Simple Console Display Manager
==============================

This simpler version of CDM:
   * can use a common .xinitrc script to start the X programs.
   * supports a default selection and with timeout.
   * doesn't depend on dialog/ncurses.
   * doesn't clear the screen.

Invocation
----------

To run cdm, use

    $ cdm [RCFILE]

cdm tries to source configuration files in this order, and uses the first
existing one:

    [RCFILE specified on command line]
    $HOME/.cdmrc
    /etc/cdmrc

To autostart cdm when you log in your account, copy the content of
/usr/share/cdm/cdm-profile.sh to the tail of your shell profile (~/.profile,
~/.bashrc, etc.):

    # To avoid potential situation where cdm(1) crashes on every TTY, here we
    # default to execute cdm(1) on tty1 only, and leave other TTYs untouched.
    if [[ "$(tty)" == '/dev/tty1' ]]; then
        [[ -n "$CDM_SPAWN" ]] && return
        # Avoid executing cdm(1) when X11 has already been started.
        [[ -z "$DISPLAY$SSH_TTY$(pgrep xinit)" ]] && cdm
    fi

Customisation
-------------

See /etc/cdmrc for examples.


Copying
-------

CDM-simple Copyright (C) 2013, J Honorio Casado Fdez <jhcasado@cuantobit.com>    
CDM  Copyright (C) 2009-2012, Daniel J Griffiths <dgriffiths@ghost1227.com>

Thanks to:

    Andrwe          beta-testing and submitting the fix for the all
                    important X incrementation function
    brisbin33       code cleanup
    tigrmesh        finding a critical issue with the gnome-session handler
    Profjim         several incredibly useful patches
    lambchops468    consolekit and hibernation patches
    CasperVector    Massive rearchitecturing and code sanitation

Licensed under GPLv2+

