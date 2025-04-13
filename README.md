# CBT749
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. GitHub repos will be deleted and created during this period...

```
//***FILE 749 is from Gilbert Saint-flour and contains programs     *   FILE 749
//*           from his large collection of utilities on File 183,   *   FILE 749
//*           which were reworked to be assembled with IFOX00 and   *   FILE 749
//*           run under MVS 3.8 under Hercules.                     *   FILE 749
//*                                                                 *   FILE 749
//*           Unfortunately, Gilbert has passed on.  His software   *   FILE 749
//*           support is being continued by Carlos Aguilera and     *   FILE 749
//*           Sam Golob.                                            *   FILE 749
//*                                                                 *   FILE 749
//*           email:  carlos@gsf-soft.com                           *   FILE 749
//*           email:  sbgolob@cbttape.org                           *   FILE 749
//*                                                                 *   FILE 749
//*                .----------------------------.                   *   FILE 749
//*                |      CBT Tape File 183     |                   *   FILE 749
//*                |  Index of OSVS238J Member  |                   *   FILE 749
//*                '----------------------------'                   *   FILE 749
//*                                                                 *   FILE 749
//*           Gilbert's web site is being supported by Carlos       *   FILE 749
//*           Aguilera:                                             *   FILE 749
//*                                                                 *   FILE 749
//*                 http://gsf-soft.com/Freeware                    *   FILE 749
//*                                                                 *   FILE 749
//*                         COPYRIGHT                               *   FILE 749
//*                                                                 *   FILE 749
//*     These programs are Freeware and may be freely copied.       *   FILE 749
//*     They may be freely distributed to any other party on        *   FILE 749
//*     condition that no inducement beyond reasonable handling     *   FILE 749
//*     costs is offered or accepted by either side for such        *   FILE 749
//*     distribution.                                               *   FILE 749
//*                                                                 *   FILE 749
//*                         DISCLAIMER                              *   FILE 749
//*                                                                 *   FILE 749
//*     Gilbert Saint-Flour neither expresses nor implies any       *   FILE 749
//*     warranty as to the fitness of these computer programs for   *   FILE 749
//*     any function.  The use of these programs or the results     *   FILE 749
//*     therefrom is entirely at the risk of the user.              *   FILE 749
//*     Consequently, the user may modify these programs in any     *   FILE 749
//*     way he/she thinks fit.                                      *   FILE 749
//*                                                                 *   FILE 749
//*                     CONTACT INFORMATION                         *   FILE 749
//*                                                                 *   FILE 749
//*     We would be interested to hear of comments                  *   FILE 749
//*     and/or proposed enhancements.  Please e-Mail to:            *   FILE 749
//*                                                                 *   FILE 749
//*              Carlos Aguilera <carlos@gsf-soft.com>              *   FILE 749
//*                                                                 *   FILE 749
//*     or visit the web site at http://gsf-soft.com/Freeware       *   FILE 749
//*                                                                 *   FILE 749
//*                                                                 *   FILE 749
//*  ----------------- TSO and ISPF commands -------------------    *   FILE 749
//*                                                                 *   FILE 749
//*  CLS       A 5-line "clear screen" command for TSO              *   FILE 749
//*                                                                 *   FILE 749
//*  EXECPGM   TSO command - invoke a utility program or compiler   *   FILE 749
//*            with an alternate ddname list, as follows:           *   FILE 749
//*               EXECPGM IEV90           +                         *   FILE 749
//*                 PARM(NOOBJECT,NODECK,NOXREF,NORLD) +            *   FILE 749
//*                 SYSIN(TEMPWK2)        +                         *   FILE 749
//*                 SYSUT1(TEMPWK1)       +                         *   FILE 749
//*                 SYSLIB(ASMLIB)        +                         *   FILE 749
//*                 SYSPRINT(ASMH$PRT)    +                         *   FILE 749
//*                 STEPLIB(LINKLIST)                               *   FILE 749
//*                                                                 *   FILE 749
//*  INITKSDS  Initialize a KSDS after it's been DEFINE'd           *   FILE 749
//*                                                                 *   FILE 749
//*            This program prevents OPEN from failing when         *   FILE 749
//*            opening with MACRF=(IN,OUT) or STRNO=2 a KSDS        *   FILE 749
//*            that has just been defined.  Can be invoked as       *   FILE 749
//*            a batch program, a TSO command, or a sub-routine.    *   FILE 749
//*                                                                 *   FILE 749
//*  ------------------ Batch Programs --------------------------   *   FILE 749
//*                                                                 *   FILE 749
//*  BLKSIZE2  Scan a PDS and print the size of each block and      *   FILE 749
//*            the track balance                                    *   FILE 749
//*                                                                 *   FILE 749
//*            This is a batch program, for people interested       *   FILE 749
//*            in what a PDS looks like, from the inside.           *   FILE 749
//*                                                                 *   FILE 749
//*  BYPASSNQ  Assembler program.  Scratch or Rename a Data Set     *   FILE 749
//*            without SYSDSN ENQ                                   *   FILE 749
//*                                                                 *   FILE 749
//*            BYPASSNQ is a driver that allows you to run any      *   FILE 749
//*            utility program (such as IEHPROGM or IDCAMS) and     *   FILE 749
//*            bypass dsname ENQ that is normally performed by      *   FILE 749
//*            the DYNALLOC, SCRATCH and RENAME SVCs.               *   FILE 749
//*                                                                 *   FILE 749
//*  CANMSGCL  Purge current job's held output after a few hours.   *   FILE 749
//*            Useful for those jobs that work OK 99% of the time   *   FILE 749
//*            (must be authorized)                                 *   FILE 749
//*                                                                 *   FILE 749
//*            Example:                                             *   FILE 749
//*                                                                 *   FILE 749
//*              //MYJOB    JOB ACCT#,CLASS=A,MSGCLASS=X            *   FILE 749
//*              //COPY1   EXEC PGM=IEBCOPY                         *   FILE 749
//*              //...      DD   ...                                *   FILE 749
//*              //CONDPURG EXEC PGM=CANMSGCL,PARM=2,               *   FILE 749
//*              //              COND=(0,NE,COPY1)                  *   FILE 749
//*                                                                 *   FILE 749
//*              The number in the parm is a number of hours.       *   FILE 749
//*              If the 'COPY1' step ends at 10:28 with a           *   FILE 749
//*              return code equal to zero, the 'CONDPURG' step     *   FILE 749
//*              executes and issues the following command:         *   FILE 749
//*                                                                 *   FILE 749
//*                $TA,T=12.28,'$OJ01234,Q=X,CANCEL'                *   FILE 749
//*                                                                 *   FILE 749
//*  CLEANUP   Assembler program.  Automatically searches the MVS   *   FILE 749
//*            catalog for non-GDG data sets that will be created   *   FILE 749
//*            in subsequent steps of your job and deletes them.    *   FILE 749
//*                                                                 *   FILE 749
//*                  //MYJOB   JOB  acct#                           *   FILE 749
//*                  //*                                            *   FILE 749
//*                  //CLEANUP EXEC PGM=CLEANUP                     *   FILE 749
//*                  //*                                            *   FILE 749
//*                  //STEP1   EXEC PGM=MYPROG1                     *   FILE 749
//*                  //OUTDD    DD  DSN=MY.FILE1,DISP=(,CATLG)      *   FILE 749
//*                  //STEP2   EXEC PGM=MYPROG2                     *   FILE 749
//*                  //OUTDD    DD  DSN=MY.FILE2,DISP=(,CATLG)      *   FILE 749
//*                                                                 *   FILE 749
//*            Can also be executed as the LAST step of a job to    *   FILE 749
//*            delete non-GDG data sets that were created during    *   FILE 749
//*            job execution.                                       *   FILE 749
//*                                                                 *   FILE 749
//*  CMDJ      Send a JES2 command with the current job's number    *   FILE 749
//*            (must be authorized)                                 *   FILE 749
//*                                                                 *   FILE 749
//*            Example:                                             *   FILE 749
//*                                                                 *   FILE 749
//*               //PURGEJOB EXEC PGM=CMDJES2,PARM=P                *   FILE 749
//*                                                                 *   FILE 749
//*            If the current job's number is JOB01234,             *   FILE 749
//*            then the following command is issued:                *   FILE 749
//*                                                                 *   FILE 749
//*                  $PJ  01234                                     *   FILE 749
//*                                                                 *   FILE 749
//*  GSFLKED   Front-end to the linkage editor to recover           *   FILE 749
//*            from SD37 on SYSLMOD (must be authorized)            *   FILE 749
//*                                                                 *   FILE 749
//*            This program may be invoked instead of the DFP       *   FILE 749
//*            linkage editor. It calls the linkage editor and,     *   FILE 749
//*            if an SD37 abend occurs, calls IEBCOPY to compress   *   FILE 749
//*            the SYSLMOD PDS, then calls the linkage editor       *   FILE 749
//*            again.                                               *   FILE 749
//*                                                                 *   FILE 749
//*            Another feature of this program is to                *   FILE 749
//*            conditionally append a PDS member to SYSLIN,         *   FILE 749
//*            if that member exists.                               *   FILE 749
//*                                                                 *   FILE 749
//*  JOBRLSE   Release a job by number (must be authorized)         *   FILE 749
//*                                                                 *   FILE 749
//*            This program issues a $A command to release a job    *   FILE 749
//*            previously submitted to JES2 with "TYPRUN=HOLD".     *   FILE 749
//*                                                                 *   FILE 749
//*            To prevent "multiple jobs found" conditions,         *   FILE 749
//*            this program uses the sub-system interface           *   FILE 749
//*            to inquire about the status of homonym jobs.         *   FILE 749
//*            Then, it issues a $A command with the job            *   FILE 749
//*            number of the first job found in the input           *   FILE 749
//*            queue in held status (for example: $A J1234).        *   FILE 749
//*                                                                 *   FILE 749
//*            Sample execution JCL:                                *   FILE 749
//*                                                                 *   FILE 749
//*              //RLSENEXT EXEC PGM=JOBRLSE,PARM=PAYROL22          *   FILE 749
//*                                                                 *   FILE 749
//*  NOTCTLG3  Prolog step to prevent "NOT CATLG 2" and verify      *   FILE 749
//*            VSAM data sets                                       *   FILE 749
//*                                                                 *   FILE 749
//*            This program may be executed at the beginning        *   FILE 749
//*            of a batch job.  It scans the job's SWA to           *   FILE 749
//*            locate JFCBs and does two things:                    *   FILE 749
//*                                                                 *   FILE 749
//*            1. checks if any non-gdg data set with               *   FILE 749
//*               DISP=(NEW,CATLG) is already cataloged.            *   FILE 749
//*               If it finds at least one (i.e. a "NOT             *   FILE 749
//*               CATLG 2" is about to occur), it issues a          *   FILE 749
//*               message and abends the job                        *   FILE 749
//*                                                                 *   FILE 749
//*            2. Checks if any VSAM data set has been left         *   FILE 749
//*               in OPEN status by an abending job.  Every         *   FILE 749
//*               data set in this case is opened and closed.       *   FILE 749
//*               The way this condition is detected is quite       *   FILE 749
//*               interesting, look at the code.                    *   FILE 749
//*                                                                 *   FILE 749
//*  DONTFAIL  Prevent job failure caused by uncataloged data       *   FILE 749
//*            sets (ESA only, must be authorized)                  *   FILE 749
//*                                                                 *   FILE 749
//*            This program has been designed to prevent jobs       *   FILE 749
//*            that accept multiple inputs from failing in the      *   FILE 749
//*            middle of the night because of a "typo" in a data    *   FILE 749
//*            set name.  When DONTFAIL detects that an input       *   FILE 749
//*            data set is not cataloged, it converts it to a       *   FILE 749
//*            null data set and allows the job to run with         *   FILE 749
//*            partial input.                                       *   FILE 749
//*                                                                 *   FILE 749
//*  SYSMOVE   Unload a PDS to a sequential data set in             *   FILE 749
//*            IEHMOVE format.                                      *   FILE 749
//*                                                                 *   FILE 749
//*  UNITAFF   Dynamically sets UNIT=AFF for input tape files       *   FILE 749
//*            (must be authorized)                                 *   FILE 749
//*                                                                 *   FILE 749
//*            This program was originally designed to reduce       *   FILE 749
//*            the number of tape drives used by user-submitted     *   FILE 749
//*            SAS steps.  It scans the SWA for the next step       *   FILE 749
//*            and changes some of the SIOT's fields to force       *   FILE 749
//*            all input tape data sets to the same drive.          *   FILE 749
//*                                                                 *   FILE 749
//*            It must be executed immediately before the           *   FILE 749
//*            step to process (SAS, SORT, or any other             *   FILE 749
//*            program that reads a variable number of tape         *   FILE 749
//*            files, one at a time).                               *   FILE 749
//*                                                                 *   FILE 749
//*            Sample jcl:                                          *   FILE 749
//*                                                                 *   FILE 749
//*              //UNITAFF EXEC PGM=UNITAFF                         *   FILE 749
//*              //STEPLIB  DD  DSN=SYS2.AUTHLIB,DISP=SHR           *   FILE 749
//*              //*                                                *   FILE 749
//*              //STEP53  EXEC PGM=SAS                             *   FILE 749
//*              //OSIN     DD DSN=USER1.X,DISP=SHR                 *   FILE 749
//*              //         DD DSN=UPQE.DQE40530(-1),DISP=SHR       *   FILE 749
//*              //OSIN2    DD DSN=UPQR.DQR02150(0),DISP=SHR        *   FILE 749
//*              //OSIN3    DD DSN=USER1.X,DISP=SHR                 *   FILE 749
//*              //         DD DSN=UPBG.DBGA0240(-1),DISP=SHR       *   FILE 749
//*              //OSIN4    DD DSN=USER1.X,DISP=SHR                 *   FILE 749
//*              //         DD DSN=USER1.YY,DISP=SHR                *   FILE 749
//*              //         DD DSN=UPQR.DQR02140(-1),DISP=SHR       *   FILE 749
//*                                                                 *   FILE 749
//*            The program only supports cataloged data sets;       *   FILE 749
//*            relative generation numbers are handled              *   FILE 749
//*            correctly via the GDGNT.                             *   FILE 749
//*                                                                 *   FILE 749
//*            Restriction: No distinction is made between 3420,    *   FILE 749
//*            3480 or 3490 device types; this will cause           *   FILE 749
//*            problems if the input to a step is mixed.            *   FILE 749
//*                                                                 *   FILE 749
//*                                                                 *   FILE 749
//*  ------------------ Assembler Macros ------------------------   *   FILE 749
//*                                                                 *   FILE 749
//*  BUILDCDE  Make storage allocated with GETMAIN appear as a      *   FILE 749
//*            load-module in a dump.                               *   FILE 749
//*                                                                 *   FILE 749
//*            BUILDCDE uses the "loader" form of IDENTIFY to       *   FILE 749
//*            create a major CDE and corresponding XL, then        *   FILE 749
//*            issues a LOAD SVC to create an LLE and associate     *   FILE 749
//*            the CDE with the current TCB.  Don't worry, you      *   FILE 749
//*            don't have to understand how it works to use it.     *   FILE 749
//*                                                                 *   FILE 749
//*            EXAMPLE:                                             *   FILE 749
//*                                                                 *   FILE 749
//*                  GETMAIN RU,LV=20000                            *   FILE 749
//*                  BUILDCDE LENGTH=(0),ADDR=(1),EP=DYNAM20        *   FILE 749
//*                                                                 *   FILE 749
//*            The 20K storage area will appear in a dump           *   FILE 749
//*            as a load-module called "DYNAM20".                   *   FILE 749
//*                                                                 *   FILE 749
//*  EASYSORT  Invoke an internal SORT with OPEN/PUT/GET logic      *   FILE 749
//*                                                                 *   FILE 749
//*            Allows you to do internal sorts without any          *   FILE 749
//*            knowledge of parameter lists or exit routine         *   FILE 749
//*            linkage conventions.                                 *   FILE 749
//*                                                                 *   FILE 749
//*            Example:                                             *   FILE 749
//*                                                                 *   FILE 749
//*                      EASYSORT OPEN,                             *   FILE 749
//*                            FIELDS=(1,22,CH,A),                  *   FILE 749
//*                            TYPE=F,LENGTH=64,                    *   FILE 749
//*                            OPTION='EQUALS,RESINV=500K'          *   FILE 749
//*                      .     .                                    *   FILE 749
//*              READ    GET   FILEIN                               *   FILE 749
//*                      EASYSORT PUT,(1)   pass record to SORT     *   FILE 749
//*                      B     READ                                 *   FILE 749
//*                      .     .                                    *   FILE 749
//*              REWRITE EASYSORT GET,      get sorted record       *   FILE 749
//*                            SET=(R3),                            *   FILE 749
//*                            EODAD=ENDSORT                        *   FILE 749
//*                      PUT   FILEOUT,(R3)                         *   FILE 749
//*                      B     REWRITE                              *   FILE 749
//*                      .     .                                    *   FILE 749
//*              ENDSORT EASYSORT CLOSE                             *   FILE 749
//*                                                                 *   FILE 749
//*  GETDIR    Read a directory sequentially with a BPAM DCB        *   FILE 749
//*                                                                 *   FILE 749
//*            This macro offers a simple way to read directory     *   FILE 749
//*            entries and members with a single BPAM DCB.          *   FILE 749
//*                                                                 *   FILE 749
//*  STRING    Provides functions similar to PL/I's                 *   FILE 749
//*            PUT EDIT or COBOL's STRING.                          *   FILE 749
//*                                                                 *   FILE 749
//*            This is the only non-IBM macro you need to           *   FILE 749
//*            assemble the programs in this file.                  *   FILE 749
//*                                                                 *   FILE 749
//*            This member contains the macro, a test job,          *   FILE 749
//*            and the documentation.                               *   FILE 749
//*                                                                 *   FILE 749
//*                                                                 *   FILE 749
//*  ---------------------- Miscellaneous -----------------------   *   FILE 749
//*                                                                 *   FILE 749
//*  DEFGDGSR  Sub-routine - invokes SVC 26 to define a GDG base    *   FILE 749
//*                                                                 *   FILE 749
//*            May be invoked from a COBOL program, like this:      *   FILE 749
//*                                                                 *   FILE 749
//*                  05  DSNAME   PIC X(44) VALUE 'MY.DSNAME'.      *   FILE 749
//*                  05  GDGLIMIT PIC   999 VALUE 027.              *   FILE 749
//*                                                                 *   FILE 749
//*                      CALL 'DEFGDGSR' USING DSNAME,              *   FILE 749
//*                                            GDGLIMIT.            *   FILE 749
//*                                                                 *   FILE 749
//*  FILLDASD  Asm pgm to fill free DASD space with binary zeroes   *   FILE 749
//*                                                                 *   FILE 749
//*  HANDBOOK  Job - Creates an on-line copy of the DATA AREAS      *   FILE 749
//*            (aka Debugging Handbook) manuals                     *   FILE 749
//*                                                                 *   FILE 749
//*            This job assembles macros from SYS1.MACLIB and       *   FILE 749
//*            SYS1.AMODGEN and stores the assembly listings        *   FILE 749
//*            into PDS members.  It is set up for over 60          *   FILE 749
//*            commonly used MVS control blocks (such as CVT,       *   FILE 749
//*            TCB, JFCB, etc) and may be easily modified to        *   FILE 749
//*            support other ones.                                  *   FILE 749
//*                                                                 *   FILE 749
//*            The assembly listing for each macro is stored        *   FILE 749
//*            into the output PDS under the control block          *   FILE 749
//*            name.  For example, the assembly listing for         *   FILE 749
//*            "IKJTCB" is stored into the "TCB" member.            *   FILE 749
//*                                                                 *   FILE 749
//*            To conserve dasd space, the LMCOPY service of        *   FILE 749
//*            ISPF/PDF is used to pack the output of the           *   FILE 749
//*            assembler.                                           *   FILE 749
//*                                                                 *   FILE 749
//*  TCTDCTR   Sub-routine - Prints the EXCP count for each DD      *   FILE 749
//*            in the job step                                      *   FILE 749
//*                                                                 *   FILE 749
//*            May be invoked at the end of a program for           *   FILE 749
//*            debugging or tuning purposes.                        *   FILE 749
//*                                                                 *   FILE 749
//*  TRIMMAC   Job - Creates a reduced-size MACLIB that may be      *   FILE 749
//*            used instead of the SYS1.MACLIB/SYS1.AMODGEN         *   FILE 749
//*            concatenation to improve the performance of the      *   FILE 749
//*            assembler.                                           *   FILE 749
//*                                                                 *   FILE 749
//*            The "TRIMMAC" library is built as follows:           *   FILE 749
//*                                                                 *   FILE 749
//*            1. selected macros are read from ddname "SYSLIB",    *   FILE 749
//*               trimmed from PL/AS code and other comment         *   FILE 749
//*               lines, then written to a temporary data set.      *   FILE 749
//*                                                                 *   FILE 749
//*            2. the SORT utility is invoked to sort the macros    *   FILE 749
//*               in ascending sequence of their size.              *   FILE 749
//*                                                                 *   FILE 749
//*            3. the sorted macros are written to SYSPUNCH         *   FILE 749
//*               as an IEBUPDTE sysin stream.                      *   FILE 749
//*                                                                 *   FILE 749
//*            4. IEBUPDTE is executed in the last step to          *   FILE 749
//*               load the macros into the "TRIMMAC" library,       *   FILE 749
//*               the smallest macros being loaded first.           *   FILE 749
//*                                                                 *   FILE 749
//*            You may customize the member list and the input      *   FILE 749
//*            concatenation to add other macros and/or macro       *   FILE 749
//*            libraries, as needed.                                *   FILE 749
//*                                                                 *   FILE 749
//*            Use the "TRIMMAC" library instead of the             *   FILE 749
//*            MACLIB/AMODGEN concatenation to assemble a           *   FILE 749
//*            program and compare the before/after values for      *   FILE 749
//*            the elapsed time, excp count and I/O connect         *   FILE 749
//*            time.  Expect savings of 30 to 60 percent when       *   FILE 749
//*            "TRIMMAC" is used.                                   *   FILE 749
//*                                                                 *   FILE 749
//*            My "TRIMMAC" PDS is currently allocated as           *   FILE 749
//*            follows:                                             *   FILE 749
//*                                                                 *   FILE 749
//*                UNIT=3390,SPACE=(CYL,(9,,18)),                   *   FILE 749
//*                DCB=(RECFM=FB,LRECL=80,BLKSIZE=29720)            *   FILE 749
//*                                                                 *   FILE 749
```
