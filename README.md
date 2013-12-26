\documentclass[a4paper,12pt]{article}
\usepackage[utf8]{inputenc}
\usepackage[francais]{babel}
\usepackage[T1]{fontenc}
\title{Rapport LinkStateRouting}
\author{Elodie Delcambe 142066 & Alois Paulus 141582 Groupe 11}

\begin{document}

\tableofcontents
\newpage
\section{Construction et Exécution}
\subsection{Construction}
\begin{itemize}
\item se placer dans le dossier src
\item lancer la commande : javac -d ../build -sourcepath . linkStateRouting/Demo.java

\end{itemize}
\subsection{Exécution}
\begin{itemize}
\item se placer dans le dossier build
\item lancer la commande : java -cp . linkStateRouting.Demo

\end{itemize}

\section{Explication du projet}
\begin{itemize}
\item 1ère étape: Découverte des voisins.
Lorsqu'un voisin est découvert, il est ajouté dans une HashMap qui représente la liste des voisins. Pour chaque voisin, on conserve plusieurs informations tel que la distance, l'interface et l'identifiant du routeur.

\item 2ème étape: Le flooding.
Chaque routeur envoie un LSP sur toutes ses interfaces qu'il construit à partir de sa liste de voisins et forward les LSP reçus des autres routeurs.
Lorsqu'il reçoit un LSP, il le stocke dans une HashMap appelée LSDB et chaque entrée de cette HashMap va contenir l'indentifiant du routeur, le numéro de séquence et la liste de ses voisins.

\item 3ème étape: Calcul du plus court chemin à l'aide de l'algorithme de Dijkstra.
\begin{itemize}
\item Utilisation de la méthode de "Decrease Key" à la place de "l'insert delete" pour des raisons de rapidité. 
\item Utilisation du tas de Fibonacci dans cet algorithme, également pour des raisons de rapidité.
\end{itemize}
\end{itemize}
\newpage
\section{Problèmes rencontrés}
\begin{itemize}
\item
Au début, on avait supposé qu'on connaissait déjà tous nos voisins grâce aux interfaces et donc notre table des voisins était incorrecte. Pour résoudre ce problème, on a implémenté correctement les "Hello packets".
\item
Lors de la 3ème étape, on a rencontré un problème au niveau du calcul du plus court chemin. On additionnait deux valeurs positives et on obtenait une valeur négative à cause que l'une des valeurs valait un integer.max
\item
Le second problème au niveau de cet algorithme est apparu lors du changement de méthode : insert delete vers decrease key. Il suffisait de changer la méthode d'initialisation.
\end{itemize}
\section{État de l'implémentation finale} 
\subsection{Ce qui a été implémenté}
\begin{itemize}
\item 
La découverte des voisins
\item
Le flooding
\item
L'algorithme de Dijkstra et tas de Fibonacci
\item
Timer pour les LSP et les "packets Hello"
\item Timer pour les changements d'états des interface : up, down et distance.
\end{itemize}
 \subsection{Ce qui n'a pas été implémenté}
\begin{itemize}
\item 
Suppression des LSP au bout d'un certain temps (ageing)
\end{itemize}
\end{document} 
