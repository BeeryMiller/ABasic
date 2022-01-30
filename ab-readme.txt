File:       AB-README
Program:    Geneve 9640 Advanced BASIC (ABASIC)
Version:    4.08
Released:   1 February 2022
Ref Manual: Updated January 2022
Contact:    9640News or InsaneMultitasker, at AtariAge.com
=====================================================================

Geneve 9640 Advanced BASIC (ABASIC) is a native MDOS programming environment
that is upwardly compatible with TI Extended BASIC.  It implements new
commands, statements, and functions for graphics, file access, and device
handling.

Some of the features include support for V9938 graphics modes, both REAL(float)
and INTEGER variable support, expanded program, stack, and assembly memory
space, and more.

It is HIGHLY recommended that you review the reference manual. A complete
review and update was completed by @hloberg, to go along with this release.

COMPATIBILITY:
---------------
Although built with compatibility in mind, some programs that rely upon
non-standard access to the keyboard and file IO (such as loaders with
embedded assembly support) or that rely upon ROM/GROM peek/poke/load addresses
may not function as expected. Timing loops may operate too quickly and certain
programs that use reserved keys, such as CTRL-C (BREAK) may require slight
modification (such as adding ON BREAK NEXT).


PREPARATION:
------------
For those already using ABASIC, simply replace the four PROGRAM files with
those from this release.


USAGE:
=======
ABASIC requires a minimum of << XXX K>> to load.  You may specify MORE memory
with runtime options, as described in the ABASIC reference manual.

Earlier release notes recommend running ABASIC from a batch file. The bug that
prompted this behavior has been corrected.  The user may continue to use
batch files or load ABASIC from the command line.

If you are running a standard system (512K DRAM, 64K SRAM) and do not have
enough memory to load ABASIC, check your AUTOEXEC for the RAMDISK and TIMODE
statements. You may need to reduce their memory usage or, with MDOS 7.30+,
utilize the TIMODE2 option to free 64K. Note: ABASIC does not require TIMODE.


OPEN ISSUES LOG:
----------------
       - CALL DISTANCE and CALL COINC may return incorrect values. Requires
         further testing of bug report program by Jim Uzzell.
       - Memory constraints within the ABASIC interpreter; <256 bytes free
         across the entire application.
       - "RETURN ELSE RETURN" may cause spurious error messages by interpreter
       - SUBprograms called by another SUBprogram may not be found by the
         interpreter. Appears to be a presecan issue; recommend not nesting
         subprograms where feasible. Referencing them at the start of the
         program (as one does to turn off prescan) may be a temporary fix.
       - ON ERROR within subprograms requires a RETURN to a line within the
         subprogram, prior to SUBEXIT/SUBEND.
       - Coding errors such as using NEXT/FOR with IF/THEN may generate
         unrelated line number errors during program initialization.


ENHANCEMENT LOG:
---------------
V4.08  1 February 2022
       - Updated reference manual, very nice work by @hloberg!
       - Corrected RUN command to execute from within a program, without
         requiring the optional line number
       - Corrected RUN command, able to load programs from the current
         working directory e.g., RUN "FILE" and with MDOS device
         identification e.g., RUN "H:\GAMES\LOADER" in immediate and
         program modes.
       - CTRL-C now works when a program is loaded and auto-started
       - CTRL-C artifact is no longer printed when key is pressed
       - RANDOMIZE now generates different sequences at startup, when no
         seed is specified. System clock is used to set RAND16. A big
         thank you to Lee Stewart for reviewing the ABASIC random code!
       - Noted issues and potential gotchas based on testing

V4.07  2021?????  9640News
       - Corrected time/date functions TIME$/DATE$; reverted to 2-digit
         year and fixed time output.
       - Consolidated ABASIC reference manual using the page updates from
         Jim Uzzel.  Published code on git/9640News website

V4.05  24 November 2013  TT
     - Fixed long-standing STRREF/STRASG/NUMREF/NUMASG bug.  Parameters passed
       to these routines resulted in a BAD VALUE error.  The bug was located in
       166\ASM2000N, just before label CALARE
           Fix:  change "MOV @SAVER0,R0" to "MOV @SAVER0-ASOF,R0"


Ver    06 August 1999 by DDI Software
-------------------------------------
4.04 - Fixed a bug created by INPUT fix in Ver 4.03 where a quoted string
       is used with input.

4.03 - Fix INPUT to properly store input where data crosses a page boundary.

       As a result of this fix the following changes were made to page 257
       of manual(for those with version 4.02 and prior).

       Memory block >F000->FFFF

       >FE30->FFDF was change to;
            >FE30->FF2F  Reserved for ABASIC
            >FF30->FFDF  Unused block of memory

       DATE$ now returns the full year i.e. PRINT DATE$ returns XX-XX-XXXX
       Call Date was not changed and is used as described in manual.
           (NOTE: Returned to 2-digit year in v4.08)

4.02 - Fixed a bug in the print to printer.(that I created)
     - Call files now reports full year.(not a bug)


4.01 - Activated ON KEY(#) to accept 15 keys. Version 3.0 locked out all above
       10.

     - Change KEY STOP to clear ON MOUSE GOSUB line numbers. There is no mouse
       key off.

     - KEY STOP clears ALL gosubs(both ON KEY and ON MOUSE). Both MUST be
       reactivated to use.


4.0  - Catalog of harddrive (via FILES)

     - ACCEPT AT w/negative size in a window, where window row is greater than 1

     - RESequence where a branch(then xxxx,goto xxxx,etc.) after a HEX$
       statement. Would not change line number.

     - CALL HCHAR/VCHAR repetitions to allow a numeric-variable to be a zero.
       The effect is it does nothing. i.e. CALL HCHAR(x,y,65,r) r=0.

     - PSET command/statement.

     - NEW command would not allow creating a new program after a protected
       program had been in memory. Old would clear protection, but not new.

     - SWAP to retain a required space between swap and first variable.

     - MOUSE ON use can now exist with an assembly program in memory.

  COMMANDS DELETED

     - Call key mode 6 (See pg 97 of manual)

     - DEFvartype   single and double precision and CDBL, CSNG

     - CALL CHARSET(x,y)

       jim uzzell,  MYBASIC 4.0  DDI SOFTWARE   UPDATED 8-06-99

** End of file 29-Jan-2022, TT
