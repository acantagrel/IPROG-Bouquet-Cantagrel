static void tirer (string saisieColonne, int ligne, char[,] tableau)
        {
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

            if (tableau[ligne, colonne] == 0)
            {
                tableau[ligne, colonne] = 'O'; //raté, tir dans l'eau
                Console.WriteLine("Raté !");
            }
            else
                        if (tableau[ligne, colonne] == '#')//cad sur un bateau
            {
                tableau[ligne, colonne] = 'X'; //touché
                Console.WriteLine("Touché !");
            }
            else if ((tableau[ligne, colonne] == 'O') || (tableau[ligne, colonne] == 'X'))
            { Console.WriteLine("Attention ! Vous aviez déjà tiré à cet endroit."); } // ATTENTION ! DEPEND DU MODE DE JEU

        }
