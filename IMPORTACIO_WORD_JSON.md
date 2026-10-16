# Conversió de PI Word a JSON · esquema del generador v0.84

La versió de l'aplicació és 0.84; l'esquema del fitxer continua sent `pi.primaria.v0.2`, amb les dades dins de `data`.

No n'hi ha prou amb extreure les taules del Word. Cal mapar les dades a cada camp, sense copiar-hi les etiquetes ni les instruccions de plantilla.

- `reason`: només la justificació individual. Mai la llista «Motivat per», ni les instruccions de la plantilla.
- `justificationChecks`: índexs de les opcions marcades, començant per 0. Ordre: informe NESE, avaluació psicopedagògica, avaluació inicial nouvingut, origen estranger fora d'acollida, incorporació tardana, CAEI, altres. No deduir marques que no siguin identificables.
- `group`: curs escolar de primària, per exemple `4t`. `classGroup`: lletra o grup de classe. `year`: any acadèmic, per exemple `2025-2026`.
- `professionals`: objecte per índex del rol. Cada entrada conté `active` (casella) i `detail` (nom o dada real). No posar l'etiqueta del rol dins de `detail`.
- `previousSupports`: dades que segueixen l'etiqueta de suports anteriors, sense reproduir l'etiqueta.
- `staffMeetings`, `familyMeetings`, `continuityMeetings`: dates a `Data`, persones a `Agents participants` i contingut a les columnes corresponents. Les dades poden estar a les cel·les de capçalera del Word. Cal llegir-les abans de descartar una fila com a capçalera. No inventar un acord seleccionat quan només hi ha una llista d'opcions.
- `objectives`: un registre per criteri general. `reference` conté el codi; `statement` conté el text sense tornar a incloure el mateix codi. `area` i `cycle` separats. `specificCriterion` conté una adaptació completa per línia: unir salts de línia purament tipogràfics del Word, mantenir separades les adaptacions que siguin realment diferents. No dividir per cada frase o signe de puntuació.
- Si es fa servir `adaptationsManaged:true`, cal omplir `selectedAdaptations` i/o `customAdaptation`; no deixar només `specificCriterion`, perquè les files es generen a partir d'aquests camps estructurats.
- Conservar el document extret íntegre a `sourceArchive` o `sourceDocument`, fora dels camps imprimibles. No omplir `sourceNotes` amb la plantilla sencera.
- No inventar dades absents ni substituir criteris originals per oficials sense un contrast explícit.

Comprovació abans de lliurar: importació al generador, revisió dels camps i caselles, exportació PDF i comprovació visual. Els textos ambigus s'han d'identificar; conservar l'original no equival a haver-lo mapat correctament.

La v0.84 repara patrons inequívocs d'extraccions anteriors i conserva els valors substituïts a `importRecovery.originalFields`. La recuperació no és un convertidor universal de Word ni pot reparar dades perdudes que no siguin a l'arxiu.
