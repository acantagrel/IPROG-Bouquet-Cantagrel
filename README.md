using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;


namespace ProjetInfo
{
    class Program
    {
        //BATAILLE NAVALE SALVO
        /*
         * PROJET IPROG 2017 - ENSC 1A
         * Auteurs : BOUQUET Antoine, CANTAGREL Alice 
         * TD 3
         * Objectif : créer une interface de jeu de bataille navale contre une IA.
         */
        static void DebuterPartie(ref bool bool1, ref bool bool2, ref bool bool3, ref bool bool4, ref char[,] tab, ref char[,] tab1, ref int[] donnees1, ref int[] donnees2)
        {
            /*procédure qui présente le jeu.
            * Arguments : 
            *     - bool1 : booléen, réponse du joueur pour le mode de jeu à conserver (INOUT)
            *     - bool2 : booléen, réponse du joueur pour le niveau de l'ordi à conserver (INOUT)
            *     - bool3 : booléen, réponse du joueur pour le chargement de la partie à conserver (INOUT)
            *     - bool4 : Booléen, réponse joueur pour le placement des bateaux manuellement à conserver (INOUT)
            *     - tab : tableau de charactères à deux dimensions, plateau de jeu à conserver (INOUT)
            *     - tab1 : tableau de charactères à deux dimensions, plateau de jeu à conserver (INOUT)
            *     - donnees1 : tableau d'entier, données de jeu à conserver (INOUT)
            *     - donnees2 : tableau d'entier, données de jeu à conserver (INOUT)
            * Variables : 
            *     - reponse : string, contient la réponse du joueur entrée sur la console
            *     - reponse2 : string, contient la réponse du joueur entrée sur la console
            *     - reponse3 : string, contient la réponse du joueur entrée sur la console
            * Appel : 
            *     - ReprendrePartie()
            * Préconditions : aucune
            * Postconditions : modifie les valeurs de bool1 et bool2
            */
            Console.WriteLine(" _____       ___   _____       ___   _   _       _       _____  ");
            Console.WriteLine("|  _  \\     /   | |_   _|     /   | | | | |     | |     | ____| ");
            Console.WriteLine("| |_| |    / /| |   | |      / /| | | | | |     | |     | |__   ");
            Console.WriteLine("|  _  {   / / | |   | |     / / | | | | | |     | |     |  __|  ");
            Console.WriteLine("| |_| |  / /  | |   | |    / /  | | | | | |___  | |___  | |___");
            Console.WriteLine("|_____/ /_/   |_|   |_|   /_/   |_| |_| |_____| |_____| |_____| ");
            Console.WriteLine("\n\n __   _       ___   _     _       ___   _       _____ ");
            Console.WriteLine("|  \\ | |     /   | | |   / /     /   | | |     | ____|");
            Console.WriteLine("|   \\| |    / /| | | |  / /     / /| | | |     | |__   ");
            Console.WriteLine("| |\\   |   / / | | | | / /     / / | | | |     |  __| ");
            Console.WriteLine("| | \\  |  / /  | | | |/ /     / /  | | | |___  | |___  ");
            Console.WriteLine("|_|  \\_| /_/   |_| |___/     /_/   |_| |_____| |_____| ");
            Console.WriteLine("\n\n############################### BATAILLE NAVALE ###############################");
            Console.WriteLine("\nBienvenue ! Ce jeu vous permet de jouer à la bataille navale contre votre ordinateur.");
            string reponse = "a";
            while ((reponse != "o") && (reponse != "n"))
            {
                Console.WriteLine("Voulez-vous lire les règles ? (o/n)");
                reponse = Console.ReadLine();
            }
            if (reponse == "o")
            {
                Console.WriteLine("##### REGLES #####\n\nPour jouer à la bataille navale, chaque joueur dispose de 5 bateaux et d’un plateau de jeu carré \n de taille 10x10. Le plateau de jeu comporte donc 100 cases repérées en colonne par des lettres \n (colonne A, colonne B, …, colonne J) et repérées en ligne par des chiffres (ligne 1, ligne 2, … ligne 10).\n");
                Console.WriteLine("En début de partie, chaque joueur place ses bateaux sur son plateau sans voir celui de son adversaire.\n Le but de la bataille navale est ainsi de trouver et de couler tous les bateaux de son adversaire.\n Pour cela, chacun à leur tour, les joueurs essaient de tirer sur les bateaux de l'adversaire.\n Chaque joueur dispose de 5 bateaux longueurs différentes: \n");
                Console.WriteLine("Un porte - avion d'une longueur de 5 cases\n");
                Console.WriteLine("Un cuirassé d'une longueur de 4 cases \n");
                Console.WriteLine("Un sous - marin et un croiseur d'une longueur de 3 cases \n");
                Console.WriteLine("Un contre - torpilleur d'une longueur de 2 cases \n");
                Console.WriteLine("Suivant le mode de jeu choisi, la façon de tirer ne s’effectue pas de la même manière:\n");
                Console.WriteLine("le mode classique: A chaque tir annoncé par un joueur(par exemple, 'case C5'), \n le second joueur regarde si l’un de ses navires occupe la case visée.Il doit indiquer à l'autre\n joueur s'il a touché('Touché') ou coulé('Touché coulé') un navire ou bien tiré dans l'eau ('Raté').\n");
                Console.WriteLine("le mode salvo: chaque joueur annonce plusieurs tirs à la fois.Le nombre de tirs simultanés est\n de 5 initialement.Ce nombre diminue en fonction du nombre de bateaux déjà coulés.\n Quand un joueur détruit un navire de son adversaire, il ne tire plus que 4 coups au lieu de 5.\n Quand 2 bateaux sont détruits, le joueur ennemi tire uniquement 3 coups. \nQuand 3 navires sont détruits, le joueur opposé ne tire plus que 2 coups, etc.\n A chaque tir, l’adversaire indique si le joueur a touché('Touché') ou coulé('Touché coulé')\n un navire ou bien tiré dans l'eau ('Raté').\n");
            }
            ReprendrePartie(ref bool3, ref tab, ref tab1, ref donnees1, ref donnees2, ref bool1, ref bool2);
            if (bool3 == false)
            {
                string reponse2 = "a";
                while ((reponse2 != "s") && (reponse2 != "n"))
                {
                    Console.WriteLine("Avec quel mode voulez-vous jouer ? Tapez 's' pour le mode Salvo ou 'n' pour le mode normal");
                    reponse2 = Console.ReadLine();
                }
                if (reponse2 == "n")
                {
                    bool1 = false; //mode de jeu
                }
                string reponse3 = "a";
                while ((reponse3 != "f") && (reponse3 != "i"))
                {
                    Console.WriteLine("Quel niveau souhaitez-vous pour l'ordinateur ? Tapez 'f' pour facile ou 'i' pour intelligent");
                    reponse3 = Console.ReadLine();
                }
                if (reponse3 == "i")
                {
                    bool2 = true; //niveau de difficulté
                }
                reponse = "a";
                while ((reponse != "o") && (reponse != "n"))
                {
                    Console.WriteLine("Voulez-vous placer vos bateaux vous même ? (o/n)");
                    reponse = Console.ReadLine();
                }
                if (reponse == "o")
                {
                    bool4 = true;//placement manuel
                }
            }
        }

        static void InitialiserPlateau(char[,] tab, char[] tabBateau, int nb, ref int[] data)
        {
            /*procédure qui place aléatoirement les bateaux  sur le plateau de jeu correspondant
             * Arguments : 
             *     - tab : tableau de char à deux dimensions, contient les éléments à afficher (IN)
             *     - tabBateau : tableau de char à une dimension, représente un bateau. Concrètement, le symbole contenu dans chacune des cases de ce tableau indique l'état du bateau (touché ou non). (IN)
             *     - nb : entier, permet d'écrire dans data à partir d'un certain rang (IN)
             *     - data : tableau d'entiers à une dimension, contient les éléments importants permettant de situer chaque bateau sur le plateau de jeu de l'IA. La procédure permet de modifier ce tableau. (INOUT)
             * Variables : 
             *     - r : random
             *     - choix : entier, détermine le placement vertical ou horizontal
             *     - test : booléen, sert à détermine si il y a la place de placer tabBateau à l'endroit choisi 
             *     - indiceI : entier, valeur de i à récupérer dans data
             *     - indiceJ : entier, valeur de j à récupérer dans data 
             *     - i : entier, valeur prise aléatoirement entre 0 et 9 pour déterminer la première case de tab où placer tabBateau (ligne)
             *     - j : entier, valeur prise aléatoirement entre 0 et 9 pour déterminer la première case de tab où placer tabBateau (colonne)
             *     - k : entier, compteur de la taille de tabBateau
             * Préconditions : dans le contexte où cette procédure sera utilisée, nb doit être inférieur à 5 car data.Length vaudra 20
             * Postconditions : les valeurs de data ont été modifiées
             */
            Random r = new Random();
            int choix;
            bool test;
            int indiceI; //à récupérer, premier case du bateau
            int indiceJ;//à récupérer, premier case du bateau
            do
            {
                choix = r.Next(2);
                test = true;

                if (choix == 0)//place verticalement
                {

                    int i = r.Next(10);
                    int j = r.Next(10 - tabBateau.Length);
                    indiceI = i;
                    indiceJ = j;
                    //teste si le tableau est vide là où on veut écrire
                    int k; //compteur de la taille du tableau du bateau
                    for (k = 0; k < tabBateau.Length; k++)
                    {
                        if (tab[i, j + k] != 0)
                        {
                            test = false;
                        }
                    }

                    if (test == true)
                    {
                        for (k = 0; k < tabBateau.Length; k++)
                        {
                            tab[i, j + k] = tabBateau[k];
                        }
                    }

                }
                else// place horizontalement
                {


                    int j = r.Next(10);
                    int i = r.Next(10 - tabBateau.Length);
                    indiceI = i;
                    indiceJ = j;
                    //teste si le tableau est vide là où on veut écrire
                    int k; //compteur de la taille du tableau du bateau
                    for (k = 0; k < tabBateau.Length; k++)
                    {
                        if (tab[i + k, j] != 0)
                        {
                            test = false;
                        }
                    }

                    if (test == true)
                    {
                        for (k = 0; k < tabBateau.Length; k++)
                        {
                            tab[i + k, j] = tabBateau[k];
                        }
                    }
                }
            } while (test == false);
            //data = { tabBateau.Length, choix, indiceI; indiceJ};
            data[0 + nb * 4] = tabBateau.Length;
            data[1 + nb * 4] = choix;
            data[2 + nb * 4] = indiceI;
            data[3 + nb * 4] = indiceJ;
        }

