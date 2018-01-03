# IPROG
Projet Info S5


            //Initialisation du plateau de l'IA
            Console.WriteLine("PLATEAU DE L'IA");
            for (int k = 0; k < 5; k++)
            {
                tabOrdi[3 + k, 0] = PA[k];
            }
            DessinerPlateau(tabOrdi);
            Console.WriteLine("\n \n");


            //Déroulement de la partie
            int nbBateauCoulé = 0;
            int nbTirDispo = 5 - nbBateauCoulé;
            Console.WriteLine("C'est votre tour. Sur quelle case voulez-vous tirer ? \n Vous avez le droit à {0} tir(s).", nbTirDispo);


            
            for (int nbTir = 0; nbTir < 5; nbTir++)
            {
                Console.WriteLine("C'est votre tir n°{0}.", (nbTir + 1));

                string saisieCase;
                do
                {
                    saisieCase = Console.ReadLine();
                } while (saisieCase.Length > 3);

                char saisieColonne = saisieCase[0];
                //while ((saisieColonne != 'A') )//&& (saisieColonne != "B") && (saisieColonne != "C") && (saisieColonne != "D") && (saisieColonne != "E") && (saisieColonne != "F") && (saisieColonne != "G") && (saisieColonne != "H") && (saisieColonne != "I") && (saisieColonne != "J"))
                //{
                //Console.Write("Colonne ? ");
                //saisieColonne = Console.ReadLine();
                //}
                int colonne = -3;
                if (saisieColonne == 'A')
                { colonne = 0; }
                /*else if ( saisieColonne == "B")
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
                { colonne = 9; }*/
                Console.Write("Colonne : ", colonne);

                /*int ligne = 11;
                while ((ligne<0)||(ligne>9))*/
                int ligne = 0;
                for (int l=0;l < saisieCase.Length;l++)
                { Console.WriteLine(saisieCase[l]); }
                Console.ReadKey();
                char saisieLigne = saisieCase[1];//Console.ReadLine();
                ligne = Convert.ToInt16(saisieLigne);
                //while ((ligne < 0) || (ligne > 9))
                //{
                    //Console.Write("Ligne ? ");
                    saisieLigne = saisieCase[1];//Console.ReadLine();
                    ligne = Convert.ToInt16(saisieLigne);
                //}                
                ligne--;//pour que le numéro de ligne entré corresponde à la bonne ligne du plateau
                Console.Write("Ligne : ", ligne);
                
                 
               

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
                }
                else if ((tabOrdi[ligne, colonne] == 'O') || (tabOrdi[ligne, colonne] == 'X'))
                { Console.WriteLine("Attention ! Vous aviez déjà tiré à cet endroit."); } // ATTENTION ! DEPEND DU MODE DE JEU

            }
