using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace test1
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
            int choix; //si choix vaut 0, il place de manière horizontale, sinon de manière verticale
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
                        if (tab[i + k, j] == '#')
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
                }//il faut mettre un while !!! pour recommencer quand le test est faux !!!
            }
            while (test == false);
        }

        static void Main(string[] args)
        {
            char[,] tabj1 = new char[10, 10];
            //tabj1[0, 0] = 'X' ;

            //Création des bateaux
            char[] PA = { '#', '#', '#', '#', '#' }; //PorteAvion
            char[] Cuir = { '#', '#', '#', '#' }; //Cuirassé
            char[] SM = { '#', '#', '#' }; //SousMarin
            char[] Crois = { '#', '#', '#' }; //Croiseur
            char[] CT = { '#', '#' };//ContreTorpilleur

            DessinerPlateau(tabj1);
            Console.Write("\n");
            InitialiserPlateau(tabj1, PA);
            InitialiserPlateau(tabj1, Cuir);
            InitialiserPlateau(tabj1, SM);
            InitialiserPlateau(tabj1, Crois);
            InitialiserPlateau(tabj1, CT);
            DessinerPlateau(tabj1);
            string reponse = "a";
            while ((reponse != "o") && (reponse != "n"))
            {
                Console.WriteLine("Le placement des bateaux vous convient-il ? (o/n)");
                reponse = Console.ReadLine();
                while (reponse == "n")
                {
                    tabj1 = new char[10, 10];
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
            Console.ReadKey();
        }
    }
}
