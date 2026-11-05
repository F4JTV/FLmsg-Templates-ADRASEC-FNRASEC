ADRASEC - FLmsg custom forms (v1.1.0)
=====================================

Generic forms for every ADRASEC, whatever the department, so that messages
can be exchanged between departments.

Files
-----
  ADRASEC_Message.html   Message ADRASEC: ambiance, situation, encapsulated
                         message, coded procedure (PAPA/SIERRA/GOLF/ECHO/ALPHA/DELTA)
  ADRASEC_AR.html        AR ADRASEC: acknowledgement of receipt

Installation
------------
Copy both .html files into the FLmsg CUSTOM folder:
  Windows : C:\Users\<user>\NBEMS.files\CUSTOM\
  Linux   : ~/.nbems/CUSTOM/
FLmsg picks them up within a second (Form > Custom menu, or Create in the
simple interface). The sending AND receiving stations both need the files:
only field values are transmitted, the form itself is not.

Interoperability: do not rename the files
-----------------------------------------
Every FLmsg message carries the file name of its form (CUSTOM_FORM,
ADRASEC_Message.html). The receiving station opens the message with the file
of the same name in its own CUSTOM folder. A department that renames the files
can no longer read, or be read by, the other departments.

Adapting the forms to a department
----------------------------------
Nothing needs to change: the sending station is identified by its callsign
(Origine field), and the authorities by the encapsulated-message fields.
To show the department anyway, edit only the visible title, for example:
  <h1>Message ADRASEC        ->   <h1>Message ADRASEC 83
in ADRASEC_Message.html (and likewise in ADRASEC_AR.html if wanted).
Keep the file names and the META MENU_ITEM line unchanged.

Sending a message
-----------------
1. Open the form, fill it in, click "Transmettre a FLmsg".
2. Save the message in FLmsg (.k2s file).
3. Select the mode and press AutoSend: fldigi transmits it.

Acknowledgement of receipt
--------------------------
FLmsg has no reply template. Open the received message (View Form), click
"Preparer l'accuse de reception", then open "AR ADRASEC" (Edit Form):
number, recipient and reference are pre-filled.

Upgrading from the ADRASEC 06 version (1.0.0)
---------------------------------------------
- The forms are now ADRASEC_Message.html and ADRASEC_AR.html, listed as
  "Message ADRASEC" and "AR ADRASEC".
- Messages saved with 1.0.0 refer to ADRASEC06_Message.html and
  ADRASEC06_AR.html: keep those two old files in the CUSTOM folder as long as
  you need to view such messages, then delete them.
- The remembered callsign and message counter start afresh: enter them once.

Notes
-----
- All text is converted to 7-bit ASCII on submit (fldigi modes such as MT63
  or Olivia do not reliably carry accented characters).
- The message number and callsign are remembered by the browser used by
  FLmsg (local storage), as FLmsg provides no sequence number.
