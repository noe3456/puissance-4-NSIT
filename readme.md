PUISSANCE 4

Description rapide: Le projet que je vais présenter consiste à réaliser le jeu du puissance 4 sur python. Il y aura deux manières différentes de jouer dans mon puissance 4, vous pourrez jouer à deux joueurs ou encore affronter un ordinateur. Le but de ce jeu est d’aligner quatres jetons de sa couleur (verticalement,horizontalement ou en diagonale) sur un plateau de jeu. L’ordinateur aura plusieurs niveaux de difficultés. A chaque fin de partie il y aura un tableau des scores où sera affiché le nombre de parties gagnées pour chaque joueur.

**Objectif de Base:**
- Afficher un plateau de jeu ( 6 lignes x 7 lignes), et le mettre a jour apres chaque tour 
- Permet aux joueurs de placer leur jeton tour à tour dans la colonne du plateau qu’ils souhaitent
- Vérifie à chaque tour si un joueur a gagné et s’il n’y a pas égalité ( plateau plein et sans gagnant )
- Affichage d’un tableau des scores à la fin de la partie
- Création d’un programme qui permet à l’ordinateur de jouer le second joueur
</div>

**Entrées:**

- Entrer son nom de joueur
- Choix du mode jeu (ordinateur ou partie local)
- Choisir niveau de difficulté ( si jouer contre ordinateur)
- La colonne choisie par le joueur pour chaque tour de jeu


**Liste des fonctions :**


 1. MODÉLISATION DU PLATEAU
def init_plateau():
    """Crée une grille vide de 6 lignes × 7 colonnes."""
    lignes, colonnes = 6, 7
    plateau = [[" " for _ in range(colonnes)] for _ in range(lignes)]
    return plateau



 2. AFFICHAGE DU PLATEAU


def afficher_plateau(plateau):
    """Affiche le plateau dans la console."""
    print("\n  1   2   3   4   5   6   7")
    print("+" + "---+" * 7)
    for ligne in plateau:
        print("| " + " | ".join(ligne) + " |")
        print("+" + "---+" * 7)
    print()



 3. SAISIE UTILISATEUR


def demander_colonne(joueur):
    """Demande au joueur de choisir une colonne (1-7)."""
    while True:
        try:
            col = int(input(f"Joueur {joueur}, choisis une colonne (1-7) : ")) - 1
            if col in range(7):
                return col
            else:
                print("⚠️  Colonne invalide. Choisis entre 1 et 7.")
        except ValueError:
            print("⚠️  Entrée non valide. Entre un nombre entre 1 et 7.")



 4. PLACEMENT DES PIONS


def placer_pion(plateau, col, symbole):
    """Place le pion du joueur dans la colonne choisie."""
    for ligne in reversed(plateau):
        if ligne[col] == " ":
            ligne[col] = symbole
            return True
    print("⚠️  Cette colonne est pleine. Essaie une autre.")
    return False



 5. VÉRIFICATION DES CONDITIONS DE VICTOIRE


def est_victoire(plateau, symbole):
    """Vérifie si le joueur avec ce symbole a gagné."""
    lignes, colonnes = 6, 7

    # Horizontal
    for i in range(lignes):
        for j in range(colonnes - 3):
            if all(plateau[i][j + k] == symbole for k in range(4)):
                return True

    # Vertical
    for i in range(lignes - 3):
        for j in range(colonnes):
            if all(plateau[i + k][j] == symbole for k in range(4)):
                return True

    # Diagonale ↘
    for i in range(lignes - 3):
        for j in range(colonnes - 3):
            if all(plateau[i + k][j + k] == symbole for k in range(4)):
                return True

    # Diagonale ↙
    for i in range(3, lignes):
        for j in range(colonnes - 3):
            if all(plateau[i - k][j + k] == symbole for k in range(4)):
                return True

    return False



 6. VÉRIFICATION DU MATCH NUL


def est_plein(plateau):
    """Retourne True si le plateau est plein."""
    return all(cellule != " " for ligne in plateau for cellule in ligne)


 7. PROGRAMME PRINCIPAL


def puissance4():
    """Boucle principale du jeu."""
    plateau = init_plateau()
    joueur = 1
    symbole_joueur = {1: "X", 2: "O"}

    print("\n=== 🎮 PUISSANCE 4 🎮 ===")
    afficher_plateau(plateau)

    while True:
        col = demander_colonne(joueur)
        if placer_pion(plateau, col, symbole_joueur[joueur]):
            afficher_plateau(plateau)

            if est_victoire(plateau, symbole_joueur[joueur]):
                print(f"🏆 Joueur {joueur} ({symbole_joueur[joueur]}) a gagné !")
                break
            elif est_plein(plateau):
                print("🤝 Match nul !")
                break

            joueur = 2 if joueur == 1 else 1



 8. LANCEMENT DU JEU


if __name__ == "__main__":
    puissance4()










