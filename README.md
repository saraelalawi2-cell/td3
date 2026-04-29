#include <stdio.h>
#include <stdlib.h>

/* Structure d'un noeud */
typedef struct Noeud {
    int valeur;
    struct Noeud* suivant;
} Noeud;

/* Ajouter un élément à la fin de la liste */
Noeud* ajouterFin(Noeud* tete, int val) {
    Noeud* nouveau = (Noeud*) malloc(sizeof(Noeud));
    nouveau->valeur = val;
    nouveau->suivant = NULL;

    // si la liste est vide
    if(tete == NULL) {
        return nouveau;
    }

    // aller jusqu'au dernier noeud
    Noeud* courant = tete;
    while(courant->suivant != NULL) {
        courant = courant->suivant;
    }

    courant->suivant = nouveau;
    return tete;
}

/* Fonction de fusion */
Noeud* fusionner(Noeud* A, Noeud* B) {
    Noeud* C = NULL;

    // fusion alternée
    while(A != NULL && B != NULL) {
        C = ajouterFin(C, A->valeur);
        C = ajouterFin(C, B->valeur);

        A = A->suivant;
        B = B->suivant;
    }

    // ajouter le reste de A
    while(A != NULL) {
        C = ajouterFin(C, A->valeur);
        A = A->suivant;
    }

    // ajouter le reste de B
    while(B != NULL) {
        C = ajouterFin(C, B->valeur);
        B = B->suivant;
    }

    return C;
}

/* Afficher une liste */
void afficher(Noeud* tete) {
    while(tete != NULL) {
        printf("%d -> ", tete->valeur);
        tete = tete->suivant;
    }
    printf("NULL\n");
}

int main() {
    Noeud *A = NULL, *B = NULL, *C = NULL;
    int m, n, i, x;

    // saisie taille liste A
    printf("Entrer la taille de la liste A : ");
    scanf("%d", &m);

    // remplissage liste A
    for(i = 0; i < m; i++) {
        printf("A[%d] = ", i + 1);
        scanf("%d", &x);
        A = ajouterFin(A, x);
    }

    // saisie taille liste B
    printf("Entrer la taille de la liste B : ");
    scanf("%d", &n);

    // remplissage liste B
    for(i = 0; i < n; i++) {
        printf("B[%d] = ", i + 1);
        scanf("%d", &x);
        B = ajouterFin(B, x);
    }

    // affichage des listes
    printf("\nListe A : ");
    afficher(A);

    printf("Liste B : ");
    afficher(B);

    // fusion
    C = fusionner(A, B);

    // affichage résultat
    printf("Liste C (fusion) : ");
    afficher(C);

    return 0;
}
