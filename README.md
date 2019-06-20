# Notebook. Andrew Lai CS185
Open `notebookv1/index.html` to load a local version of the website.  

See `design_document.pdf` instead, for most of the design details/user evaluation/concepts.  

For the art itself: [instagram](https://www.instagram.com/mzcxla/)    
There are two parts to this - the README.md describes some of the coding shit I tried, the PDF describes the other stuff - user experience and whatever. Some parts don't display - especially in `Locations` and `Characters` - because the images are hosted on a webserver, and I couldn't find an easy way to make it work over local.  

## Character Scripts // command line client setup
In terms of the command line client: ideally, you'd be able to do something like `megadoc -c ren_kuraokami --offense S --wealth A` to edit character stats, or directly modify the entry yourself - either by way of the notebook GUI, or directly using a text editor.

An example minimal string:  
`EXAMPLE,EFREN,KO_EFREN,WIZARD,11_9_0_16,MALE,5_10_178_145,HUMAN_EASTERN,STRAIGHT,RED,YELLOW,LIGHT_EASTERN,ENGLISH--KOREAN--MANDARIN,CHAOTIC_NEUTRAL,SWEEPER_LUCID, STUDENT_(KARAKURI_HIGH)",A,N/A,N/A,N/A,GLASSES--HEADPHONES--CODEX,NIGHT_OWL--FAST_LEARNER--PACKRAT,C,D+,C+,SS,C,A-,C-,D-,C+,C-,A,C-,B,F,F-,D,A+,D,B+,A,SS,5,4,4,5,1,2,3,4,2`  

Essentially, the backend for things like stats would be based around parsing and manipulating these minimal strings.  
The client would then parse the strings and generate readable outputs, CS major style. :^)   
This would be especially useful if linked to both the online notebook and the backend of whatever game you have in development.

Here is an example of the `help`:
```
[ APTITUDE ] 		PERCENTILES [F: 0, E: 10, D: 25, C: 50, B: 75, A: 90, S: 98, SS: 99.5]
			        These describe a character's overall placement tiers in different areas.
			        They cannot be directly modified, but some are based off a character's stats.
OFFENSE: 		    Overall offensive ability.
DEFENSE: 		    Overall defensive ability.
SPEED: 			    Overall mobility.
INTELLIGENCE: 	    Overall intelligence. Combination of the first four thought traits.
			        A character with low combat stats but a high intelligence stat can outsmart 
			        stronger characters, and pull victories through strategy alone.
STATUS:			    Overall social standing; how powerful/widespread a character's connections are.
			        A high status stat can basically override everything else.
WEALTH:			    Literally how rich a character is, in terms of EX.
LUCK: 			    In this universe, characters can be born lucky, or born unlucky. :^)
			        This very literally plays as a seed for anything RNG based. Unlucky characters with high 
			        intelligence can override this by never leaving anything to chance.

[ STATS ]		    PERCENTILES [F: 0, E: 10, D: 25, C: 50, B: 75, A: 90, S: 98, SS: 99.5]
			        These are basically a character's current levels and stats, and can be modified.
			        They consist of both the base stat and the character's growth rate for the stat.
STRENGTH: 		    Physical strength. Affects both offense and defense.
DEXTERITY: 		    Affects accuracy and technique.
AGILITY: 		    Affects mobility and dodging.
CONSTITUTION: 		Health pool. High constitution means a character can tank a shit ton.
MAGIC: 			    Magical power. Affects efficacy of mana manipulation, i.e. magic.
MANA: 			    Mana pool. Grows per level, can't be trained. Many characters have 0 mana.
KNOWLEDGE: 		    Overall scholarly aptitude. High knowledge allows for advanced techniques.

[ THOUGHT TRAITS ] 	These describe a character's thinking style and aptitude.
INTELLECT: 		    Ability to learn and grasp complex ideas.
CREATIVITY:		    Ability to innovate and form new ideas.
PROBLEM-SOLVING: 	Ability to solve difficult problems given sufficient information.
CUNNING: 		    Ability to read people and disguise own intentions, aka "street smarts."
AMBITION: 		    Willingness to set difficult goals and follow through.
NARCISSISM:		    Tendency to act selfishly.
SOCIABILITY: 		Willingness to work with others, and ask for help or advice if needed.
DEPRESSION:		    (In)ability to derive pleasure or meaning from anything.
MACHIAVELLIANISM: 	Willingness to fuck over others for personal gain, aka the "villain" stat. 
			        A lawful good character with high machiavellianism is still likely antagonistic.
			        Chessmaster-type characters tend to have high machiavellianism.
```

