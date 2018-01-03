# IPROG
Projet Info S5

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
                    Console.Write((i + 1) +" ");
                }//fin nom des lignes
                for (int j = 0; j<10; j++)
                {
                    Console.Write("*  " + tab[i, j] + "  ");
                    if (j==9)
                    {
                        Console.Write("*");
                    }
                }
                Console.Write("\n");
                Console.Write("   *     *     *     *     *     *     *     *     *     *     *\n");
                if (i==9)
                {
                    Console.Write("****************************************************************\n");
                }
            }
        }



        /*
        static void InitialiserPlateau(char[,] tab, char[] tabBateau)
        {
            Random r = new Random();
            int choix = r.Next(2); //si choix vaut 0, il place de manière horizontale, sinon de manière verticale
            bool test = true;
           
            do
            {
                if (choix == 0)
                {
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

                        if (test == true)
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
                }//il faut mettre un while !!! pou recommencer quand le test est faux !!!
            } while (test == false);
        }*/



        static void InitialiserPlateau(char[,] tab, char[] tabB1, char[] tabB2, char[] tabB3, char[] tabB4, char[] tabB5)
        {
            Random r = new Random();
            int choix = r.Next(2); //si choix vaut 0, il place de manière horizontale, sinon de manière verticale
            bool test = true;

            do
            {
                if (choix == 0)
                {
                    int i = r.Next(10);
                    int j = r.Next(10 - tabB1.Length);
                    //teste si le tableau est vide là où on veut écrire
                    int k; //compteur de la taille du tableau du bateau
                    for (k = 0; k < tabB1.Length; k++)
                    {
                        if (tab[i, j + k] != 0)
                        {
                            test = false;

                        }

                        if (test == true)
                        {

                            tab[i, j + k] = tabB1[k];
                        }
                    }
                }
                else
                {
                    int j = r.Next(10);
                    int i = r.Next(10 - tabB1.Length);
                    //teste si le tableau est vide là où on veut écrire
                    int k; //compteur de la taille du tableau du bateau
                    for (k = 0; k < tabB1.Length; k++)
                    {
                        if (tab[i + k, j] != 0)
                        {
                            test = false;

                        }
                    }
                    if (test == true)
                    {
                        for (k = 0; k < tabB1.Length; k++)
                        {
                            tab[i + k, j] = tabB1[k];
                        }
                    }
                }//il faut mettre un while !!! pou recommencer quand le test est faux !!!
            } while (test == false);

            do
            {
                if (choix == 0)
                {
                    int i = r.Next(10);
                    int j = r.Next(10 - tabB2.Length);
                    //teste si le tableau est vide là où on veut écrire
                    int k; //compteur de la taille du tableau du bateau
                    for (k = 0; k < tabB2.Length; k++)
                    {
                        if (tab[i, j + k] != 0)
                        {
                            test = false;

                        }

                        if (test == true)
                        {

                            tab[i, j + k] = tabB2[k];
                        }
                    }
                }
                else
                {
                    int j = r.Next(10);
                    int i = r.Next(10 - tabB2.Length);
                    //teste si le tableau est vide là où on veut écrire
                    int k; //compteur de la taille du tableau du bateau
                    for (k = 0; k < tabB2.Length; k++)
                    {
                        if (tab[i + k, j] != 0)
                        {
                            test = false;

                        }
                    }
                    if (test == true)
                    {
                        for (k = 0; k < tabB2.Length; k++)
                        {
                            tab[i + k, j] = tabB2[k];
                        }
                    }
                }//il faut mettre un while !!! pou recommencer quand le test est faux !!!
            } while (test == false);
            do
            {
                if (choix == 0)
                {
                    int i = r.Next(10);
                    int j = r.Next(10 - tabB3.Length);
                    //teste si le tableau est vide là où on veut écrire
                    int k; //compteur de la taille du tableau du bateau
                    for (k = 0; k < tabB3.Length; k++)
                    {
                        if (tab[i, j + k] != 0)
                        {
                            test = false;

                        }

                        if (test == true)
                        {

                            tab[i, j + k] = tabB3[k];
                        }
                    }
                }
                else
                {
                    int j = r.Next(10);
                    int i = r.Next(10 - tabB3.Length);
                    //teste si le tableau est vide là où on veut écrire
                    int k; //compteur de la taille du tableau du bateau
                    for (k = 0; k < tabB3.Length; k++)
                    {
                        if (tab[i + k, j] != 0)
                        {
                            test = false;

                        }
                    }
                    if (test == true)
                    {
                        for (k = 0; k < tabB3.Length; k++)
                        {
                            tab[i + k, j] = tabB3[k];
                        }
                    }
                }//il faut mettre un while !!! pou recommencer quand le test est faux !!!
            } while (test == false);
            do
            {
                if (choix == 0)
                {
                    int i = r.Next(10);
                    int j = r.Next(10 - tabB4.Length);
                    //teste si le tableau est vide là où on veut écrire
                    int k; //compteur de la taille du tableau du bateau
                    for (k = 0; k < tabB4.Length; k++)
                    {
                        if (tab[i, j + k] != 0)
                        {
                            test = false;

                        }

                        if (test == true)
                        {

                            tab[i, j + k] = tabB4[k];
                        }
                    }
                }
                else
                {
                    int j = r.Next(10);
                    int i = r.Next(10 - tabB4.Length);
                    //teste si le tableau est vide là où on veut écrire
                    int k; //compteur de la taille du tableau du bateau
                    for (k = 0; k < tabB4.Length; k++)
                    {
                        if (tab[i + k, j] != 0)
                        {
                            test = false;

                        }
                    }
                    if (test == true)
                    {
                        for (k = 0; k < tabB4.Length; k++)
                        {
                            tab[i + k, j] = tabB4[k];
                        }
                    }
                }//il faut mettre un while !!! pou recommencer quand le test est faux !!!
            } while (test == false);
            do
            {
                if (choix == 0)
                {
                    int i = r.Next(10);
                    int j = r.Next(10 - tabB5.Length);
                    //teste si le tableau est vide là où on veut écrire
                    int k; //compteur de la taille du tableau du bateau
                    for (k = 0; k < tabB5.Length; k++)
                    {
                        if (tab[i, j + k] != 0)
                        {
                            test = false;

                        }

                        if (test == true)
                        {

                            tab[i, j + k] = tabB1[k];
                        }
                    }
                }
                else
                {
                    int j = r.Next(10);
                    int i = r.Next(10 - tabB5.Length);
                    //teste si le tableau est vide là où on veut écrire
                    int k; //compteur de la taille du tableau du bateau
                    for (k = 0; k < tabB5.Length; k++)
                    {
                        if (tab[i + k, j] != 0)
                        {
                            test = false;

                        }
                    }
                    if (test == true)
                    {
                        for (k = 0; k < tabB5.Length; k++)
                        {
                            tab[i + k, j] = tabB5[k];
                        }
                    }
                }//il faut mettre un while !!! pou recommencer quand le test est faux !!!
            } while (test == false);

        }



        /*
        static void DessinerPlateauJ1(char[,] tab, char[] tabB1, char[] tabB2, char[] tabB3, char[] tabB4, char[] tabB5)
        {
            InitialiserPlateau(tab, tabB1);
            //DessinerPlateau(tab);
            InitialiserPlateau(tab, tabB2);
            //DessinerPlateau(tab);
            InitialiserPlateau(tab, tabB3);
            //DessinerPlateau(tab);
            InitialiserPlateau(tab, tabB4);
            //DessinerPlateau(tab);
            InitialiserPlateau(tab, tabB5);
            //DessinerPlateau(tab);
        }*/


        static void Main(string[] args)
        {
            char[,] tabj1 = new char[10, 10];
            char[,] tabOrdi = new char[10, 10];

            //Création des bateaux
            char[] PA = { '#', '#', '#', '#', '#' }; //PorteAvion
            char[] Cuir = { '#', '#', '#', '#' }; //Cuirassé
            char[] SM = { '#', '#', '#' }; //SousMarin
            char[] Crois = { '#', '#', '#' }; //Croiseur
            char[] CT = { '#', '#' };//ContreTorpilleur

            /*DessinerPlateau(tabj1);
            Console.Write("\n");
            InitialiserPlateau(tabj1, PA);
            DessinerPlateau(tabj1);
            InitialiserPlateau(tabj1, Cuir);
            DessinerPlateau(tabj1);
            InitialiserPlateau(tabj1, SM);
            DessinerPlateau(tabj1);
            InitialiserPlateau(tabj1, Crois);
            DessinerPlateau(tabj1);
            InitialiserPlateau(tabj1, CT);
            DessinerPlateau(tabj1);*/
            DessinerPlateau(tabj1);

            //DessinerPlateauJ1(tabj1, PA, Cuir, SM, Crois, CT);
            InitialiserPlateau(tabj1, PA, Cuir, SM, Crois, CT);
            DessinerPlateau(tabj1);


            string reponse = "a";
            while ((reponse != "o") && (reponse != "n"))
            {
                Console.WriteLine("Le placement des bateaux vous convient-il ? (o/n)");
                reponse = Console.ReadLine();
                while (reponse == "n")
                {
                    InitialiserPlateau(tabj1, PA, Cuir, SM, Crois, CT);
                    DessinerPlateau(tabj1);
                }
            }




            Console.ReadKey();
        }
    }
}