        static void PlacerBateau(char[,] tab, char[] tabBateau, int nb, ref int[] data)
        {
            /*procédure qui permet au joueur de placer ses bateaux  sur le plateau de jeu correspondant
             * Arguments : 
             *     - tab : tableau de char à deux dimensions, contient les éléments à afficher (IN)
             *     - tabBateau : tableau de char à une dimension, représente un bateau. Concrètement, le symbole contenu dans chacune des cases de ce tableau indique l'état du bateau (touché ou non) (IN)
             *     - nb : entier, permet d'écrire dans data à partir d'un certain rang (IN)
             *     - data : tableau d'entiers à une dimension, contient les éléments importants permettant de situer chaque bateau sur le plateau de jeu de l'IA. La procédure permet de modifier ce tableau. (INOUT)
             * Variables : 
             *     - saisieUtilisateur : chaîne de charactère , réponse de l'utilisateur
             *     - choix : entier, détermine le placement vertical ou horizontal
             *     - test : booléen, sert à détermine si il y a la place de placer tabBateau à l'endroit choisi 
             *     - indiceLigne : entier, valeur de i à récupérer dans data
             *     - indiceColonne : entier, valeur de j à récupérer dans data 
             *     - i : entier, valeur entre 0 et 9 pour déterminer la première case de tab où placer tabBateau (ligne)
             *     - j : entier, valeur entre 0 et 9 pour déterminer la première case de tab où placer tabBateau (colonne)
             *     - k : entier, compteur de la taille de tabBateau
             * Préconditions : dans le contexte où cette procédure sera utilisée, nb doit être inférieur à 5 car data.Length vaudra 20
             * Postconditions : les valeurs de data ont été modifiées
             */

            int choix;
            bool test;
            int indiceLigne = -1; //à récupérer, premier case du bateau
            int indiceColonne;//à récupérer, premier case du bateau
            string saisieUtilisateur;
            int i;
            int j;
            do
            {
                do
                {
                    Console.WriteLine("Horizontal/Vertical (0/1) ?");
                    saisieUtilisateur = Console.ReadLine();
                    choix = Convert.ToInt32(saisieUtilisateur);
                }
                while (saisieUtilisateur != "0" && saisieUtilisateur != "1");
                test = true;

                if (choix == 0)//place horizontal
                {
                    do
                    {
                        Console.WriteLine("Sur quelle case voulez-vous placer le début de votre bateau ? ");
                        saisieUtilisateur = Console.ReadLine();
                        indiceColonne = TraduireCharEnInt(saisieUtilisateur[0]);
                        if (saisieUtilisateur.Length == 3 && saisieUtilisateur[1] == '1' && saisieUtilisateur[2] == '0')
                        {
                            indiceLigne = 9;
                        }
                        else if (saisieUtilisateur.Length == 2)
                        {
                            indiceLigne = saisieUtilisateur[1] - 49;
                        }
                        if ((indiceColonne > 9 - tabBateau.Length) || ((indiceLigne < 0) || (indiceLigne > 9)))
                        {
                            Console.WriteLine("Attention votre bateau ne sera pas sur le plateau, veuillez recommencer.");
                        }
                    }
                    while ((indiceColonne > 9 - tabBateau.Length) || ((saisieUtilisateur != "A") && (saisieUtilisateur != "B") && (saisieUtilisateur != "C") && (saisieUtilisateur != "D") && (saisieUtilisateur != "E") && (saisieUtilisateur != "F") && (saisieUtilisateur != "G") && (saisieUtilisateur != "H") && (saisieUtilisateur != "I")) && ((indiceLigne < 0) || (indiceLigne > 9)));

                    i = indiceLigne;
                    j = indiceColonne;
                    //teste si le tableau est vide là où on veut écrire
                    int k; //compteur de la taille du tableau du bateau
                    for (k = 0; k < tabBateau.Length; k++)
                    {
                        if (tab[i, j + k] != 0)
                        {
                            test = false;
                        }
                    }

                    if (test == true)
                    {
                        for (k = 0; k < tabBateau.Length; k++)
                        {
                            tab[i, j + k] = tabBateau[k];
                        }
                    }

                }
                else// place verticalement
                {
                    do
                    {
                        Console.WriteLine("Sur quelle case voulez-vous placer le début de votre bateau ? ");
                        saisieUtilisateur = Console.ReadLine();
                        indiceColonne = TraduireCharEnInt(saisieUtilisateur[0]);
                        if (saisieUtilisateur.Length == 3 && saisieUtilisateur[1] == '1' && saisieUtilisateur[2] == '0')
                        {
                            indiceLigne = 9;
                        }
                        else if (saisieUtilisateur.Length == 2)
                        {
                            indiceLigne = saisieUtilisateur[1] - 49;
                        }
                        if (indiceLigne > 9 - tabBateau.Length)
                        {
                            Console.WriteLine("Attention votre bateau ne sera pas sur le plateau, veuillez recommencer.");
                        }
                    } while ((saisieUtilisateur != "A") && (saisieUtilisateur != "B") && (saisieUtilisateur != "C") && (saisieUtilisateur != "D") && (saisieUtilisateur != "E") && (saisieUtilisateur != "F") && (saisieUtilisateur != "G") && (saisieUtilisateur != "H") && (saisieUtilisateur != "I") && (saisieUtilisateur != "J") && (indiceLigne < 0) || (indiceLigne > 9 - tabBateau.Length));

                    i = indiceLigne;
                    j = indiceColonne;
                    //teste si le tableau est vide là où on veut écrire
                    int k; //compteur de la taille du tableau du bateau
                    for (k = 0; k < tabBateau.Length; k++)
                    {
                        if (tab[i + k, j] != 0)
                        {
                            test = false;
                            Console.WriteLine("Attention! Vous faites se chevaucher 2 bateaux ! Recommencez le placement.");
                        }
                    }

                    if (test == true)
                    {
                        for (k = 0; k < tabBateau.Length; k++)
                        {
                            tab[i + k, j] = tabBateau[k];
                        }
                    }
                }
            } while (test == false);
            //data = { tabBateau.Length, choix, indiceI; indiceJ};
            data[0 + nb * 4] = tabBateau.Length;
            data[1 + nb * 4] = choix;
            data[2 + nb * 4] = indiceLigne;
            data[3 + nb * 4] = indiceColonne;
            Console.WriteLine("\nVOTRE PLATEAU");
            DessinerPlateau(tab);
        }

        static void DessinerPlateau(char[,] tab)
        {
            /*procédure qui trace le plateau de jeu, i.e. un tableau de case 10x10
             * Argument : 
             *     - tab : tableau de char à deux dimensions, contient les éléments à afficher (IN)
             * Préconditions : aucune
             * Postconditions : aucune
             */
            Console.Write("   *  A  *  B  *  C  *  D  *  E  *  F  *  G  *  H  *  I  *  J  *\n");
            for (int i = 0; i < 10; i++)
            {
                Console.WriteLine("****************************************************************");
                Console.Write("   *     *     *     *     *     *     *     *     *     *     *\n");
                //nom des lignes
                if (i < 9)
                {
                    Console.Write((i + 1) + "  ");
                }
                else
                {
                    Console.Write((i + 1) + " ");
                }//fin nom des lignes
                for (int j = 0; j < 10; j++)
                {
                    Console.Write("*  " + tab[i, j] + "  ");
                    if (j == 9)
                    {
                        Console.Write("*");
                    }
                }
                Console.Write("\n");
                Console.Write("   *     *     *     *     *     *     *     *     *     *     *\n");
                if (i == 9)
                {
                    Console.Write("****************************************************************\n");
                }
            }
        }

