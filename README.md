# rehearser script

## Introduction

### Context

Actors require a text to memprize. They usually learn there lines and memorize their scenes. 

- Remarques :
  - long texts are hard to memorize

> simple line and no software involved yet
> >This document describes the algorithm for editing a text file containing the text of atheater play (= "text"), in order to put it in a format for importing into the "Script Rehearser" software (SR). SR helps actors memorise text, by playing the actors' lines (and the other character's lines) aloud.

> might be in strategy or software architecture and procedure
>> - SR interpets the text as follows:
>>    - text spoken (="script") by a theater character (= "person") if it is preceded by a line containing the name of this person name in uppercase, itself preceded by an empty line
>>    - the stage "directions" if contained in parentheses
>>    - the "transition" line if it contains certain keywords

### Objective

- SR plays one person block at the time.
- Software to be implemented would:
  - import texts from a file
  - display lines for each roles
  - split text in small chunks

### Strategy

Develop a software which can read a file, define chunks and display lines.

> This are some information to help the developper to produce each part of the software
> > - Analyse the script line by line, and we call:
> >   - "transition": a line containing a keyword (SCENE, ACT, END, FIN)
> >   - "person" name: a line all in uppercase
> >   - "main line": a transition line or a person line
> >   - "directions": a line contained in parentheses
> >   - "blank": an empty line
> >   - "script": any other line, assumed to be actual script
> >   - "block": a group of lines starting from (and including) a main line, until (and excluding) another main line
> >   - "person block": a block whose first line is a person name (these contain the actual script, plus possibly stage directions)
> > - Then break the person blocks into smaller blocks if they are large, or contain multiple stage directions.

## File description

a file has the following format:

```text
TITRE : L'ILE DES ESCLAVES

SCENE I 
(Iphicrate s'avance tristement sur le théâtre avec Arlequin)

IPHICRATE
(s'avance tristement sur le théâtre avec Arlequin)
Arlequin ?

ARLEQUIN
(avec une bouteille de vin qu'il a à sa ceinture)
Mon patron.

IPHICRATE
Que deviendrons-nous dans cette île ?
```

```text
CREON
Et, puisque je suis roi, j'ai résolu, avec moins d'ambition que ton père, de m'employer tout simplement à rendre l'ordre de ce monde un peu moins absurde, si c'est possible.

CREON
Ce n'est même pas une aventure, c'est un métier pour tous les jours et pas toujours drôle, comme tous les métiers. Mais puisque je suis là pour le faire, je vais le faire...

CREON
Alors, écoute-moi bien. Tu es Antigone, tu es la fille d'Oedipe, soit, mais tu as vingt ans et il n'y a pas longtemps encore tout cela se serait réglé par du pain sec et une paire de gifles.

(Il la regarde, souriant.)

CREON
Te faire mourir ! Tu ne t'es pas regardée, moineau ! Tu es trop maigre. Grossis un peu, plutôt, pour faire un beau bébé à mon fils.
```

- BLANK_LINE: Line without content and informing about the transition nature
- TITRE: define the title of the play
- SCENE [order]: scene number represented by a roman number or a number or another sequence string (I, 1, PREMIÈRE)
- PERSON NAME: name of the person telling the following lines until next BLANK_LINE.
  - under the PERSPN NAME tag one should find (order is not requiered:
  - (**xxxx[, yyyy]]**): define directions to help the actor, can be other characters or attitude, whatever
  - TEXT: text of the character (PERSON_NAME)

## Use cases

### Load File

This function return content of a file

### Analyze file

This function produces an object which can be used by other functions

### Display 

#### Define filter

This function outputs available criteria to produce request form
 
#### using filter

This function inputs a filter to extract corresponding  texts

