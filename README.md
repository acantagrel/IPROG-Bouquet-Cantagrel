using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;


namespace ProjetInfo
{
    class Program
    {



        static void DessinerPlateau(char[,] tab)
        {
            //procédure qui trace le plateau de jeu, i.e. un tableau de case 10x10
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




        static void InitialiserPlateau(char[,] tab, char[] tabBateau)
        {
            Random r = new Random();
            int choix;
            bool test;
            do
            {
                choix = r.Next(2);
                test = true;
                if (choix == 0)
                {

                    int i = r.Next(10);
                    int j = r.Next(10 - tabBateau.Length);
                    //teste si le tableau est vide là où on veut écrire
                    int k; //compteur de la taille du tableau du bateau
                    for (k = 0; k < tabBateau.Length; k++)
                    {
                        if (tab[i, j + k] == '#')
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


                else
                {

                    int j = r.Next(10);
                    int i = r.Next(10 - tabBateau.Length);
                    //teste si le tableau est vide là où on veut écrire
                    int k; //compteur de la taille du tableau du bateau
                    for (k = 0; k < tabBateau.Length; k++)
                    {
                        if (tab[i + k, j] == '#') //(tab[i + k, j] != 0)
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
        }




        static void InitialiserPlateauOrdi(char[,] tab, char[] tabBateau, int nb, ref int[] data)
        {
            Random r = new Random();
            int choix;
            bool test;
            int indiceI; //à récupérer, premier case du bateau
            int indiceJ;
            do
            {
                choix = r.Next(2);
                test = true;

                if (choix == 0)
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
                else
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

            //return data;
        }


        static int LirePlateau(char[,] tab)
        {
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




        static void PresenterJeu(ref bool bool1, ref bool bool2)
        {
            Console.WriteLine("######################## BATAILLE NAVALE ########################");
            Console.WriteLine("\nBienvenue ! Ce jeu vous permet de jouer à la bataille navale contre votre ordinateur.");
            string reponse = "a";
            while ((reponse != "o") && (reponse != "n"))
            {

                Console.WriteLine("Voulez -vous lire les règles ? (o/n)");
                reponse = Console.ReadLine();
            }
            if (reponse == "o")
            {
                Console.WriteLine("##### REGLES #####\n\nLe but de la bataille navale est de couler tous les bateaux de son adversaire.\nDans un premier temps, chaque joueur place ses bateaux sur le plateau sans voir ceux de son adversaire.\nEnsuite, chacun à leur tour, les joueurs essaient de trouver et de couler les bateaux de l'adversaire.\nChaque joueur dispose de 5 bateaux longueurs différentes: \n- Un porte-avion d'une longueur de 5 cases\n- Un cuirassé d'une longueur de 4 cases \n- Un sous-marin et un croiseur d'une longueur de 3 cases \n- Un contre-torpilleur d'une longueur de 2 cases \nCe jeu dispose de deux modes de jeux suivant la façon de tirer :\n- le mode classique : A chaque tir annoncé par un joueur (par exemple, 'case C5'), le second joueur regarde si l’un de ses navires occupe la case visée. \nIl doit indiquer à l'autre joueur s'il a touché ('Touché') ou coulé ('Touché coulé') un navire ou bien tiré dans l'eau ('Raté').\n- mode salvo : chaque joueur annonce plusieurs tirs à la fois. Le nombre de tirs simultanés est de 5 initialement. Ce nombre diminue en fonction du nombre de bateaux déjà coulés.\nQuand un joueur détruit un navire de son adversaire, il ne tire plus que 4 coups au lieu de 5. Quand 2 bateaux sont détruits, le joueur ennemi tire uniquement 3 coups. \nQuand 3 navires sont détruits, le joueur opposé ne tire plus que 2 coups, etc.");
            }
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
        }



        static void TesterToucheCoule(char[] tabBateau, ref int nbBateauCoulé, ref bool coulé)
        {
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
            //score ?
            Console.WriteLine("Merci d'avoir joué ! Nous espérons vous revoir bientôt !");
            Console.WriteLine("Ce programme a été développé par Antoine BOUQUET et Alice CANTAGREL dans le cadre du projet informatique IPROG de première année à l'ENSC.");
        }


        static void DefinirTableau(char[] tabBateau, int a, int[] donnees, char[,] tab)
        {

            if (donnees[1 + a * 4] == 0)
            {
                for (int k = 0; k < donnees[a * 4]; k++)
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




        static void Tirer(int colonne, int ligne, char[,] tableau)
        {

            if (tableau[ligne, colonne] == 0)
            {
                tableau[ligne, colonne] = 'O'; //raté, tir dans l'eau
                Console.WriteLine("Raté !");
            }
            else
                        if ((tableau[ligne, colonne] == '#') || (tableau[ligne, colonne] == ' '))//cad sur un bateau
            {
                tableau[ligne, colonne] = 'X'; //touché
                Console.WriteLine("Touché !");
            }
            else if ((tableau[ligne, colonne] == 'O') || (tableau[ligne, colonne] == 'X'))
            { Console.WriteLine("Attention ! Vous aviez déjà tiré à cet endroit."); } // ATTENTION ! DEPEND DU MODE DE JEU

        }
        static int TraduireStringEnInt(string saisieColonne)
        {
            int colonne = -1;
            if (saisieColonne == "A")
            {
                colonne = 0;
            }
            else if (saisieColonne == "B")
            {
                colonne = 1;
            }
            else if (saisieColonne == "C")
            {
                colonne = 2;
            }
            else if (saisieColonne == "D")
            {
                colonne = 3;
            }
            else if (saisieColonne == "E")
            {
                colonne = 4;
            }
            else if (saisieColonne == "F")
            {
                colonne = 5;
            }
            else if (saisieColonne == "G")
            {
                colonne = 6;
            }
            else if (saisieColonne == "H")
            {
                colonne = 7;
            }
            else if (saisieColonne == "I")
            {
                colonne = 8;
            }
            else if (saisieColonne == "J")
            {
                colonne = 9;
            }
            return colonne;
        }

        static char TraduireIntEnChar(int colonne)
        {
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
        static void Quitter(string answer, ref char[,] tab)
        {
            answer = "a";
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
                            Sauvegarder(ref tab);
                        }

                    }
                    Environment.Exit();
                }
            }
           

        }


        static void Sauvegarder(ref char[,] tab)
        {
            Console.WriteLine("Sous quel nom voulez-vous enregistrer votre partie ?");
            string nom = Console.ReadLine();
            string path = "H:\\test-projet info\\";
            string format = ".txt";
            string pathComplet = path + nom + format;
            String date = System.DateTime.Now.ToShortDateString();
            string presentation = "vous avez sauvegardé cette partie le " + date;
            System.IO.File.WriteAllText(@pathComplet, presentation);// crée le fichier et enregistre le deuxième argument dedans
            string[,] tabString = new string[10, 10];
            //tabString = Convert.ToString(tab);

            using (System.IO.StreamWriter file = new System.IO.StreamWriter(@pathComplet, true))
            {
                //file.WriteLine(DessinerPlateau(tab));
            }

        }




        static void Main(string[] args)
        {
            //interface et choix de jeu
            bool modeJeu = true; //par défaut le mode salvo est lancé
            bool niveauOrdi = false; //par défaut le niveau facile est lancé
            PresenterJeu(ref modeJeu, ref niveauOrdi); //faut placer les arguments en références pour qu'ils soient effectivement modifiés


            char[,] tabj1 = new char[10, 10];
            char[,] tabOrdi = new char[10, 10];
            int nbTours = 0;

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

            //Début de partie : choix du placement des bateaux
            Random r = new Random();
            int choix = r.Next(2); //si choix vaut 0, il place de manière horizontale, sinon de manière verticale
            string reponse = "a";
            Console.WriteLine("\nVOTRE PLATEAU");
            InitialiserPlateau(tabj1, PA);
            InitialiserPlateau(tabj1, Cuir);
            InitialiserPlateau(tabj1, SM);
            InitialiserPlateau(tabj1, Crois);
            InitialiserPlateau(tabj1, CT);
            DessinerPlateau(tabj1);
            while ((reponse != "o") && (reponse != "n"))
            {
                Console.WriteLine("Le placement des bateaux vous convient-il ? (o/n)");
                reponse = Console.ReadLine();

                while (reponse == "n")
                {
                    tabj1 = new char[10, 10]; //réinitialiser tabj1 
                    InitialiserPlateau(tabj1, PA);
                    InitialiserPlateau(tabj1, Cuir);
                    InitialiserPlateau(tabj1, SM);
                    InitialiserPlateau(tabj1, Crois);
                    InitialiserPlateau(tabj1, CT);
                    DessinerPlateau(tabj1);
                    Console.WriteLine("Le placement des bateaux vous convient-il ? (o/n)");
                    reponse = Console.ReadLine();
                }
            }
            Console.WriteLine("\n \n");


            //Initialisation du plateau de l'IA
            Console.WriteLine("PLATEAU DE L'IA");
            int[] donneesOrdi = new int[20];
            int[] donnees = new int[20];
            int compteur = 0;
            int bateau = 0;
            for (compteur = 0; compteur < 5; compteur++)
            {
                if (bateau == 0)
                {
                    InitialiserPlateauOrdi(tabOrdi, PAOrdi, compteur, ref donneesOrdi);
                }
                if (bateau == 1)
                {
                    InitialiserPlateauOrdi(tabOrdi, CuirOrdi, compteur, ref donneesOrdi);
                }
                if (bateau == 2)
                {
                    InitialiserPlateauOrdi(tabOrdi, SMOrdi, compteur, ref donneesOrdi);
                }
                if (bateau == 3)
                {
                    InitialiserPlateauOrdi(tabOrdi, CroisOrdi, compteur, ref donneesOrdi);
                }
                if (bateau == 4)
                {
                    InitialiserPlateauOrdi(tabOrdi, CTOrdi, compteur, ref donneesOrdi);
                }
                bateau++;
            }

            /*TEST POUR PLACEMENT D 1 BATEAU 
             * for (int k = 0; k < 5; k++)
             {
                 tabOrdi[3 + k, 0] = PA[k];
             }*/


            DessinerPlateau(tabOrdi);
            Console.WriteLine("\n");


            //Déroulement de la partie
            int nbBateauCoulé = 0;
            int nbBateauCouléOrdi = 0;

            int victoire = -1;
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


            while (victoire != 0 || victoire != 1)
            {
                if (modeJeu == true) // ((couléPA == false) || (couléCuir == false) || (couléSM == false) || (couléCrois == false) || (couléCT == false))
                {
                    int nbTirDispoOrdi;
                    int nbTirDispo = 5 - nbBateauCouléOrdi;
                    nbTours++;
                    Console.WriteLine("###### TOUR {0} ######", nbTours);
                    Console.WriteLine("C'est votre tour. Sur quelle case voulez-vous tirer ? \nVous avez le droit à {0} tir(s).", nbTirDispo);
                    for (int nbTir = 0; nbTir < nbTirDispo; nbTir++)
                    {
                        Console.WriteLine("C'est votre tir n°{0}.", (nbTir + 1));
                        string saisieColonne = "K";
                        while ((saisieColonne != "A") && (saisieColonne != "B") && (saisieColonne != "C") && (saisieColonne != "D") && (saisieColonne != "E") && (saisieColonne != "F") && (saisieColonne != "G") && (saisieColonne != "H") && (saisieColonne != "I") && (saisieColonne != "J") && (saisieColonne != "Q"))
                        {
                            Console.Write("Colonne ? ");
                            saisieColonne = Console.ReadLine();
                        }
                        int colonne = -1;

                        if (saisieColonne != "Q")
                        {
                            colonne = TraduireStringEnInt(saisieColonne);
                        }
                        else
                        {
                            Quitter(reponse, ref tabj1);
                            Environment.Exit(0);
                        }

                        int ligne = 11;
                        while ((ligne < 0) || (ligne > 10))
                        {
                            Console.Write("Ligne ? ");
                            string saisieLigne = Console.ReadLine();
                            ligne = Convert.ToInt16(saisieLigne);
                        }
                        ligne--;//pour que le numéro de ligne entré corresponde à la bonne ligne du plateau

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
                        DessinerPlateau(tabOrdi);
                        //DessinerPlateau(tabj1);
                    }//for (nbTir<5)
                    nbTirDispoOrdi = 5 - nbBateauCoulé;
                    Console.WriteLine("C'est le tour de l'ordi. \nIl a le droit à {0} tir(s).", nbTirDispoOrdi);
                    int colonneOrdi;
                    int ligneOrdi;


                    for (int nbTir = 0; nbTir < nbTirDispoOrdi; nbTir++)
                    {
                        char saisieColonneOrdi = 'W';
                        if (niveauOrdi == false)
                        {
                            do
                            {
                                colonneOrdi = r.Next(0, 10);
                                ligneOrdi = r.Next(0, 10);
                                saisieColonneOrdi = TraduireIntEnChar(colonneOrdi);

                            }
                            while (tabj1[ligneOrdi, colonneOrdi] == 'O' || tabj1[ligneOrdi, colonneOrdi] == 'X');
                        }
                        else
                        {

                        }
                        Console.WriteLine("L'ordi a tiré en " + saisieColonneOrdi + (ligneOrdi + 1));
                        Tirer(colonneOrdi, ligneOrdi, tabj1);
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

                    }
                    DessinerPlateau(tabj1);

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

                else
                {
                    nbTours++;
                    Console.WriteLine("###### TOUR {0} ######", nbTours);
                    Console.WriteLine("C'est votre tour. Sur quelle case voulez-vous tirer ? ");
                    string saisieColonne = "K";
                    while ((saisieColonne != "A") && (saisieColonne != "B") && (saisieColonne != "C") && (saisieColonne != "D") && (saisieColonne != "E") && (saisieColonne != "F") && (saisieColonne != "G") && (saisieColonne != "H") && (saisieColonne != "I") && (saisieColonne != "J") && (saisieColonne != "Q"))
                    {
                        Console.Write("Colonne ? ");
                        saisieColonne = Console.ReadLine();
                    }
                    int colonne = -1;

                    if (saisieColonne != "Q")
                    {
                        colonne = TraduireStringEnInt(saisieColonne);
                    }
                    else
                    {
                        Quitter(reponse, ref tabj1);
                        Environment.Exit(0);
                    }


                    int ligne = 11;
                    while ((ligne < 0) || (ligne > 10))
                    {
                        Console.Write("Ligne ? ");
                        string saisieLigne = Console.ReadLine();
                        ligne = Convert.ToInt16(saisieLigne);
                    }
                    ligne--;//pour que le numéro de ligne entré corresponde à la bonne ligne du plateau


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

                    DessinerPlateau(tabOrdi);
                    Console.WriteLine("C'est le tour de l'ordi. ");
                    int colonneOrdi;
                    int ligneOrdi;
                    char saisieColonneOrdi = 'W';
                    if (niveauOrdi == false)
                    {
                        do
                        {
                            colonneOrdi = r.Next(0, 10);
                            ligneOrdi = r.Next(0, 10);
                            saisieColonneOrdi = TraduireIntEnChar(colonneOrdi);
                        }
                        while (tabj1[ligneOrdi, colonneOrdi] == 'O' || tabj1[ligneOrdi, colonneOrdi] == 'X');
                    }
                    else
                    {

                    }
                    Console.WriteLine("L'ordi a tiré en " + saisieColonneOrdi + (ligneOrdi + 1));
                    Tirer(colonneOrdi, ligneOrdi, tabj1);
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
                if (victoire == 1)
                { Console.WriteLine("Bravo ! Vous avez gagné !\n Il vous a fallu {0} tours pour gagner.", nbTours); }
                if (victoire == 0)
                { Console.WriteLine("Désolé vous avez perdu !\n Il vous a fallu {0} tours pour gagner.", nbTours); }


            }


            Console.WriteLine("Bravo ! Vous avez gagné !\n Il vous a fallu {0} tours pour gagner.", nbTours);



            //Vérifications 
            DessinerPlateau(tabOrdi);


            //scores

            //Sauvegarde

            //Fin de partie
            FinirJeu();


            Console.ReadKey();
        }
    }
}