        static void Tirer(int colonne, int ligne, char[,] tableau)
        {
            /*procédure qui indique l'action réalisée sur le plateau après le tir del'IA
            * Arguments : 
            *     - colonne : entier, colonne de la case où l'IA a tiré (IN)
            *     - ligne : entier, ligne de la case où l'IA a tiré (IN)
            *     - tableau : tableau de char à deux dimensions, représente le plateau où tirer (IN)
            * Préconditions : colonne et ligne doivent représenter des indices de lignes et colonnes à l'intérieur de tableau
            * Postconditions : aucune
            */

            if (tableau[ligne, colonne] == 0)
            {
                tableau[ligne, colonne] = 'O'; //raté, tir dans l'eau
                Console.WriteLine("Raté !");
            }
            else if ((tableau[ligne, colonne] == '#') || (tableau[ligne, colonne] == ' '))//cad sur un bateau
            {
                tableau[ligne, colonne] = 'X'; //touché
                Console.WriteLine("Touché !");
            }
            else if ((tableau[ligne, colonne] == 'O') || (tableau[ligne, colonne] == 'X'))
            { Console.WriteLine("Attention ! Vous aviez déjà tiré à cet endroit."); } 

        }

        static void TirerOrdi(int colonne, int ligne, char[,] tableau, ref bool touche)
        {
            /*procédure qui indique l'action réalisée sur le plateau après le tir del'IA
             * Arguments : 
             *     - colonne : entier, colonne de la case où l'IA a tiré (IN)
             *     - ligne : entier, ligne de la case où l'IA a tiré (IN)
             *     - tableau : tableau de char à deux dimensions, représente le plateau où tirer (IN)
             *     - touche : booléen, détermine si le tir à touché un bateau ou non (INOUT)
             * Préconditions : colonne et ligne doivent représenter des indices de lignes et colonnes à l'intérieur de tableau
             * Postconditions : modifie la valeur de touche
             */
            if (tableau[ligne, colonne] != '#')
            {
                tableau[ligne, colonne] = 'O'; //raté, tir dans l'eau
                Console.WriteLine("Raté !");
                touche = false;
            }
            else //cad sur un bateau
            {
                tableau[ligne, colonne] = 'X'; //touché
                Console.WriteLine("Touché !");
                touche = true;
            }

        }

        static void ChercherCible(ref int orientation, ref int pas, ref int colonne, ref int ligne, char[,] tableau, ref bool touche)
        {
            /*procédure qui cherche où sont les bateaux autour après avoir touché un bateau
             * Arguments : 
             *     - orientation : entier , direction dans laquelle l'ordi cherche sa prochaine cible (droite, gauche, bas, haut) (INOUT)
             *     - colonne : entier, colonne de la case où l'IA a tiré (INOUT)
             *     - ligne : entier, ligne de la case où l'IA a tiré (INOUT)
             *     - tableau : tableau de char à deux dimensions, représente le plateau où tirer (IN)
             *     - touche : booléen, détermine si le tir à touché un bateau ou non (INOUT)
             * Variable :
             *     - saisieColonne : charactère, lettre de la colonne où l'IA a tiré
             * Appel : 
             *     - TirerOrdi()
             *     - TraduireIntEnChar()
             * Préconditions : 
             *     - Mode de jeu IA "intelligente"
             *     - colonne et ligne doivent représenter des indices de lignes et colonnes à l'intérieur de tableau
             * Postconditions : modifie la valeur de orientation, pas, colonne, ligne, touche
             */
            char saisieColonne;
            if (colonne + pas <= 9 && orientation == 0)//cherche vers la droite
            {
                if (tableau[ligne, colonne + pas] == 'O' || tableau[ligne, colonne + pas] == 'X')
                {
                    orientation++;
                    pas = 1;
                }
                else
                {
                    TirerOrdi(colonne + pas, ligne, tableau, ref touche);
                    saisieColonne = TraduireIntEnChar(colonne + pas);
                    Console.WriteLine("L'ordi a tiré en : " + saisieColonne + (ligne + 1));
                }
            }
            if (colonne + pas >= 9 && orientation == 0)//cherche vers la gauche si bord du plateau
            {
                if (tableau[ligne, colonne - pas] == 'O' || tableau[ligne, colonne - pas] == 'X')
                {
                    orientation++;
                    pas = 1;
                }
                else
                {
                    TirerOrdi(colonne - pas, ligne, tableau, ref touche);
                    saisieColonne = TraduireIntEnChar(colonne - pas);
                    Console.WriteLine("L'ordi a tiré en : " + saisieColonne + (ligne + 1));
                }
            }
            if (colonne - pas >= 0 && orientation == 1)//cherche vers la gauche
            {
                if (tableau[ligne, colonne - pas] == 'O' || tableau[ligne, colonne - pas] == 'X')
                {
                    orientation++;
                    pas = 1;
                }
                else
                {
                    TirerOrdi(colonne - pas, ligne, tableau, ref touche);
                    saisieColonne = TraduireIntEnChar(colonne - pas);
                    Console.WriteLine("L'ordi a tiré en : " + saisieColonne + (ligne + 1));

                }
            }
            if (colonne <= 0 && orientation == 1)//cherche vers la droite si bord du plateau
            {
                if (tableau[ligne, colonne + pas] == 'O' || tableau[ligne, colonne + pas] == 'X')
                {
                    orientation++;
                    pas = 1;
                }
                else
                {
                    TirerOrdi(colonne + pas, ligne, tableau, ref touche);
                    saisieColonne = TraduireIntEnChar(colonne + pas);
                    Console.WriteLine("L'ordi a tiré en : " + saisieColonne + (ligne + 1));
                }
            }
            if (ligne + pas <= 9 && orientation == 2)//cherche vers le bas
            {
                if (tableau[ligne + pas, colonne] == 'O' || tableau[ligne + pas, colonne] == 'X')
                {
                    orientation++;
                    pas = 1;
                }
                else
                {
                    TirerOrdi(colonne, ligne + pas, tableau, ref touche);
                    saisieColonne = TraduireIntEnChar(colonne);
                    Console.WriteLine("L'ordi a tiré en : " + saisieColonne + (ligne + pas + 1));
                }
            }
            if (ligne >= 9 && orientation == 2)//cherche vers le haut si bord du plateau
            {
                if (tableau[ligne - pas, colonne] == 'O' || tableau[ligne - pas, colonne] == 'X')
                {
                    orientation++;
                    pas = 1;
                }
                else
                {
                    TirerOrdi(colonne, ligne - pas, tableau, ref touche);
                    saisieColonne = TraduireIntEnChar(colonne);
                    Console.WriteLine("L'ordi a tiré en : " + saisieColonne + (ligne - pas + 1));
                }
            }
            if (ligne - pas >= 0 && orientation == 3)//cherche vers le bas
            {
                if (tableau[ligne - pas, colonne] == 'O' || tableau[ligne - pas, colonne] == 'X')
                {
                    orientation++;
                    pas = 1;
                }
                else
                {
                    TirerOrdi(colonne, ligne - pas, tableau, ref touche);
                    saisieColonne = TraduireIntEnChar(colonne);
                    Console.WriteLine("L'ordi a tiré en : " + saisieColonne + (ligne - pas + 1));
                }
            }
            if (ligne <= 0 && orientation == 3)//cherche vers le bas si bord plateau
            {
                if (tableau[ligne + pas, colonne] == 'O' || tableau[ligne + pas, colonne] == 'X')
                {
                    orientation++;
                    pas = 1;
                }
                else
                {
                    TirerOrdi(colonne, ligne + pas, tableau, ref touche);
                    saisieColonne = TraduireIntEnChar(colonne);
                    Console.WriteLine("L'ordi a tiré en : " + saisieColonne + (ligne + pas + 1));
                }
            }
        }

        static void DefinirTableau(char[] tabBateau, int a, int[] donnees, char[,] tab)
        {
            /*procédure qui met à jour tabBateau  
             * Arguments : 
             *     - tabBateau : tableau de char à une dimension, bateau à tester (IN)
             *     - a : entier, numéro du bateau correspondant à tabBateau donc du rang à partir duquel il faut lire dans donnees (IN)
             *     - donnees : tableau d'entiers à une dimension, contient les donnees relatives à tabBateau (IN)
             *     - tab : tableau de char à deux dimensions, plateau de jeu (IN)
             * Préconditions : a compris entre 0 et 4 inclus
             * Postconditions : aucune 
             */
            if (donnees[1 + a * 4] == 0)
            {
                for (int k = 0; k < tabBateau.Length; k++)
                {
                    tabBateau[k] = tab[donnees[2 + a * 4], (donnees[3 + a * 4] + k)];
                }
            }
            else
            {
                for (int k = 0; k < tabBateau.Length; k++)
                {
                    tabBateau[k] = tab[(donnees[2 + a * 4] + k), donnees[3 + a * 4]];
                }
            }

        }

        static void TesterToucheCoule(char[] tabBateau, ref int nbBateauCoulé, ref bool coulé)

