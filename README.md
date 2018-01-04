using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace IPROG_Alice
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
            int choix = r.Next(2); //si choix vaut 0, il place de manière horizontale, sinon de manière verticale
            bool test = true;
            if (choix == 0)
            {
                do
                {
                    test = true;
                    int i = r.Next(10);
                    int j = r.Next(10 - tabBateau.Length);
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
                } while (test == false);
            }
            else
            {
                do
                {
                    test = true;
                    int j = r.Next(10);
                    int i = r.Next(10 - tabBateau.Length);
                    //teste si le tableau est vide là où on veut écrire
                    int k; //compteur de la taille du tableau du bateau
                    for (k = 0; k < tabBateau.Length; k++)
                    {
                        if ((tab[i + k, j] != 0)) //|| (tab[i + k, j] == '#'))
                        {
                            test = false;
                        }

                        if (test == true)
                        {
                            tab[i + k, j] = tabBateau[k];
                        }
                    }
                } while (test == false);
            }
        }




        static void InitialiserPlateauOrdi(char[,] tab, char[] tabBateau, int[] data)
        {
            Random r = new Random();
            int choix = r.Next(2); //si choix vaut 0, il place de manière horizontale, sinon de manière verticale
            bool test = true;
            int indiceI; //à récupérer, premier case du bateau
            int indiceJ;
            if (choix == 0)
            {
                do
                {
                    test = true;
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
                } while (test == false);
            }
            else
            {
                do
                {
                    test = true;
                    int j = r.Next(10);
                    int i = r.Next(10 - tabBateau.Length);
                    indiceI = i;
                    indiceJ = j;
                    //teste si le tableau est vide là où on veut écrire
                    int k; //compteur de la taille du tableau du bateau
                    for (k = 0; k < tabBateau.Length; k++)
                    {
                        if ((tab[i + k, j] != 0)) //|| (tab[i + k, j] == '#'))
                        {
                            test = false;
                        }

                        if (test == true)
                        {
                            tab[i + k, j] = tabBateau[k];
                        }
                    }
                } while (test == false);
            }
            //data = { tabBateau.Length, choix, indiceI; indiceJ};
            data[0] = tabBateau.Length;
            data[1] = choix;
            data[2] = indiceI;
            data[3] = indiceJ;

            //return data;
        }


        static void LirePlateauOrdi(char[,] tab, int[,] donnees)
        {
            for (int k = 0; k < 17; k++)
            {
                for (int i = 0; i < 10; i++)
                {
                    for (int j = 0; j < 10; j++)
                    {

                        if (tab[i, j] == '#')
                        {
                            donnees[k, 0] = i;
                            donnees[k, 1] = j;
                        }
                    }
                }
            }

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
                Console.WriteLine("##### REGLES #####\n\n A expliquer !!! \nmode normal + mode salvo");
            }
            string reponse2 = "a";
            while ((reponse2 != "s") && (reponse2 != "n"))
            {
                Console.WriteLine("Avec quel mode voulez-vous jouer ? Tapez 's' pour le mode Salvo ou 'n' pour le mode normal");
                reponse2 = Console.ReadLine();
            }
            if (reponse2 == "n")
            {
                bool1 = false;
            }
            string reponse3 = "a";
            while ((reponse3 != "f") && (reponse3 != "i"))
            {
                Console.WriteLine("Quel niveau souhaitez-vous pour l'ordinateur ? Tapez 'f' pour facile ou 'i' pour intelligent");
                reponse3 = Console.ReadLine();
            }
            if (reponse3 == "i")
            {
                bool2 = true;
            }
        }


        static void Main(string[] args)
        {
            bool modeJeu = true; //par défaut le mode salvo est lancé
            bool niveauOrdi = false; //par défaut le niveau facile est lancé
            PresenterJeu(ref modeJeu, ref niveauOrdi); //faut placer les arguments en références pour qu'ils soient effectivement modifiés
            Console.WriteLine("Mode Jeu : "+ modeJeu);
            Console.WriteLine("nivordi :" +niveauOrdi);

            

            char[,] tabj1 = new char[10, 10];
            char[,] tabOrdi = new char[10, 10];

            //Création des bateaux
            char[] PA = { '#', '#', '#', '#', '#' }; //PorteAvion
            char[] Cuir = { '#', '#', '#', '#' }; //Cuirassé
            char[] SM = { '#', '#', '#' }; //SousMarin
            char[] Crois = { '#', '#', '#' }; //Croiseur
            char[] CT = { '#', '#' };//ContreTorpilleur

            //Début de partie : choix du placement des bateaux
            string reponse = "a";
            Console.WriteLine("VOTRE PLATEAU");
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
            int[] dataPA = new int[4];
            int[] dataCuir = new int[4];
            int[] data = new int[4]; //ATTTTEEEENNTTTTIOOOONN !!!!!!!!!!!!!!!!
            int[] dataCrois = new int[4];
            int[] dataCT = new int[4];
            int[,] donnees = new int[17, 2];
            for (int k = 0; k < 5; k++)
            {
                tabOrdi[3 + k, 0] = PA[k];
            }
            InitialiserPlateauOrdi(tabOrdi, SM, data);
            for (int m = 0; m < 4; m++)
            { Console.WriteLine(data[m]); }
            DessinerPlateau(tabOrdi);
            LirePlateauOrdi(tabOrdi, donnees);
            for (int i = 0; i < 17; i++)
            {
                Console.Write(donnees[i, 0]);
                Console.Write(',');
            }
            Console.WriteLine("\n");
            for (int i = 0; i < 17; i++)
            {
                Console.Write(donnees[i, 1]);
                Console.Write(',');
            }
            Console.WriteLine("\n \n");


            //Déroulement de la partie
            int nbBateauCoulé = 0;
            int nbTirDispo = 5 - nbBateauCoulé;
            Console.WriteLine("C'est votre tour. Sur quelle case voulez-vous tirer ? \nVous avez le droit à {0} tir(s).", nbTirDispo);

            for (int nbTir = 0; nbTir < 5; nbTir++)
            {
                Console.WriteLine("C'est votre tir n°{0}.", (nbTir + 1));
                string saisieColonne = "K";
                while ((saisieColonne != "A") && (saisieColonne != "B") && (saisieColonne != "C") && (saisieColonne != "D") && (saisieColonne != "E") && (saisieColonne != "F") && (saisieColonne != "G") && (saisieColonne != "H") && (saisieColonne != "I") && (saisieColonne != "J"))
                {
                    Console.Write("Colonne ? ");
                    saisieColonne = Console.ReadLine();
                }
                int colonne = -3;
                if (saisieColonne == "A")
                { colonne = 0; }
                else if (saisieColonne == "B")
                { colonne = 1; }
                else if (saisieColonne == "C")
                { colonne = 2; }
                else if (saisieColonne == "D")
                { colonne = 3; }
                else if (saisieColonne == "E")
                { colonne = 4; }
                else if (saisieColonne == "F")
                { colonne = 5; }
                else if (saisieColonne == "G")
                { colonne = 6; }
                else if (saisieColonne == "H")
                { colonne = 7; }
                else if (saisieColonne == "I")
                { colonne = 8; }
                else if (saisieColonne == "J")
                { colonne = 9; }


                int ligne = 11;
                while ((ligne < 0) || (ligne > 9))
                {
                    Console.Write("Ligne ? ");
                    string saisieLigne = Console.ReadLine();
                    ligne = Convert.ToInt16(saisieLigne);
                }
                ligne--;//pour que le numéro de ligne entré corresponde à la bonne ligne du plateau


                //Actions sur le plateau de l'IA
                if (tabOrdi[ligne, colonne] == 0)
                {
                    tabOrdi[ligne, colonne] = 'O'; //raté, tir dans l'eau
                    Console.WriteLine("Raté !");
                }
                else
                    if (tabOrdi[ligne, colonne] == '#')//cad sur un bateau
                {
                    tabOrdi[ligne, colonne] = 'X'; //touché
                    Console.WriteLine("Touché !");

                    /*if (data[0]==2)
                    {
                        CT[0] = 'X';
                    } else */
                    /*if (data[0] == 3)
                    {
                        SM[0] = 'X';
                    }*//* else if (data[0]==4)
                    {
                        Cuir[0] = 'X';
                    }else if (data[0]==5)
                    {
                        PA[0] = 'X';
                    }
                    else
                    {
                        Crois[0] = 'X';
                    }*/
                }
                else if ((tabOrdi[ligne, colonne] == 'O') || (tabOrdi[ligne, colonne] == 'X'))
                { Console.WriteLine("Attention ! Vous aviez déjà tiré à cet endroit."); } // ATTENTION ! DEPEND DU MODE DE JEU














                //TOUCHE COULE
                bool test = true;
                for (int k = 0; k < 3; k++)
                {
                    if (SM[k] != '#')
                    {
                        test = false;
                    }
                    if (test == true)
                    {
                        Console.WriteLine("Touché coulé !");
                    }
                }
            }




            //Vérifications 
            DessinerPlateau(tabOrdi);

            Console.ReadKey();
        }


    }
}
