====================
Uni Oldenburg Latex Template für Abschlussarbeiten
====================

Das Template soll eine Vorlage für die Erstellung von Abschlussarbeiten in der Informatik an der Universität Oldenburg darstellen, zum Beispiel bei Bachelor- oder Masterarbeiten. Das Format entspricht grob den Vorgaben der Universität und wurde in dieser Form auch ohne Anmerkungen akzeptiert.

Getting Started
---------------
Auf der Titelseite müssen Namen, Titel und Abteilung angepasst werden, ebenso in der Versicherung am Ende der Arbeit.

Features
---------------
 - Literaturverzeichnis
 - Abbildungsverzeichnis
 - Tabellenverzeichnis
 - Quelltextauszüge
 - Glossar
 
Feedback
---------------
Verbessungsvorschläge für das Template sind gerne gesehen! Bitte entweder als Issue eintragen oder Änderungen direkt als Pull Request vorschlagen.

Hilfe
---------------
Zur Erstellung der pdf-Datei wird latexmk empfohlen, welches in einer texlive-Installation bereits vorhanden ist. Das Dokument wird dann mit latexmk -pdf theses.tex erstellt.
Um das Glossar zu erzeugen, reicht es nicht aus, die Latexdatei zu kompilieren. Hierzu muss zusätzlich makeglossaries aufgerufen werden und das Dokument erneut kompiliert werden. Um diesen Schritt zu sparen kann folgende latexmkrc angelegt werden:

 add_cus_dep('glo', 'gls', 0, 'run_makeglossaries');
 
 add_cus_dep('acn', 'acr', 0, 'run_makeglossaries');

 sub run_makeglossaries {
   if ( $silent ) {
     system "makeglossaries -q '$_[0]'";
   }
   else {
     system "makeglossaries '$_[0]'";
   };
 }

 push @generated_exts, 'glo', 'gls', 'glg';
 push @generated_exts, 'acn', 'acr', 'alg';
 $clean_ext .= ' %R.ist %R.xdy';

Diese erstellt die Glossareinträge automatisch. Unter Linux muss diese Datei als ~/.latexmkrc erstellt werden.