        {
            /*procédure qui teste si le bateau correspondant à tabBateau est touché coulé.
             * Arguments : 
             *     - tabBateau : tableau de char à une dimension, bateau à tester (IN)
             *     - nbBateauCoulé : entier, compte le nombre de bateau coulé par le joueur (INOUT)
             *     - coulé : booléen, indique si le bateau est coulé (INOUT)
             * Variables : 
             *     - testBateau : booléen, teste si toutes les cases de tabBateau sont touchées
             * Préconditions : aucune
             * Postconditions : modifie les valeurs de nbBateauCoulé et coulé
             */
            bool testBateau = true;
            for (int k = 0; k < tabBateau.Length; k++)
            {
                if (tabBateau[k] != 'X')
                {
                    testBateau = false;
                }
            }
            if (testBateau == true)
            {
                Console.WriteLine("COULE !");
                nbBateauCoulé++;
                coulé = true;
            }
        }

        static void FinirJeu()
        {
            /*procédure qui affiche le texte de fin de jeu.
             * Préconditions : aucune
             * Postconditions : aucune
             */

            Console.WriteLine("Merci d'avoir joué ! Nous espérons vous revoir bientôt !");
            Console.WriteLine("Ce programme a été développé par Antoine BOUQUET et Alice CANTAGREL dans le cadre du projet informatique IPROG de première année à l'ENSC.");
        }

        static void Quitter(ref char[,] tab, ref char[,] tab2, ref int[] donnees1, ref int[] donnees2, ref bool bool1, ref bool bool2)
        {
            /*procédure qui s'occupe de quitter la partie en cours.
             * Arguments : 
             *     - tab : tableau de char à deux dimensions, plateau de jeu (INOUT)
             *     - tab2 : tableau de char à deux dimensions, plateau de jeu (INOUT)
             *     - donnees1 : tableau d'entier, données de jeu (INOUT)
             *     - donnees2 : tableau d'entier, données de jeu (INOUT)
             *     - bool1 : booléen, réponse du joueur pour le mode de jeu (INOUT)
             *     - bool2 : booléen, réponse du joueur pour le niveau de l'ordi (INOUT)
             * Variable :
             *     - answer : string, correspond à la réponse que le joueur aura rentrée
             * Appel :
             *     - Sauvegarder(); 
             * Préconditions : aucune
             * Postconditions : retourne un entier
             */
            string answer = "a";
            while ((answer != "n") && (answer != "o"))
            {
                Console.WriteLine("Voulez vous vraiment quitter la partie ?");
                answer = Console.ReadLine();
                if (answer == "o")
                {
                    answer = "a";
                    while ((answer != "n") && (answer != "o"))
                    {
                        Console.WriteLine("Voulez vous sauvegarder la partie ?");
                        answer = Console.ReadLine();
                        if (answer == "o")
                        {
                            Sauvegarder(ref tab, ref tab2, ref donnees1, ref donnees2, ref bool1, ref bool2);

                        }
                    }
                }
            }
        }

        static void Sauvegarder(ref char[,] tab, ref char[,] tab2, ref int[] donnees1, ref int[] donnees2, ref bool bool1, ref bool bool2)
        {
            /* procédure qui permet de sauvegarder une partie 
             * Arguments :
             *     - tab : tableau de char à deux dimensions, plateau de jeu (INOUT)
             *     - tab2 : tableau de char à deux dimensions, plateau de jeu (INOUT)
             *     - donnees1 : tableau d'entier, données de jeu (INOUT)
             *     - donnees2 : tableau d'entier, données de jeu (INOUT)
             *     - bool1 : booléen, réponse du joueur pour le mode de jeu (INOUT)
             *     - bool2 : booléen, réponse du joueur pour le niveau de l'ordi (INOUT)
             * Variables :
             *     - nom : string, nom du fichier
             *     - path : string, chemin du fichier
             *     - format : string, extension du fichier
             *     - pathComplet : string, chemin complet du fichier
             *     - date : string, date de sauvegarde
             *     - presentation : string, texte de présentation à écrire dans le fichier
             * Préconditions : aucune
             * Postconditions : créer un fichier non vide
             */

            Console.WriteLine("Sous quel nom voulez-vous enregistrer votre partie ?");
            string nom = Console.ReadLine();
            string path;
            do
            {
                Console.WriteLine("Veuillez entrer le chemin du dossier où vous voulez enregistrer votre partie.");
                Console.WriteLine("Attention ! Ce chemin doit commencer par votre espace de stockage et aller \njusqu'au dossier contenant le fichier à ouvrir.\nChaque transition entre dossiers doit être notée par \\\\");
                path = Console.ReadLine();
            } while (System.IO.Directory.Exists(path) == false);

            string format = ".txt";
            string pathComplet = path + nom + format;
            System.IO.File.WriteAllText(@pathComplet, "");// crée le fichier et enregistre le deuxième argument dedans

            using (System.IO.StreamWriter file = new System.IO.StreamWriter(@pathComplet, true))
            {
                foreach (char line in tab)
                {
                    file.WriteLine("{0} ", line);
                }
                foreach (char line in tab2)
                {
                    file.WriteLine("{0} ", line);
                }
                foreach (int line in donnees1)
                {
                    file.WriteLine("{0} ", line);
                }
                foreach (int line in donnees2)
                {
                    file.WriteLine("{0} ", line);
                }
                file.WriteLine("{0}", bool1);
                file.WriteLine("{0}", bool2);

            }

        }

        static void ReprendrePartie(ref bool bool1, ref char[,] tab, ref char[,] tab2, ref int[] donnees1, ref int[] donnees2, ref bool bool2, ref bool bool3)
        {
            /* procédure qui premet de charger une partie
             * Arguments :
             *     - bool1 : booléen, réponse du joueur pour le chargement de partie (INOUT)
             *     - tab : tableau de char à deux dimensions, plateau de jeu (INOUT)
             *     - tab2 : tableau de char à deux dimensions, plateau de jeu (INOUT)
             *     - donnees1 : tableau d'entier, données de jeu (INOUT)
             *     - donnees2 : tableau d'entier, données de jeu (INOUT)
             *     - bool2 : booléen, réponse du joueur pour le mode de jeu (INOUT)
             *     - bool3 : booléen, réponse du joueur pour le niveau de l'ordi (INOUT)
             * Variables :
             *     - reponse : string, reponse à une question
             *     - reponse2 : string, reponse à une question
             *     - nom : string, nom du fichier
             *     - path : string, chemin du fichier
             *     - format : string, extension du fichier
             *     - pathComplet : string, chemin complet du fichier
             *     - date : string, date de sauvegarde
             *     - presentation : string, texte de présentation à écrire dans le fichier
             * Préconditions : le fichier à ouvrir doit exister et être non vide
             * Postconditions :aucune
             */
            string reponse = "a";
            string reponse2 = "a";
            string nom;
            string path = "\\Projet Info-Bataille Navale\\";
            string format = ".txt";

            while ((reponse != "o") && (reponse != "n"))
            {
                Console.WriteLine("Voulez-vous reprendre une partie en cours ? (o/n)");
                reponse = Console.ReadLine();
            }
            if (reponse == "o")
            {
                bool1 = true;
                //"E:\\Documents\\ENSC\\INFO\\Projet Info-Bataille Navale\\";//"C:\\Users\\Antoine\\Documents\\ENSC\\1A\\Info\\Bouquet_Cantagrel\\";
                Console.WriteLine("Veuillez entrer le chemin du dossier qui contient la partie à charger.");
                Console.WriteLine("Attention ! Ce chemin doit commencer par votre espace de stockage et aller \njusqu'au dossier contenant le fichier à ouvrir.\nChaque transition entre dossiers doit être notée par \\\\");
                path = Console.ReadLine();
                Console.WriteLine("Veuillez entrer le nom de la partie à charger.");
                nom = Console.ReadLine();
                string pathComplet = path + nom + format;
                while (System.IO.File.Exists(pathComplet) == false)
                {
                    Console.WriteLine("Erreur ! Le fichier que vous essayez d'ouvrir n'existe pas.\nVeuillez rentrer à nouveau un nom de fichier.");
                    nom = Console.ReadLine();
                    do
                    {
                        Console.WriteLine("Voulez-vous entrer un nouveau chemin d'accès ? (o/n)");
                        reponse2 = Console.ReadLine();
                    } while ((reponse2 != "o") && (reponse2 != "n"));
                    if (reponse2 == "o")
                    {
                        Console.WriteLine("Veuillez rentrer à nouveau le chemin d'accès au dossier contenant la partie à charger");
                        path = Console.ReadLine();
                        pathComplet = path + nom + format;
                    }
                }
                if (System.IO.File.Exists(pathComplet))//vérifie l'existence du fichier
                {
                    //lecture
                    string[] lines = System.IO.File.ReadAllLines(pathComplet);
                    char[] tableau = new char[100];
                    char[] tableau2 = new char[100];

                    int k = 0;
                    foreach (string line in lines)
                    {
                        if (k < 100)
                        {
                            tableau[k] = line[0];

                        }

                        if (k >= 100 && k < 200)
                        {
                            tableau2[k - 100] = line[0];

                        }

                        if (k > 199 && k < 220)
                        {
                            donnees1[k - 200] = Convert.ToInt32(line[0]) - 48;

                        }
                        if (k > 219 && k < 240)
                        {
                            donnees2[k - 220] = Convert.ToInt32(line[0]) - 48;

                        }
                        k++;
                        bool2 = Convert.ToBoolean(lines[240]);
                        bool3 = Convert.ToBoolean(lines[241]);
                    }
                    k = 0;
                    for (int i = 0; i < 10; i++)
                    {
                        for (int j = 0; j < 10; j++)
                        {
                            if (k < 100)
                            {
                                tab[i, j] = tableau[k];
                                k++;

                            }
                        }
                    }
                    for (int i = 0; i < 10; i++)
                    {
                        for (int j = 0; j < 10; j++)
                        {
                            if (k < 200)
                            {
                                tab2[i, j] = tableau2[k - 100];
                                k++;
                            }
                        }
                    }
                }



            }
        }

