Welcome to the SAVELAB Package - see the Overview below for more
information on SAVELAB.

Note: If you downloaded from github then ignore the $RECV but you
      should look at using zigi (https://zigi.rocks) for the clone
      and installation.

This dataset contains the following members (which have meaningful ISPF
stat userids):

   $README  - what you are reading
   $README2 - migration information from a pre-2.0 release
   $RECV ** - exec to run to expand the xmit members
   $WHY     - brief why use ISPF Edit Labels
   @MSG     - TSO Transmit message text
   EXEC *   - TSO Transmit (XMIT) REXX library
   EXPORT * - SAVELAB export of the Savelab labels
   PANELS * - TSO Transmit (XMIT) ISPF Panels Library
   * these members do not exist in the git repository version
   ** this is not required with the git repository version

### Installation Options

There are two options for the installation.

1. Clone the repository using ZIGI
2. If using Git only use the zginstall.rex (see zginstall.readme for
   instructions)
3. If you have the SAVELAB.XMIT or have CBT File 313 member SAVELAB
   - Issue RECEIVE INDS(savelab.xmit or cbt.file313.pds(savelab))
   - Execute member $RECV in the savelab.pds to recreate the savelab
     libraries

Then:

1. Copy the `savelab.exec` members into your SYSEXEC, or SYSPROC, library.
2. Copy the `savelab.panels` members into your ISPF Panels library that is
   allocated to ISPPLIB.

After installing SAVELAB to experiment Edit the SAVELAB exec and use the
command SAVELAB IMP savelab.export to restore the Edit Labels for it
(where dsn is the restored dataset name for the EXPORT dataset).

## Overview

   Name:      SAVELAB

   Type:      ISPF Edit Command (Macro)

  Function:    Save, Restore, or List Labels for an ISPF Edit
               member.

               Or List all existing labels in the data.
               - thanks to Alex B.

               This is accomplished by saving the label and
               associated line numbers in a row in an ISPF
               Table that is stored in the user ISPPROF PDS.

               When the SAVELAB is called it will define an
               alias to the END/PF3 commands to call the
               SAVELABE exec to save all active labels for
               the current member prior to ending the ISPF
               Edit session.

               Along with SAVELABE an alias for SAVE will be
               defined for SAVELABS so any overt SAVE will
               also save all the active labels.

               During a Restore (SAVELAB with no option) and
               an Import the code checks the number of records
               in the current member with the number of
               records when a SAVELAB Save or EXport were
               performed. If different then a warning message
               is generated as the labels may not be restored
               to the correct record locations.

  Syntax:      %SAVELAB option

               option may be:
               blank    - restore saved labels (default)
                          of this member
               EXPORT   - export the label set to a pds
               HELP     - show help info (alias is ?)
               IMAC     - Like Quiet but if not saved labels
                          will not enable automatic saving
                          ** Ideal use in an Initial Macro
               IMPORT   - import the label set from a pds
               LIST     - Selection list of active labels
               QUIET    - do not report if no labels avail
               SAVE     - save all labels
               SHOW     - alias of LIST
               SHOW ALL - display the ISPF table
                        - includes the ability to Use another
                          dataset(mem) labels in the current member

               Abbreviations:
               E        - Export dsn
               H        - Help
               I        - Import dsn
               IM       - IMAC
               L        - List active labels selection table
               Q        - Quiet
               S        - Save
               SH       - SHOW
               SH A     - SHOW ALL

  Processing:
               The labels for a dataset(member) are saved in
               a row in the SAVELAB Table in the ISPPROF PDS.
               Each dataset(member) is added to this table
               in its own row variables.

               Use SHOW ALL to view a table list of all saved
               entries in the ISPF Table.

               Export and Import require a PDS data set name
               be provided. The member used will be the
               member name of the active member.

               If the PDS does not exist it will be allocated.

               An Export will force a SAVELAB Save before
               doing an export.

  Notes:    1. If the ISPF Session abnormally terminates the
               updates may not be saved in the table.
            2. This code may be installed using a different
               name if SAVELAB is too long (e.g. SL)
               - if you do that then you MUST rename the
                 SAVELABE code which calls SAVELAB.
               ** When SAVELAB is used the 1st time to restore
                 it defines an alias of SL for SAVELAB
            3. All members/labels info is saved in a table
               in the users ISPF Profile dataset.
            4. The same member in different data sets MAY be
               processed with No Conflicts.
            5. Using the ISPF Compare, and some other tools,
               can insert additional labels that you may not
               want to save - just beware.

## Bonus

Included with SAVELAB are two additional Edit commands (macro) designed
specifically for use with REXX source code and COBOL source code.

That first command is **REXXLAB** which will create ISPF Edit Labels for
every sub-routine name within the REXX code. Existing labels are
retained and new labels created - then SAVELAB LIst is invoked.

Routine labels are for routines that start with text and end with a :

The label will be the 1st letter of each part of the routine or the 1st
5 chars of routine name.

If the label is 5 characters, or less, then it will be used as is.

If the label with _ removed and combined is 5 characters, or less, then
it will be used.

    Examples:
        DoIt:        ->    .doit
        Do_It:       ->    .doit
        Do_It12:     ->    .doit
        Do_Another:  ->    .doano
        DoSomething: ->    .dosom

Routine labels with numbers or special chars will be have them
translated to blanks.

Existing labels will be unchanged.

Duplicate labels will have a suffix of A, B, ... appended if possible.
* if label is 5 chars then last removed and the suffix appended.

The second is **COBLAB** which does the same as **REXXLAB** but with
COBOL source code.