`EXAMPLE` is the name of their main group.  
```
EXAMPLE // EFREN
[ GENERAL ]		
NAME: 			KO, EFREN
EPITHET:		WIZARD
BIRTHDATE: 		11 SEPTEMBER (AGE 16)
GENDER:			MALE
HEIGHT: 		5'10" | 178 CM
WEIGHT: 		145 LBS | 65 KG
RACE: 			HUMAN (EASTERN)
ORIENTATION: 		STRAIGHT
HAIR COLOR: 		RED
EYE COLOR: 		YELLOW
SKIN COLOR: 		LIGHT (EASTERN)
LANGUAGES:		ENGLISH, KOREAN, MANDARIN
ALIGNMENT:		CHAOTIC NEUTRAL
DESIGNATION: 		SWEEPER (LUCID), STUDENT (KARAKURI HIGH)
FLICKER CLASS: 		A
CLUBS:			N/A
SPORTS:			N/A
FACTION: 		N/A
FEATURES: 		GLASSES, HEADPHONES, CODEX
TRAITS: 		NIGHT OWL, FAST LEARNER, PACKRAT

[ APTITUDE ] 		OVERALL
OFFENSE:		C
DEFENSE:		D+
SPEED:			C+
INTELLIGENCE:		SS
STATUS:			C
WEALTH:			A-
LUCK:			C-

[ STATS ] 		BASE 	GROWTH RATE
STRENGTH: 		D-	C+
DEXTERITY:		C-	A
AGILITY: 		C-	B
CONSTITUTION:		F	F-
MAGIC:			D	A+
MANA: 			D	B+
KNOWLEDGE:		A	SS

[ THOUGHT TRAITS ] 	[0,5] 
INTELLECT: 		5
CREATIVITY:		4
PROBLEM-SOLVING: 	4
CUNNING: 		5
AMBITION: 		1
NARCISSISM:		2
SOCIABILITY: 		3
DEPRESSION:		4
MACHIAVELLIANISM: 	2

EXAMPLE // KYLE
[ GENERAL ]		
NAME: 			KURAOKAMI, KYLE
EPITHET:		KYLE
BIRTHDATE: 		29 OCT (AGE 16)
GENDER:			MALE
HEIGHT: 		6'1"
WEIGHT: 		170 LBS 
RACE: 			REVENANT
ORIENTATION: 		ASEXUAL
HAIR COLOR: 		BLACK
EYE COLOR: 		LAVENDER
SKIN COLOR: 		PALE (REVENANT)
LANGUAGES:		ENGLISH, CLASSICAL JAPANESE
ALIGNMENT:		NEUTRAL EVIL
DESIGNATION: 		SWEEPER, STUDENT (KARAKURI HIGH), BLACK LOTUS
FLICKER CLASS: 		N/A
CLUBS:			N/A
SPORTS:			N/A
FACTION: 		N/A
FEATURES: 		SWORD
TRAITS: 		NIGHT OWL, FAST LEARNER, KURAOKAMI, ANTISOCIAL, HEAVYWEIGHT

[ APTITUDE ] 		OVERALL
OFFENSE:		S
DEFENSE:		A
SPEED:			A-
INTELLIGENCE:		A-
STATUS:			B+
WEALTH:			A-
LUCK:			C

[ STATS ] 		BASE 	GROWTH RATE
STRENGTH: 		A-	A-
DEXTERITY:		A	SS
AGILITY: 		B+	S+
CONSTITUTION:		A+	A
MAGIC:			F	F
MANA: 			F	F
KNOWLEDGE:		C+	A

[ THOUGHT TRAITS ] 	[0,5] 
INTELLECT: 		5
CREATIVITY:		1
PROBLEM-SOLVING: 	5
CUNNING: 		5
AMBITION: 		2
NARCISSISM:		5
SOCIABILITY: 		1
DEPRESSION:		0
MACHIAVELLIANISM: 	4

EXAMPLE // RIKA
[ GENERAL ]		
NAME: 			NEINHART, RIKA
BIRTHDATE: 		4 JUNE (AGE 15)
GENDER:			FEMALE
HEIGHT: 		5'1"
WEIGHT: 		119 LBS 
RACE: 			HUMAN (WESTERN)
ORIENTATION: 		BISEXUAL
HAIR COLOR: 		WHITE
EYE COLOR: 		VIOLET
SKIN COLOR: 		LIGHT (WESTERN)
LANGUAGES:		ENGLISH, ANCIENT
ALIGNMENT:		CHAOTIC GOOD
DESIGNATION: 		SWEEPER, STUDENT (KARAKURI HIGH)
FLICKER CLASS: 		N/A
CLUBS:			N/A
SPORTS:			N/A
FACTION: 		N/A
FEATURES: 		BLADE, GUN, PENDANT, SCYTHE
TRAITS: 		EARLY BIRD, LIGHTWEIGHT, MAGICAL GIRL, NOBILITY

[ APTITUDE ] 		OVERALL
OFFENSE:		B+
DEFENSE:		C-
SPEED:			A+
INTELLIGENCE:		C-
STATUS:			A
WEALTH:			C
LUCK:			F+

[ STATS ] 		BASE 	GROWTH RATE
STRENGTH: 		B	A-
DEXTERITY:		C+	A
AGILITY: 		B	A+
CONSTITUTION:		D	C
MAGIC:			B+	A
MANA: 			A	A+
KNOWLEDGE:		C	B-

[ THOUGHT TRAITS ] 	[0,5] 
INTELLECT: 		3
CREATIVITY:		5
PROBLEM-SOLVING: 	2
CUNNING: 		0
AMBITION: 		5
NARCISSISM:		4
SOCIABILITY: 		5
DEPRESSION:		1
MACHIAVELLIANISM: 	0

EXAMPLE // KIMMIE
[ GENERAL ]		
NAME: 			MINAZUKI, MIHO
BIRTHDATE: 		12 FEBRUARY (AGE 16)
GENDER:			FEMALE
HEIGHT: 		5'6" 
WEIGHT: 		126 LBS 
RACE: 			HUMAN (MIXED)
ORIENTATION: 		ASEXUAL
HAIR COLOR: 		BLONDE
EYE COLOR: 		GREEN
SKIN COLOR: 		LIGHT (WESTERN)
LANGUAGES:		ENGLISH, JAPANESE, MANDARIN, KOREAN, FRENCH, RUSSIAN
ALIGNMENT:		NEUTRAL GOOD
DESIGNATION: 		SWEEPER, STUDENT (KARAKURI HIGH)
FLICKER CLASS: 		N/A
CLUBS:			N/A
SPORTS:			N/A
FACTION: 		N/A
FEATURES: 		MODEL
TRAITS: 		HONORS STUDENT, HIGH SOCIETY, MULTILINGUAL

[ APTITUDE ] 		OVERALL
OFFENSE:		S+
DEFENSE:		C-
SPEED:			C-
INTELLIGENCE:		S+
STATUS:			S
WEALTH:			S+
LUCK:			A

[ STATS ] 		BASE 	GROWTH RATE
STRENGTH: 		C	C
DEXTERITY:		S	C-
AGILITY: 		C	C+
CONSTITUTION:		C-	C-
MAGIC:			SS	C+
MANA: 			A+	A+
KNOWLEDGE:		S	A+

[ THOUGHT TRAITS ] 	[0,5] 
INTELLECT: 		5
CREATIVITY:		3
PROBLEM-SOLVING: 	5
CUNNING: 		4
AMBITION: 		1
NARCISSISM:		0
SOCIABILITY: 		1
DEPRESSION:		4
MACHIAVELLIANISM: 	0
```
