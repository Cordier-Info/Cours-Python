---
title: "Sommaire"
weight: 0
---



<script>
  var callback = function(){
      window.open("https://www.w3schools.com")
  }
</script>

{{< mermaid >}}

flowchart TB

subgraph cours1  [Cours 1 : Bases]
A1(Shell et IDE) & A2(Types de nombres) & A3(Arithmétique de base) & A4(Méthodes et attributs) & A5(Fonctions mathématiques) & A6(Variables) & A7(Comparaison et logique) & A8(type None) 
end

subgraph cours2 [Cours 2 : Chaînes de caractères]
B1(Définir une chaîne de caractères) & B2(Caractères d'échappement) & B3(Indexation et slicing) & B4(Méthodes liées aux chaînes) & B5(La fonction print) & B6(Formattage)
end

TP2(TP2)

cours1 --> TP2

cours2 --> TP2

subgraph cours3 [Cours 3 : Séquences et itérables]
C1(Séquences) & C2(Objets itérables) 
C1 -.- C11(Listes) & C12(Tuples) 
C2 -.-  C21(range) & C22(enumerate) & C23(zip) & C24(Ensembles) & C25(Dictionnaires)
C11-.- C111(Indexation) & C112(Slicing) & C113(Mutablité) & C114(Méthodes) 
C1 -.- C2
C3(Boucle for)
C3 -.- C2
C4(Listes par compréhension)
end

TP3(TP3)

cours3 --> TP3

subgraph cours4 [Cours 4 : Structures de contrôle]
D1(if, elif, else) & D2(Boucles while) & D3(break, continue et else) & D4(Gestion d'exception) 
end

TP4(TP4)

cours4--> TP4

subgraph cours5 [Cours 5 : Fonctions]
E1(Définir et appeler) & E2(Chaîne de documentation) & E3(Argument nommé)  & E4(Valeur par défaut des arguments) & E5(Portée des variables) & E6(Fonctions lambda) & E7(Les assertions)
end

subgraph cours6 [Cours 6 : Manipulation de fichiers]
F1(Interaction avec l'OS) & F2(Lecture et écriture) & F3(Fichiers images) & F4(Interaction avec l'utilisateur) & F5(Récupérer des données sur le web)
F2-.- F21(Ouvrir et fermer un fichier) & F22(Ecrire dans un fichier) & F23(Lire un fichier)
end

TP5(TP5)

cours5 & cours6 --> TP5

TP2 & TP3 & TP4 & TP5 --> TP6(TP6 : Projets)

click A1 "/cours_python/cours1/"
click A2 "/cours_python/cours1/#types-de-nombres"
click A3 "/cours_python/cours1/#arithmétique-de-base"
click A4 "/cours_python/cours1/#méthodes-et-attributs"
click A5 "/cours_python/cours1/#fonctions-mathématiques"
click A6 "/cours_python/cours1/#variables"
click A7 "/cours_python/cours1/#comparaison-et-logique"
click A8 "/cours_python/cours1/#type-none"

click B1 "/cours_python/cours2/"
click B2 "/cours_python/cours2/#caractères-déchappement"
click B3 "/cours_python/cours2/#indexation-et-slicing"
click B4 "/cours_python/cours2/#méthodes-liées-aux-chaînes"
click B5 "/cours_python/cours2/#la-fonction-print"
click B6 "/cours_python/cours2/#formatage-des-chaînes-de-caractères"

click C1 "/cours_python/cours3/"
click C11 "/cours_python/cours3/"
click C111 "/cours_python/cours3/#indexation"
click C112 "/cours_python/cours3/#slicing"
click C113 "/cours_python/cours3/#mutabilité-des-listes"
click C114 "/cours_python/cours3/#méthodes"
click C12 "/cours_python/cours3/#tuples"
click C2 "/cours_python/cours3/#objets-itérables"
click C21 "/cours_python/cours3/#range"
click C22 "/cours_python/cours3/#enumerate"
click C23 "/cours_python/cours3/#zip"
click C24 "/cours_python/cours3/#ensembles"
click C25 "/cours_python/cours3/#dictionnaires"
click C3 "/cours_python/cours3/#boucle-for"
click C4 "/cours_python/cours3/#listes-par-compréhension"

click D1 "/cours_python/cours4/"
click D2 "/cours_python/cours4/#boucles-while"
click D3 "/cours_python/cours4/#break-continue-et-else"
click D4 "/cours_python/cours4/#la-gestion-dexceptions"

click E1 "/cours_python/cours5/"
click E2 "/cours_python/cours5/#chaîne-de-documentation"
click E3 "/cours_python/cours5/#argument-nommé"
click E4 "/cours_python/cours5/#valeur-par-défaut-des-arguments"
click E5 "/cours_python/cours5/#portée-des-variables"
click E6 "/cours_python/cours5/#fonctions-lambda--des-fonctions-anonymes"
click E7 "/cours_python/cours5/#les-assertions"

click F1 "/cours_python/cours6/"
click F2 "/cours_python/cours6/#lecture-et-écriture-de-fichiers"
click F21 "/cours_python/cours6/#lecture-et-écriture-de-fichiers"
click F22 "/cours_python/cours6/#écrire-dans-un-fichier"
click F23 "/cours_python/cours6/#lire-un-fichier"
click F3 "/cours_python/cours6/#fichiers-image"
click F4 "/cours_python/cours6/#interaction-avec-lutilisateur--la-fonction-input"
click F5 "/cours_python/cours6/#récupérer-des-données-sur-le-web"

click TP2 "/tp_python/tp2/"
click TP3 "/tp_python/tp3/"
click TP4 "/tp_python/tp4/"
click TP5 "/tp_python/tp5/"
click TP6 "/tp_python/tp6/"

classDef important fill:#f88,stroke:#f66,stroke-width:2px,color:#fff;

classDef TP fill:#cfc,stroke:#2a2,stroke-width:2px;

class A6,B3,C11,C3,D1,D2,E1,E5 important;
class TP2,TP3,TP4,TP5,TP6 TP;

{{< /mermaid >}}








