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

A00(Résumé cours 1)

subgraph cours1  [Cours 1 : Bases]
A1(Shell et IDE) & A2(Installation) & A3(Types de nombres) & A4(Arithmétique de base) & A5(Méthodes et attributs) & A6(Fonctions mathématiques) & A7(Variables) & A8(Comparaison et logique) & A9(type None) 
end

B00(Résumé cours 2)

subgraph cours2 [Cours 2 : Chaînes de caractères]
B1(Définir une chaîne de caractères) & B2(Caractères d'échappement) & B3(Indexation et slicing) & B4(Méthodes liées aux chaînes) & B5(La fonction print) & B6(Formatage)
end

TP2(TP2)

A00 -.- cours1 --> TP2

B00-.-cours2 --> TP2

C00(Résumé cours 3)

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

C00-.-cours3 --> TP3

D00(Résumé cours 4)

subgraph cours4 [Cours 4 : Structures de contrôle]
D1(if, elif, else) & D2(Boucles while) & D3(break, continue et else) & D4(Gestion des exceptions) 
end

TP4(TP4)

D00-.-cours4--> TP4

E00(Résumé cours 5)

subgraph cours5 [Cours 5 : Fonctions]
E1(Définir et appeler) & E2(Chaîne de documentation) & E3(Argument nommé)  & E4(Valeur par défaut des arguments) & E5(Portée des variables) & E6(Fonctions lambda) & E7(Les assertions)
end

subgraph cours6 [Cours 6 : Manipulation de fichiers]
F1(Interaction avec l'OS) & F2(Lecture et écriture) & F3(Fichiers images) & F4(Interaction avec l'utilisateur) & F5(Récupérer des données sur le web)
F2-.- F21(Ouvrir et fermer un fichier) & F22(Ecrire dans un fichier) & F23(Lire un fichier)
end

TP5(TP5)
E00-.-cours5
cours5 & cours6 --> TP5

TP2 & TP3 & TP4 & TP5 --> TP6(TP6 : Projets)

click A1 "/cours_python/cours1/"
click A2 "/cours_python/cours1/#installation"
click A3 "/cours_python/cours1/#types-de-nombres"
click A4 "/cours_python/cours1/#arithmetique"
click A5 "/cours_python/cours1/#methodes"
click A6 "/cours_python/cours1/#fmathematiques"
click A7 "/cours_python/cours1/#variables"
click A8 "/cours_python/cours1/#comparaison-et-logique"
click A9 "/cours_python/cours1/#type-none"

click B1 "/cours_python/cours2/"
click B2 "/cours_python/cours2/#echappement"
click B3 "/cours_python/cours2/#indexation-et-slicing"
click B4 "/cours_python/cours2/#methodeschaines"
click B5 "/cours_python/cours2/#la-fonction-print"
click B6 "/cours_python/cours2/#formatage"

click C1 "/cours_python/cours3/"
click C11 "/cours_python/cours3/"
click C111 "/cours_python/cours3/#indexation"
click C112 "/cours_python/cours3/#slicing"
click C113 "/cours_python/cours3/#mutabilite"
click C114 "/cours_python/cours3/#methodes"
click C12 "/cours_python/cours3/#tuples"
click C2 "/cours_python/cours3/#iterables"
click C21 "/cours_python/cours3/#range"
click C22 "/cours_python/cours3/#enumerate"
click C23 "/cours_python/cours3/#zip"
click C24 "/cours_python/cours3/#ensembles"
click C25 "/cours_python/cours3/#dictionnaires"
click C3 "/cours_python/cours3/#boucle-for"
click C4 "/cours_python/cours3/#comprehension"

click D1 "/cours_python/cours4/"
click D2 "/cours_python/cours4/#boucles-while"
click D3 "/cours_python/cours4/#break-continue-et-else"
click D4 "/cours_python/cours4/#la-gestion-des-exceptions"

click E1 "/cours_python/cours5/"
click E2 "/cours_python/cours5/#chainededocumentation"
click E3 "/cours_python/cours5/#argumentnomme"
click E4 "/cours_python/cours5/##valeurpardefaut"
click E5 "/cours_python/cours5/#porteedesvariables"
click E6 "/cours_python/cours5/#fonctions-lambda--des-fonctions-anonymes"
click E7 "/cours_python/cours5/#les-assertions"

click F1 "/cours_python/cours6/"
click F2 "/cours_python/cours6/#lectureetecriture"
click F21 "/cours_python/cours6/#lectureetecriture"
click F22 "/cours_python/cours6/#ecrire"
click F23 "/cours_python/cours6/#lire-un-fichier"
click F3 "/cours_python/cours6/#fichiers-image"
click F4 "/cours_python/cours6/#interaction-avec-lutilisateur--la-fonction-input"
click F5 "/cours_python/cours6/#web"

click TP2 "/tp_python/tp2/"
click TP3 "/tp_python/tp3/"
click TP4 "/tp_python/tp4/"
click TP5 "/tp_python/tp5/"
click TP6 "/tp_python/tp6/"

click A00 "http://cordier-phychi.toile-libre.org/Info/cours1_pres"
click B00 "http://cordier-phychi.toile-libre.org/Info/cours2_pres"
click C00 "http://cordier-phychi.toile-libre.org/Info/cours3_pres"
click D00 "http://cordier-phychi.toile-libre.org/Info/cours4_pres"
click E00 "http://cordier-phychi.toile-libre.org/Info/cours5_pres"

classDef important fill:#f88,stroke:#f66,stroke-width:2px,color:#fff;
classDef resume fill:#5af,stroke:#66f,stroke-width:2px,color:#fff;
classDef TP fill:#cfc,stroke:#2a2,stroke-width:2px;

class A00,B00,C00,D00,E00 resume;
class A7,B3,C11,C3,D1,D2,E1,E5 important;
class TP2,TP3,TP4,TP5,TP6 TP;

{{< /mermaid >}}








