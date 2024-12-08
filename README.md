#include <stdio.h>
#include <stdlib.h>
typedef struct element {
    int val;
    struct element *suivant;
} element;
element *creerListe() {
    return NULL;
}
element *chargerListe(int Tab[], int n, element *liste) {
    element *nouveau, *courant;
    int i;
    for (i = 0; i < n; i++) {
        nouveau = (element *)malloc(sizeof(element));
        nouveau->val = Tab[i];
        nouveau->suivant = NULL;
        if (liste == NULL) {
            liste = nouveau;
            courant = nouveau;
        } else {
            courant->suivant = nouveau;
            courant = nouveau;
        }
    }
    return liste;
}
void afficherListe(element *L) {
    while (L != NULL) {
        printf("%d -> ", L->val);
        L = L->suivant;
    }
    printf("NULL\n");
}
element *supprimerEnFin(element *L) {
    if (L == NULL || L->suivant == NULL) {
        free(L);
        return NULL;
    }
    element *courant = L;
    element *precedent = NULL;
    while (courant->suivant != NULL) {
        precedent = courant;
        courant = courant->suivant;
    }
    free(courant);
    if (precedent != NULL) {
        precedent->suivant = NULL;
        return L;
    } else {
        return NULL;
    }
}
element *ajouterEnDebut(element *L1, int valeur) {
    element *nouveau = (element *)malloc(sizeof(element));
    nouveau->val = valeur;
    nouveau->suivant = L1;
    return nouveau;
}
void viderListe(element *L) {
    while (L != NULL) {
        element *temp = L;
        L = L->suivant;
        free(temp);
    }
    printf("La liste est vide\n");
}
int main() {
    int Tab[10] = {1, 3, 5, 7, 8, 10, 9, 11, 13, 20};
    element *liste = creerListe();
    element *L = chargerListe(Tab, 10, liste);
    printf("Liste initiale:\n");
    afficherListe(L);
    element *L1 = supprimerEnFin(L);
    printf("Liste apres suppression en fin:\n");
    afficherListe(L1);
    element *L2 = ajouterEnDebut(L1, 40);
    printf("Liste apres ajout en debut de 40:\n");
    afficherListe(L2);
    viderListe(L2);
    return 0;
}
