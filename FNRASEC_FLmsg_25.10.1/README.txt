FNRASEC - FLmsg custom forms (based on FNRASEC Winlink templates 25.10.1)
=========================================================================

Port to FLmsg / fldigi of the FNRASEC Winlink templates, release 25.10.1:
  https://github.com/jlzola/fnrasec-winlink-template
Original templates: F4IXH Jean-Louis Zola, F1COB Jean-Michel Brocal.
MIT License, see LICENSE.txt.

Files
-----
  FNRASEC_MessageExercice.html       FNRASEC Message Exercice
  FNRASEC_MessageCommandement.html   FNRASEC Message de commandement
  FNRASEC_BilanSituation.html        FNRASEC Bilan de situation
  FNRASEC_ArretePrefectoral.html     FNRASEC Arrete prefectoral
  FNRASEC_EtatReseaux.html           FNRASEC Etat des reseaux
  FNRASEC_AR.html                    FNRASEC Accuse de reception

Installation
------------
Copy the .html files, without renaming them, into the FLmsg CUSTOM folder:
  Windows : C:\Users\<user>\NBEMS.files\CUSTOM\
  Linux   : ~/.nbems/CUSTOM/
FLmsg picks them up within a second (Form > Custom menu, or Create in the
simple interface). The sending AND receiving stations both need the files:
only field values are transmitted, the form itself is not.

Sending a message
-----------------
1. Open the form, fill it in, click "Transmettre a FLmsg".
2. Save the message in FLmsg (.k2s file).
3. Select the mode and press AutoSend: fldigi transmits it.

Acknowledgement of receipt
--------------------------
FLmsg has no reply template. Open the received message (View Form), click
"Preparer l'accuse de reception", then open "FNRASEC Accuse de reception"
(Edit Form): number, recipient, authorities and subject are pre-filled.

Differences from the Winlink templates
--------------------------------------
- One HTML file per form, used by FLmsg for both editing and viewing.
- No {SeqNum} / {Callsign} in FLmsg: the sequence number (shared by all
  FNRASEC forms), the origin, the station and operator callsigns are
  remembered by the browser used by FLmsg.
- The Winlink "DateTime" field is named "vDateHeure": FLmsg upper-cases
  any attribute equal to "DateTime" and would break it.
- All text is converted to 7-bit ASCII on submit (the Winlink templates only
  removed accents from capitals); event values are sent without accents.
- "Etat des reseaux": the empty event choice now blocks sending, as intended
  by the "required" attribute (its value was " -  " upstream).
- Logos are embedded at reduced size to keep each file self-contained.