        static int TraduireCharEnInt(char saisieColonne)
        {
            /*fonction qui traduit les réponses en Char du joueur en entier.
             * Argument : 
             *     - saisieColonne : string, correspond à la réponse que le joueur aura rentrée (IN)
             * Variable :
             *     - colonne : entier, correspond au numéro de la colonne du plateau de jeu 
             * Préconditions : aucune
             * Postconditions : retourne un entier
             */
            int colonne = -1;
            if (saisieColonne == 'A')
            {
                colonne = 0;
            }
            else if (saisieColonne == 'B')
            {
                colonne = 1;
            }
            else if (saisieColonne == 'C')
            {
                colonne = 2;
            }
            else if (saisieColonne == 'D')
            {
                colonne = 3;
            }
            else if (saisieColonne == 'E')
            {
                colonne = 4;
            }
            else if (saisieColonne == 'F')
            {
                colonne = 5;
            }
            else if (saisieColonne == 'G')
            {
                colonne = 6;
            }
            else if (saisieColonne == 'H')
            {
                colonne = 7;
            }
            else if (saisieColonne == 'I')
            {
                colonne = 8;
            }
            else if (saisieColonne == 'J')
            {
                colonne = 9;
            }
            return colonne;
        }

        static char TraduireIntEnChar(int colonne)
        {
            /*fonction qui traduit le numéro de colonne choisie par l'IA en sa lettre sur le plateau.
             * Argument : 
             *     - colonne : int, correspond au numéro de la colonne choisie par l'IA (IN)
             * Variable :
             *     - saisieColonne : char, correspond à la lettre du plateau de jeu équivalente au numéro de la colonne du tableau du plateau de jeu
             * Préconditions : aucune
             * Postconditions : retourne un char
             */
            char saisieColonne = 'W';
            if (colonne == 0)
            {
                saisieColonne = 'A';
            }
            if (colonne == 1)
            {
                saisieColonne = 'B';
            }
            if (colonne == 2)
            {
                saisieColonne = 'C';
            }
            if (colonne == 3)
            {
                saisieColonne = 'D';
            }
            if (colonne == 4)
            {
                saisieColonne = 'E';
            }
            if (colonne == 5)
            {
                saisieColonne = 'F';
            }
            if (colonne == 6)
            {
                saisieColonne = 'G';
            }
            if (colonne == 7)
            {
                saisieColonne = 'H';
            }
            if (colonne == 8)
            {
                saisieColonne = 'I';
            }
            if (colonne == 9)
            {
                saisieColonne = 'J';
            }
            return saisieColonne;
        }

        static int LirePlateau(char[,] tab)
        {
            /*fonction qui lit le plateau de jeu pour renvoyer le nombre de dièses qu'il contient.
             * Argument : 
             *     - tab : tableau de char à deux dimensions, tableau à lire (IN)
             * Variable : 
             *     - nbDiese : entier, compteur du nombre de dièses présent dans tab 
             * Préconditions : aucune
             * Postconditions : retourne un entier
             * NB : cette fonction a été utilisée afin d'effectuer des tests au cours de notre développement pour vérifier que le bon nombre de cases du plateau était occupées par des bateaux 
             * cad 17 (= 5 + 4 + 3 + 3 + 2)
             */
            int nbDiese = 0;
            for (int i = 0; i < 10; i++)
            {
                for (int j = 0; j < 10; j++)
                {

                    if (tab[i, j] == '#')
                    {
                        nbDiese++;
                        /*donnees[k, 0] = i;
                        donnees[k, 1] = j;*/
                    }
                }
            }
            return nbDiese;
        }

