## **1) Récupérer les données de séquençage des souches (fichiers fastq)**

•	Dans le bandeau bleu de Galaxy, cliquer sur l’onglet « Data », puis « Histories » et sélectionner « Public histories » et chercher « TP REJMIC » :

<p align="center">
  <img src="captures_tp/1.png" width="2500" height="150">
</p>

•	Lancer la recherche et cliquer sur « view » :
<p align="center">
  <img src="captures_tp/2.png" width="200" height="110">
</p>

•	Puis cliquer sur « import this history » :

<p align="center">
  <img src="captures_tp/3.png">
</p>

- L’historique comprend les fichiers de séquençage de 28 souches de streptocoques du groupe B (Streptococcus agalactiae) et un génome de référence au format GeneBank (gbk) qui correspond au format Fasta avec l’annotation du génome. 

- Le format **FASTQ (Q : Quality)** est un fichier texte contenant les données issues d’un séquençage. Chaque fichier contient les différentes séquences d’ADN, ou reads, associées à un score de qualité **(Q)** pour chaque nucléotide. Pour notre souche, deux fichiers R1 et R2 sont enregistrés sous ce format FASTQ. Ils correspondent aux mêmes fragments d’ADN, séquencés dans les deux sens. En effet, la technologie Illumina réalise du « *paired-end sequencing* », c’est-à-dire que les deux extrémités de chaque fragment d’ADN sont lues par le séquenceur.


<p align="center">
  <img src="captures_tp/4.jpg" width="300" height="150">
</p>


- Les informations relatives à chaque séquence d’ADN sont organisées en 4 lignes :
  - @ + identifiant de séquence
  - Séquence nucléotidique du read
  -  "+"
  - Score de qualité associé à chaque base du read (relié à la probabilité d’erreur)

<p align="center">
  <img src="captures_tp/5.jpg">
</p>

## **2) Créer une collection**

## **3)	Contrôler la qualité des séquences**

L’analyse de la qualité des séquences est une étape importante, réalisée grâce au logiciel FastQC (QC : Quality Control). Pour cela, il faut lancer une analyse FastQC.

NB : il est possible de réaliser un nettoyage des séquences, appelé « *trimming* » qui consiste à :
- Retirer les adaptateurs utilisés afin de fixer les séquences à la flowcell pour le séquençage
- Couper les extrémités des séquences de mauvaise qualité de lecture
- Filtrer les bases avec un mauvais score de qualité en les remplaçant par un « N » (signifiant que la base est indéterminée)
Un des logiciels de nettoyage de séquences les plus utilisés, disponible sur Galaxy, est *trimmomatic*.

**Attention :** Il est important de traiter de la même manière les fichiers R1 et R2

Pour vous aider à comprendre le rapport généré par l'application, vous trouverez le manuel en suivant ce [lien](docs/FastQC_Manual.pdf).

## **4)	Réalisation du mapping et du variant calling**

- Pour cette étape, vous aurez besoin du logiciel Snippy, que vous pouvez chercher dans Galaxy grâce à la fenêtre « search tools » :

<p align="center">
  <img src="captures_tp/6.png">
</p>

- Vous pouvez moduler les paramètres du logiciel selon vos souhaits. Indiquer que vous voulez sélectionner un génome de référence à partir de votre historique et importer votre génome de référence : 

<p align="center">
  <img src="captures_tp/7.png">
</p>

- Vous pouvez également choisir les paramètres de sortie :

<p align="center">
  <img src="captures_tp/8.png">
</p>

- Cliquer sur « Run Tool » :
<p align="center">
  <img src="captures_tp/9.png">
</p>

- Les analyses lancées apparaissent en orange dans votre historique, sur la droite de l’écran : 

<p align="center">
  <img src="captures_tp/10.png">
</p>

- Une fois que les analyses sont terminées, elles apparaissent en vert dans l’historique. Les résultats de cette analyse sont disponibles sous la forme de 3 fichiers différents :
-	Un fichier « vcf » (variant call format) : format standard du rapport de SNP
-	Un fichier tab : correspond à un tableur avec les données
-	Un dossier compressé qui sert d’input au programme Snippy core 

## **5)	Etape d’alignement multiple**

- Nous utiliserons le programme Snippy core afin de générer un fichier Fasta contenant l’alignement multiple de toutes les séquences sur le génome de référence. Cliquer sur « Dataset collection » dans les paramètres du logiciel afin de sélectionner le dossier compressé généré précédemment par Snippy.

<p align="center">
  <img src="captures_tp/11.png">
</p>

Le format FASTA est utilisé pour les séquences nucléotidiques ou protéiques. Les informations d’un fichier FASTA sont organisées deux lignes pour chaque contig :
-	"> + identifiant"
-	Séquence nucléotidique du contig

<p align="center">
  <img src="captures_tp/12.png.jpg">
</p>


- Choisir les caractéristiques de l’output :

<p align="center">
  <img src="captures_tp/13b.png">
</p>


- Cliquer sur « Run Tool »

Le fichier de sortie nécessite une étape de reformatage réalisable grâce à l’outil « Snippy clean full aln » disponible sur Galaxy.

## **6)	Construction de l’arbre phylogénique**

- Pour la construction de l’arbre, nous utilisons le logiciel Fasttree, disponible dans Galaxy :

- Cliquer sur la disquette pour télécharger l’arbre

<p align="center">
  <img src="captures_tp/13.png">
</p>

- Définition modèle GTR + CAT : définition
 -	Pour visualiser l’arbre, il suffit d’importer le fichier sur le site phandango ou iTOL : 
 -	Phandango : [phandango](jameshadfield.github.io)
Cet outil possède l’avantage de permettre également une visualisation de la matrice de SNP, toutefois il n’est pas possible d’enraciner l’arbre

<p align="center">
  <img src="captures_tp/14.png">
</p>

-	iTOL : iTOL: [Interactive Tree Of Life](embl.de)

<p align="center">
  <img src="captures_tp/15.png">
</p>

<p align="center">
  <img src="captures_tp/16.png">
</p>

## **7)	Construction d’une matrice de SNP**
Utilisation du logiciel SNP distance Matrix 
Heatmap
- Créer le workflow

<p align="center">
  <img src="captures_tp/17.png">
</p>