        static void Main(string[] args)
        {
            Random r = new Random();
            //interface et choix de jeu
            bool modeJeu = true; //par défaut le mode salvo est lancé
            bool niveauOrdi = false;//par défaut le niveau facile est lancé
            bool chargerPartie = false;
            bool placerBateau = false;//par defaut placement aléatoire
            char[,] tabj1 = new char[10, 10];
            char[,] tabOrdi = new char[10, 10];
            int nbBateauCoulé = 0;
            int nbBateauCouléOrdi = 0;
            int victoire = -1;
            int nbTours = 0;
            int[] donnees = new int[20];
            int[] donneesOrdi = new int[20];
            bool touche = false;

            //booléen controle bateau coulé
            bool couléPA = false;
            bool couléCuir = false;
            bool couléSM = false;
            bool couléCrois = false;
            bool couléCT = false;
            bool couléPAOrdi = false;
            bool couléCuirOrdi = false;
            bool couléSMOrdi = false;
            bool couléCroisOrdi = false;
            bool couléCTOrdi = false;

            DebuterPartie(ref modeJeu, ref niveauOrdi, ref chargerPartie, ref placerBateau, ref tabj1, ref tabOrdi, ref donnees, ref donneesOrdi); //faut placer les arguments en références pour qu'ils soient effectivement modifiés

            //Création des bateaux
            char[] PA = { '#', '#', '#', '#', '#' }; //PorteAvion
            char[] Cuir = { '#', '#', '#', '#' }; //Cuirassé
            char[] SM = { '#', '#', '#' }; //SousMarin
            char[] Crois = { '#', '#', '#' }; //Croiseur
            char[] CT = { '#', '#' };//ContreTorpilleur
            char[] PAOrdi = { ' ', ' ', ' ', ' ', ' ' }; //PorteAvion
            char[] CuirOrdi = { ' ', ' ', ' ', ' ' }; //Cuirassé
            char[] SMOrdi = { ' ', ' ', ' ' }; //SousMarin
            char[] CroisOrdi = { ' ', ' ', ' ' }; //Croiseur
            char[] CTOrdi = { ' ', ' ' };//ContreTorpilleur
            if (chargerPartie == false)//pas de chargement de partie
            {
                //Début de partie : choix du placement des bateaux sur le plateaux du joueur
                if (placerBateau == true)
                {
                    Console.WriteLine("Placement de votre Porte-avion :");
                    PlacerBateau(tabj1, PA, 0, ref donnees);
                    Console.WriteLine("Placement de votre Cuirassé :");
                    PlacerBateau(tabj1, Cuir, 1, ref donnees);
                    Console.WriteLine("Placement de votre Sous-marin :");
                    PlacerBateau(tabj1, SM, 2, ref donnees);
                    Console.WriteLine("Placement de votre Croiseur :");
                    PlacerBateau(tabj1, Crois, 3, ref donnees);
                    Console.WriteLine("Placement de votre Contre-torpilleur :");
                    PlacerBateau(tabj1, CT, 4, ref donnees);

                }
                else
                {
                    string reponse = "a";
                    Console.WriteLine("\nVOTRE PLATEAU");
                    InitialiserPlateau(tabj1, PA, 0, ref donnees);
                    InitialiserPlateau(tabj1, Cuir, 1, ref donnees);
                    InitialiserPlateau(tabj1, SM, 2, ref donnees);
                    InitialiserPlateau(tabj1, Crois, 3, ref donnees);
                    InitialiserPlateau(tabj1, CT, 4, ref donnees);
                    DessinerPlateau(tabj1);
                    while ((reponse != "o") && (reponse != "n"))
                    {
                        Console.WriteLine("Le placement des bateaux vous convient-il ? (o/n)");
                        reponse = Console.ReadLine();

                        while (reponse == "n")
                        {
                            tabj1 = new char[10, 10]; //réinitialiser tabj1 
                            InitialiserPlateau(tabj1, PA, 0, ref donnees);
                            InitialiserPlateau(tabj1, Cuir, 1, ref donnees);
                            InitialiserPlateau(tabj1, SM, 2, ref donnees);
                            InitialiserPlateau(tabj1, Crois, 3, ref donnees);
                            InitialiserPlateau(tabj1, CT, 4, ref donnees);
                            DessinerPlateau(tabj1);
                            Console.WriteLine("Le placement des bateaux vous convient-il ? (o/n)");
                            reponse = Console.ReadLine();
                        }
                    }
                }
                Console.WriteLine("\n \n");


                //Initialisation du plateau de l'IA
                InitialiserPlateau(tabOrdi, PAOrdi, 0, ref donneesOrdi);
                InitialiserPlateau(tabOrdi, CuirOrdi, 1, ref donneesOrdi);
                InitialiserPlateau(tabOrdi, SMOrdi, 2, ref donneesOrdi);
                InitialiserPlateau(tabOrdi, CroisOrdi, 3, ref donneesOrdi);
                InitialiserPlateau(tabOrdi, CTOrdi, 4, ref donneesOrdi);

            }
            else//chargement d'une ancienne partie
            {
                //mise à jour des bateaux de l'ordi et du nombre de bateaux coulé par le joueur
                DefinirTableau(PAOrdi, 0, donneesOrdi, tabOrdi);
                DefinirTableau(CuirOrdi, 1, donneesOrdi, tabOrdi);
                DefinirTableau(SMOrdi, 2, donneesOrdi, tabOrdi);
                DefinirTableau(CroisOrdi, 3, donneesOrdi, tabOrdi);
                DefinirTableau(CTOrdi, 4, donneesOrdi, tabOrdi);
                if (couléPAOrdi == false)
                {
                    TesterToucheCoule(PAOrdi, ref nbBateauCouléOrdi, ref couléPAOrdi);
                }
                if (couléCuirOrdi == false)
                {
                    TesterToucheCoule(CuirOrdi, ref nbBateauCouléOrdi, ref couléCuirOrdi);
                }
                if (couléSMOrdi == false)
                {
                    TesterToucheCoule(SMOrdi, ref nbBateauCouléOrdi, ref couléSMOrdi);
                }
                if (couléCroisOrdi == false)
                {
                    TesterToucheCoule(CroisOrdi, ref nbBateauCouléOrdi, ref couléCroisOrdi);
                }
                if (couléCTOrdi == false)
                {
                    TesterToucheCoule(CTOrdi, ref nbBateauCouléOrdi, ref couléCTOrdi);
                }
                //mise à jour des bateaux du joueur et du nombre de bateaux coulé par l'ordi 
                DefinirTableau(PA, 0, donnees, tabj1);
                DefinirTableau(Cuir, 1, donnees, tabj1);
                DefinirTableau(SM, 2, donnees, tabj1);
                DefinirTableau(Crois, 3, donnees, tabj1);
                DefinirTableau(CT, 4, donnees, tabj1);
                if (couléPA == false)
                {
                    TesterToucheCoule(PA, ref nbBateauCoulé, ref couléPA);
                }
                if (couléCuir == false)
                {
                    TesterToucheCoule(Cuir, ref nbBateauCoulé, ref couléCuir);
                }
                if (couléSM == false)
                {
                    TesterToucheCoule(SM, ref nbBateauCoulé, ref couléSM);
                }
                if (couléCrois == false)
                {

                    TesterToucheCoule(Crois, ref nbBateauCoulé, ref couléCrois);
                }
                if (couléCT == false)
                {
                    TesterToucheCoule(CT, ref nbBateauCoulé, ref couléCT);
                }
                Console.WriteLine("Voici votre plateau :");
                DessinerPlateau(tabj1);
                Console.WriteLine("Voici le plateau de l'ordi et les tirs que vous aviez effectué :");
                DessinerPlateau(tabOrdi);
            }

            //Déroulement de la partie
            int pas = 0;
            int orientation = 0;
            int colonneOrdi = 12;
            int ligneOrdi = 12;
            string saisieUtilisateur;
            char saisieColonne;
            int colonne = -1;
            int ligne = -1;
            do
            {
                while (victoire != 0 || victoire != 1)
                {
                    if (modeJeu == true) //mode jeu salvo
                    {
                        int nbTirDispoOrdi;
                        int nbTirDispo = 5 - nbBateauCouléOrdi;

                        nbTours++;
                        Console.WriteLine("###### TOUR {0} ######", nbTours);
                        Console.WriteLine("C'est votre tour. \nVous avez le droit à {0} tir(s).", nbTirDispo);
                        for (int nbTir = 0; nbTir < nbTirDispo; nbTir++) //tir joueur
                        {
                            Console.WriteLine("C'est votre tir n°{0}.", (nbTir + 1));
                            if (niveauOrdi == false)//niveau facile : on ne peut pas tirer deux fois sur la meme case 
                            {
                                do
                                {
                                    Console.WriteLine("Sur quelle case voulez-vous tirer ? ");
                                    saisieUtilisateur = Console.ReadLine();
                                    if (saisieUtilisateur == "ENSC")
                                    {
                                        Console.WriteLine(" _____   __   __  _____   ______  ");
                                        Console.WriteLine("| ____| |  \\ | | / ___/  / ____|");
                                        Console.WriteLine("| |__   |   \\| | | |___  | |");
                                        Console.WriteLine("|  __|  | |\\   | \\____ \\ | |");
                                        Console.WriteLine("| |___  | | \\  |  ___| | | |___");
                                        Console.WriteLine("|_____| |_|  \\_| /_____/ \\_____|");
                                    }
                                    saisieColonne = saisieUtilisateur[0];
                                    colonne = TraduireCharEnInt(saisieColonne);
                                    if (saisieUtilisateur.Length == 3 && saisieUtilisateur[1] == '1' && saisieUtilisateur[2] == '0')
                                    {
                                        ligne = 9;
                                    }
                                    else if (saisieUtilisateur.Length == 2)
                                    {
                                        ligne = saisieUtilisateur[1] - 49;
                                    }
                                    if (saisieColonne == 'Q')

                                    {
                                        Quitter(ref tabj1, ref tabOrdi, ref donnees, ref donneesOrdi, ref modeJeu, ref niveauOrdi);
                                        Environment.Exit(0);
                                    }

                                    else if (((saisieColonne != 'A') && (saisieColonne != 'B') && (saisieColonne != 'C') && (saisieColonne != 'D') && (saisieColonne != 'E') && (saisieColonne != 'F') && (saisieColonne != 'G') && (saisieColonne != 'H') && (saisieColonne != 'I') && (saisieColonne != 'J')) || (saisieUtilisateur.Length >= 3 && (saisieUtilisateur[2] > 48)))
                                    {
                                        Console.WriteLine("Veuillez tirer sur le plateau ou vérifiez que votre saisie est correcte (casse, nombre).");
                                    }
                                    else if (tabOrdi[ligne, colonne] == 'O' || tabOrdi[ligne, colonne] == 'X')
                                    {
                                        Console.WriteLine("Vous aviez dejà tiré à cette endroit! Réessayez");
                                    }
                                }
                                while (((saisieColonne != 'A') && (saisieColonne != 'B') && (saisieColonne != 'C') && (saisieColonne != 'D') && (saisieColonne != 'E') && (saisieColonne != 'F') && (saisieColonne != 'G') && (saisieColonne != 'H') && (saisieColonne != 'I') && (saisieColonne != 'J')) || ((saisieUtilisateur.Length >= 3 && (saisieUtilisateur[2] > 48)) || ((tabOrdi[ligne, colonne] == 'O' || tabOrdi[ligne, colonne] == 'X'))));
                            }
                            else//niveau avancé : on peut tirer 2 fois sur la même case
                            {
                                do
                                {
                                    Console.WriteLine("Sur quelle case voulez-vous tirer ? ");
                                    saisieUtilisateur = Console.ReadLine();
                                    if (saisieUtilisateur == "ENSC")
                                    {
                                        Console.WriteLine(" _____   __   __  _____   ______  ");
                                        Console.WriteLine("| ____| |  \\ | | / ___/  / ____|");
                                        Console.WriteLine("| |__   |   \\| | | |___  | |");
                                        Console.WriteLine("|  __|  | |\\   | \\____ \\ | |");
                                        Console.WriteLine("| |___  | | \\  |  ___| | | |___");
                                        Console.WriteLine("|_____| |_|  \\_| /_____/ \\_____|");
                                    }
                                    saisieColonne = saisieUtilisateur[0];
                                    colonne = TraduireCharEnInt(saisieColonne);
                                    if (saisieUtilisateur.Length == 3 && saisieUtilisateur[1] == '1' && saisieUtilisateur[2] == '0')
                                    {
                                        ligne = 9;
                                    }
                                    else if (saisieUtilisateur.Length == 2)
                                    {
                                        ligne = saisieUtilisateur[1] - 49;
                                    }
                                    if (saisieColonne == 'Q')

                                    {
                                        Quitter(ref tabj1, ref tabOrdi, ref donnees, ref donneesOrdi, ref modeJeu, ref niveauOrdi);
                                        Environment.Exit(0);
                                    }

                                    else if ((saisieColonne != 'A') && (saisieColonne != 'B') && (saisieColonne != 'C') && (saisieColonne != 'D') && (saisieColonne != 'E') && (saisieColonne != 'F') && (saisieColonne != 'G') && (saisieColonne != 'H') && (saisieColonne != 'I') && (saisieColonne != 'J') || ((saisieUtilisateur.Length >= 3 && (saisieUtilisateur[2] > 48))))
                                    {
                                        Console.WriteLine("Veuillez tirer sur le plateau ou vérifiez que votre saisie est correcte (casse, nombre).");
                                    }

                                }
                                while ((saisieColonne != 'A') && (saisieColonne != 'B') && (saisieColonne != 'C') && (saisieColonne != 'D') && (saisieColonne != 'E') && (saisieColonne != 'F') && (saisieColonne != 'G') && (saisieColonne != 'H') && (saisieColonne != 'I') && (saisieColonne != 'J') || ((saisieUtilisateur.Length >= 3 && (saisieUtilisateur[2] > 48))));
                            }
                            Tirer(colonne, ligne, tabOrdi);

                            DefinirTableau(PAOrdi, 0, donneesOrdi, tabOrdi);
                            DefinirTableau(CuirOrdi, 1, donneesOrdi, tabOrdi);
                            DefinirTableau(SMOrdi, 2, donneesOrdi, tabOrdi);
                            DefinirTableau(CroisOrdi, 3, donneesOrdi, tabOrdi);
                            DefinirTableau(CTOrdi, 4, donneesOrdi, tabOrdi);

                            if (couléPAOrdi == false)
                            {
                                TesterToucheCoule(PAOrdi, ref nbBateauCouléOrdi, ref couléPAOrdi);
                            }
                            if (couléCuirOrdi == false)
                            {
                                TesterToucheCoule(CuirOrdi, ref nbBateauCouléOrdi, ref couléCuirOrdi);
                            }
                            if (couléSMOrdi == false)
                            {
                                TesterToucheCoule(SMOrdi, ref nbBateauCouléOrdi, ref couléSMOrdi);
                            }
                            if (couléCroisOrdi == false)
                            {
                                TesterToucheCoule(CroisOrdi, ref nbBateauCouléOrdi, ref couléCroisOrdi);
                            }
                            if (couléCTOrdi == false)
                            {
                                TesterToucheCoule(CTOrdi, ref nbBateauCouléOrdi, ref couléCTOrdi);
                            }
                            Console.WriteLine("Plateau de l'adversaire");
                            DessinerPlateau(tabOrdi);
                            Console.WriteLine("\nAppuyez sur une touche pour continuer.");
                            Console.ReadKey();
                        }

                        //tour de l'IA
                        nbTirDispoOrdi = 5 - nbBateauCoulé;
                        Console.WriteLine("C'est le tour de l'ordi. \nIl a le droit à {0} tir(s).", nbTirDispoOrdi);

                        for (int nbTir = 0; nbTir < nbTirDispoOrdi; nbTir++)
                        {
                            char saisieColonneOrdi = 'W';
                            if (niveauOrdi == false)//niveau ordi facile
                            {
                                do
                                {
                                    colonneOrdi = r.Next(0, 10);
                                    ligneOrdi = r.Next(0, 10);
                                    saisieColonneOrdi = TraduireIntEnChar(colonneOrdi);

                                }
                                while (tabj1[ligneOrdi, colonneOrdi] == 'O' || tabj1[ligneOrdi, colonneOrdi] == 'X');

                                Console.WriteLine("L'ordi a tiré en " + saisieColonneOrdi + (ligneOrdi + 1));
                                Tirer(colonneOrdi, ligneOrdi, tabj1);
                            }
                            else //nivOrdi == true, cad l'IA est intelligente
                            {
                                if (pas == 0)//si l'ordi n'a pas de cible en mémoire
                                {
                                    do
                                    {
                                        colonneOrdi = r.Next(0, 10);
                                        ligneOrdi = r.Next(0, 10);
                                        saisieColonneOrdi = TraduireIntEnChar(colonneOrdi);
                                    }
                                    while (tabj1[ligneOrdi, colonneOrdi] == 'O' || tabj1[ligneOrdi, colonneOrdi] == 'X');
                                    TirerOrdi(colonneOrdi, ligneOrdi, tabj1, ref touche);
                                    Console.WriteLine("L'ordi a tiré en : " + saisieColonneOrdi + (ligneOrdi + 1));
                                    if (touche == true)
                                    {
                                        pas++;
                                    }
                                }
                                else// si l'ordi a une cible en mémoire
                                {

                                    ChercherCible(ref orientation, ref pas, ref colonneOrdi, ref ligneOrdi, tabj1, ref touche);
                                    /*Verifications :
                                    Console.WriteLine(touche);
                                    Console.WriteLine("orientation=" + orientation);
                                    Console.WriteLine("pas :" + pas);*/
                                    if (touche == false)
                                    {
                                        orientation = orientation + 1;
                                        pas = 1;
                                    }
                                    else
                                    {
                                        pas++;
                                    }
                                    if (pas == 5)
                                    {

                                        orientation++;
                                        pas = 1;
                                    }
                                    if (orientation == 4)
                                    {
                                        pas = 0;
                                        orientation = 0;
                                    }
                                }
                            }
                            DefinirTableau(PA, 0, donnees, tabj1);
                            DefinirTableau(Cuir, 1, donnees, tabj1);
                            DefinirTableau(SM, 2, donnees, tabj1);
                            DefinirTableau(Crois, 3, donnees, tabj1);
                            DefinirTableau(CT, 4, donnees, tabj1);
                            if (couléPA == false)
                            {
                                TesterToucheCoule(PA, ref nbBateauCoulé, ref couléPA);
                                if (couléPA == true)
                                {
                                    pas = 0;
                                    orientation = 0;
                                }
                            }
                            if (couléCuir == false)
                            {
                                TesterToucheCoule(Cuir, ref nbBateauCoulé, ref couléCuir);
                                if (couléCuir == true)
                                {
                                    pas = 0;
                                    orientation = 0;
                                }
                            }
                            if (couléSM == false)
                            {

                                TesterToucheCoule(SM, ref nbBateauCoulé, ref couléSM);
                                if (couléSM == true)
                                {
                                    pas = 0;
                                    orientation = 0;
                                }
                            }
                            if (couléCrois == false)
                            {

                                TesterToucheCoule(Crois, ref nbBateauCoulé, ref couléCrois);
                                if (couléCrois == true)
                                {
                                    pas = 0;
                                    orientation = 0;
                                }
                            }
                            if (couléCT == false)
                            {

                                TesterToucheCoule(CT, ref nbBateauCoulé, ref couléCT);
                                if (couléCT == true)
                                {
                                    pas = 0;
                                    orientation = 0;
                                }
                            }
                            DessinerPlateau(tabj1);
                            Console.ReadKey();
                        }
                        DessinerPlateau(tabOrdi);
                        Console.WriteLine("Vous avez coulé {0} bateau(x).", nbBateauCouléOrdi);
                        if ((couléPAOrdi == true) && (couléCuirOrdi == true) && (couléSMOrdi == true) && (couléCroisOrdi == true) && (couléCTOrdi == true))
                        {
                            victoire = 1;
                        }
                        if ((couléPA == true) && (couléCuir == true) && (couléSM == true) && (couléCrois == true) && (couléCT == true))
                        {
                            victoire = 0;
                        }
                    }

                    else // mode jeu normal
                    {
                        // tour joueur
                        nbTours++;
                        Console.WriteLine("###### TOUR {0} ######", nbTours);
                        Console.WriteLine("C'est votre tour. \nVous avez le droit à 1 tir.");
                        
                        if (niveauOrdi == false)//niveau facile : on ne peut pas tirer deux fois sur la meme case 
                        {
                            do
                            {
                                Console.WriteLine("Sur quelle case voulez-vous tirer ? ");
                                saisieUtilisateur = Console.ReadLine();
                                if (saisieUtilisateur == "ENSC")
                                {
                                    Console.WriteLine(" _____   __   __  _____   ______  ");
                                    Console.WriteLine("| ____| |  \\ | | / ___/  / ____|");
                                    Console.WriteLine("| |__   |   \\| | | |___  | |");
                                    Console.WriteLine("|  __|  | |\\   | \\____ \\ | |");
                                    Console.WriteLine("| |___  | | \\  |  ___| | | |___");
                                    Console.WriteLine("|_____| |_|  \\_| /_____/ \\_____|");
                                }
                                saisieColonne = saisieUtilisateur[0];
                                colonne = TraduireCharEnInt(saisieColonne);
                                if (saisieUtilisateur.Length == 3 && saisieUtilisateur[1] == '1' && saisieUtilisateur[2] == '0')
                                {
                                    ligne = 9;
                                }
                                else if (saisieUtilisateur.Length == 2)
                                {
                                    ligne = saisieUtilisateur[1] - 49;
                                }
                                if (saisieColonne == 'Q')

                                {
                                    Quitter(ref tabj1, ref tabOrdi, ref donnees, ref donneesOrdi, ref modeJeu, ref niveauOrdi);
                                    Environment.Exit(0);
                                }

                                else if ((saisieColonne != 'A') && (saisieColonne != 'B') && (saisieColonne != 'C') && (saisieColonne != 'D') && (saisieColonne != 'E') && (saisieColonne != 'F') && (saisieColonne != 'G') && (saisieColonne != 'H') && (saisieColonne != 'I') && (saisieColonne != 'J') || (saisieUtilisateur.Length >= 3 && (saisieUtilisateur[2] > 48)))
                                {
                                    Console.WriteLine("Veuillez tirer sur le plateau ou vérifiez que votre saisie est correcte (casse, nombre).");
                                }
                                else if (tabOrdi[ligne, colonne] == 'O' || tabOrdi[ligne, colonne] == 'X')
                                {
                                    Console.WriteLine("Vous aviez dejà tiré à cette endroit! Réessayez");
                                }
                            }
                            while ((saisieColonne != 'A') && (saisieColonne != 'B') && (saisieColonne != 'C') && (saisieColonne != 'D') && (saisieColonne != 'E') && (saisieColonne != 'F') && (saisieColonne != 'G') && (saisieColonne != 'H') && (saisieColonne != 'I') && (saisieColonne != 'J') || (saisieUtilisateur.Length >= 3 && (saisieUtilisateur[2] > 48)) || ((tabOrdi[ligne, colonne] == 'O' || tabOrdi[ligne, colonne] == 'X')));
                        }
                        else//niveau avancé : on peut tirer 2 fois sur la même case
                        {
                            do
                            {
                                Console.WriteLine("Sur quelle case voulez-vous tirer ? ");
                                saisieUtilisateur = Console.ReadLine();
                                if (saisieUtilisateur == "ENSC")
                                {
                                    Console.WriteLine(" _____   __   __  _____   ______  ");
                                    Console.WriteLine("| ____| |  \\ | | / ___/  / ____|");
                                    Console.WriteLine("| |__   |   \\| | | |___  | |");
                                    Console.WriteLine("|  __|  | |\\   | \\____ \\ | |");
                                    Console.WriteLine("| |___  | | \\  |  ___| | | |___");
                                    Console.WriteLine("|_____| |_|  \\_| /_____/ \\_____|");
                                }
                                saisieColonne = saisieUtilisateur[0];
                                colonne = TraduireCharEnInt(saisieColonne);
                                if (saisieUtilisateur.Length == 3 && saisieUtilisateur[1] == '1' && saisieUtilisateur[2] == '0')
                                {
                                    ligne = 9;
                                }
                                else if (saisieUtilisateur.Length == 2)
                                {
                                    ligne = saisieUtilisateur[1] - 49;
                                }
                                if (saisieColonne == 'Q')

                                {
                                    Quitter(ref tabj1, ref tabOrdi, ref donnees, ref donneesOrdi, ref modeJeu, ref niveauOrdi);
                                    Environment.Exit(0);
                                }

                                else if ((saisieColonne != 'A') && (saisieColonne != 'B') && (saisieColonne != 'C') && (saisieColonne != 'D') && (saisieColonne != 'E') && (saisieColonne != 'F') && (saisieColonne != 'G') && (saisieColonne != 'H') && (saisieColonne != 'I') && (saisieColonne != 'J') || (saisieUtilisateur.Length >= 3 && (saisieUtilisateur[2] > 48)))
                                {
                                    Console.WriteLine("Veuillez tirer sur le plateau  ou vérifiez que votre saisie est correcte (casse, nombre).");
                                }
                            }
                            while ((saisieColonne != 'A') && (saisieColonne != 'B') && (saisieColonne != 'C') && (saisieColonne != 'D') && (saisieColonne != 'E') && (saisieColonne != 'F') && (saisieColonne != 'G') && (saisieColonne != 'H') && (saisieColonne != 'I') && (saisieColonne != 'J') || (saisieUtilisateur.Length >= 3 && (saisieUtilisateur[2] > 48)));
                        }

                        Tirer(colonne, ligne, tabOrdi);
                        DefinirTableau(PAOrdi, 0, donneesOrdi, tabOrdi);
                        DefinirTableau(CuirOrdi, 1, donneesOrdi, tabOrdi);
                        DefinirTableau(SMOrdi, 2, donneesOrdi, tabOrdi);
                        DefinirTableau(CroisOrdi, 3, donneesOrdi, tabOrdi);
                        DefinirTableau(CTOrdi, 4, donneesOrdi, tabOrdi);

                        if (couléPAOrdi == false)
                        {
                            TesterToucheCoule(PAOrdi, ref nbBateauCouléOrdi, ref couléPAOrdi);
                        }
                        if (couléCuirOrdi == false)
                        {
                            TesterToucheCoule(CuirOrdi, ref nbBateauCouléOrdi, ref couléCuirOrdi);
                        }
                        if (couléSMOrdi == false)
                        {
                            TesterToucheCoule(SMOrdi, ref nbBateauCouléOrdi, ref couléSMOrdi);
                        }
                        if (couléCroisOrdi == false)
                        {
                            TesterToucheCoule(CroisOrdi, ref nbBateauCouléOrdi, ref couléCroisOrdi);
                        }
                        if (couléCTOrdi == false)
                        {
                            TesterToucheCoule(CTOrdi, ref nbBateauCouléOrdi, ref couléCTOrdi);
                        }
                        Console.WriteLine("Plateau de l'adversaire");
                        DessinerPlateau(tabOrdi);
                        Console.WriteLine(" \nAppuyez sur une touche pour continuer.");
                        Console.ReadKey();
                        //tour ordi
                        Console.WriteLine("C'est le tour de l'ordi. ");

                        char saisieColonneOrdi = 'W';
                        if (niveauOrdi == false)//ordi mode facile
                        {
                            do
                            {
                                colonneOrdi = r.Next(0, 10);
                                ligneOrdi = r.Next(0, 10);
                                saisieColonneOrdi = TraduireIntEnChar(colonneOrdi);
                            }
                            while (tabj1[ligneOrdi, colonneOrdi] == 'O' || tabj1[ligneOrdi, colonneOrdi] == 'X');


                            Console.WriteLine("L'ordi a tiré en " + saisieColonneOrdi + (ligneOrdi + 1));
                            Tirer(colonneOrdi, ligneOrdi, tabj1);
                        }
                        else//nivOrdi == true, cad l'IA est intelligente
                        {
                            if (pas == 0)//l'IA n'a pas de cible en mémoire
                            {
                                do
                                {
                                    colonneOrdi = r.Next(0, 10);
                                    ligneOrdi = r.Next(0, 10);
                                    saisieColonneOrdi = TraduireIntEnChar(colonneOrdi);
                                }
                                while (tabj1[ligneOrdi, colonneOrdi] == 'O' || tabj1[ligneOrdi, colonneOrdi] == 'X');
                                TirerOrdi(colonneOrdi, ligneOrdi, tabj1, ref touche);
                                Console.WriteLine("L'ordi a tiré en : " + saisieColonneOrdi + (ligneOrdi + 1));
                                if (touche == true)
                                {
                                    pas++;
                                }
                            }
                            else//l'IA a une cible en mémoire
                            {

                                ChercherCible(ref orientation, ref pas, ref colonneOrdi, ref ligneOrdi, tabj1, ref touche);
                                /*Verifications 
                                Console.WriteLine(touche);
                                Console.WriteLine("orientation=" + orientation);
                                Console.WriteLine("pas :" + pas);*/
                                if (touche == false)
                                {
                                    orientation = orientation + 1;
                                    pas = 1;
                                }
                                else
                                {
                                    pas++;
                                }
                                if (pas == 5)
                                {
                                    orientation++;
                                    pas = 1;
                                }
                                if (orientation == 4)
                                {
                                    pas = 0;
                                    orientation = 0;
                                }
                            }
                        }

                        DefinirTableau(PA, 0, donnees, tabj1);
                        DefinirTableau(Cuir, 1, donnees, tabj1);
                        DefinirTableau(SM, 2, donnees, tabj1);
                        DefinirTableau(Crois, 3, donnees, tabj1);
                        DefinirTableau(CT, 4, donnees, tabj1);

                        if (couléPA == false)
                        {
                            TesterToucheCoule(PA, ref nbBateauCoulé, ref couléPA);
                        }
                        if (couléCuir == false)
                        {
                            TesterToucheCoule(Cuir, ref nbBateauCoulé, ref couléCuir);
                        }
                        if (couléSM == false)
                        {
                            TesterToucheCoule(SM, ref nbBateauCoulé, ref couléSM);
                        }
                        if (couléCroisOrdi == false)
                        {
                            TesterToucheCoule(Crois, ref nbBateauCoulé, ref couléCrois);
                        }
                        if (couléCT == false)
                        {
                            TesterToucheCoule(CT, ref nbBateauCoulé, ref couléCT);
                        }
                        DessinerPlateau(tabj1);
                        if ((couléPAOrdi == true) && (couléCuirOrdi == true) && (couléSMOrdi == true) && (couléCroisOrdi == true) && (couléCTOrdi == true))
                        {
                            victoire = 1;
                        }
                        if ((couléPA == true) && (couléCuir == true) && (couléSM == true) && (couléCrois == true) && (couléCT == true))
                        {
                            victoire = 0;
                        }
                    }
                }
                //Affichage de fin
                if (victoire == 1)
                { Console.WriteLine("Bravo ! Vous avez gagné !\n Il vous a fallu {0} tours pour gagner.", nbTours); }
                if (victoire == 0)
                { Console.WriteLine("Désolé vous avez perdu !\n La partie a duré {0} tours.", nbTours); }
                Console.WriteLine("Voulez-vous rejouer ? (o/n)");
                saisieUtilisateur = Console.ReadLine();
            } while (saisieUtilisateur == "o");
            //Vérifications 
            DessinerPlateau(tabOrdi);

            //Fin de partie
            FinirJeu();

            Console.ReadKey();
        }
    }
}

