# gestion-etudiant-c-#include <iostream>
#include <string>

using namespace std;
class etudiant {
    public:
    string matricule;
    string nom;
    string prenom;
    unsigned int age;
    unsigned float note1,note2,note3;
    char sexe;
    etudiant* next;

    etudiant::etudiant(string m,string n,string p,unsigned int a,unsigned float (n1,n2,n3),char s) 
    : matricule(m), nom(n), prenom(p), sexe(s), age(a), note1(n1), note2(n2), note3(n3), suivant(nullptr) {}
};


class ListeEtudiants {
private:
    Etudiant* tete;

public:
    ListeEtudiants() : tete(nullptr) {}

    
    void ajouterEtudiant(string matricule, string nom, string prenom, char sexe, int age, float note1, float note2, float note3) {
        Etudiant* nouvelEtudiant = new Etudiant(matricule, nom, prenom, sexe, age, note1, note2, note3);
        if (!tete) {
            tete = nouvelEtudiant;
        } else {
            Etudiant* temp = tete;
            while (temp->suivant) {
                temp = temp->suivant;
            }
            temp->suivant = nouvelEtudiant;
        }
        cout << "Étudiant ajouté avec succès !" << endl;
    }

    
    void mettreAJourEtudiant(string matricule) {
        Etudiant* temp = tete;
        while (temp) {
            if (temp->matricule == matricule) {
                cout << "Entrez les nouvelles informations pour l'étudiant :" << endl;
                cout << "Nom : ";
                cin >> temp->nom;
                cout << "Prénom : ";
                cin >> temp->prenom;
                cout << "Sexe (M/F) : ";
                cin >> temp->sexe;
                cout << "Âge : ";
                cin >> temp->age;
                cout << "Note 1 : ";
                cin >> temp->note1;
                cout << "Note 2 : ";
                cin >> temp->note2;
                cout << "Note 3 : ";
                cin >> temp->note3;
                cout << "Étudiant mis à jour avec succès !" << endl;
                return;
            }
            temp = temp->suivant;
        }
        cout << "Étudiant avec le matricule " << matricule << " non trouvé !" << endl;
    }

    
    void supprimerEtudiant(string matricule) {
        if (!tete) {
            cout << "La liste est vide !" << endl;
            return;
        }

        if (tete->matricule == matricule) {
            Etudiant* aSupprimer = tete;
            tete = tete->suivant;
            delete aSupprimer;
            cout << "Étudiant supprimé avec succès !" << endl;
            return;
        }

        Etudiant* temp = tete;
        while (temp->suivant && temp->suivant->matricule != matricule) {
            temp = temp->suivant;
        }

        if (temp->suivant) {
            Etudiant* aSupprimer = temp->suivant;
            temp->suivant = temp->suivant->suivant;
            delete aSupprimer;
            cout << "Étudiant supprimé avec succès !" << endl;
        } else {
            cout << "Étudiant avec le matricule " << matricule << " non trouvé !" << endl;
        }
    }

    
    void afficherEtudiants() {
        if (!tete) {
            cout << "Aucun étudiant dans la liste." << endl;
            return;
        }
        Etudiant* temp = tete;
        while (temp) {
            cout << "Matricule: " << temp->matricule 
                 << ", Nom: " << temp->nom 
                 << ", Prénom: " << temp->prenom 
                 << ", Sexe: " << temp->sexe 
                 << ", Âge: " << temp->age 
                 << ", Notes: [" << temp->note1 << ", " << temp->note2 << ", " << temp->note3 << "]" 
                 << endl;
            temp = temp->suivant;
        }
    }

    
    ~ListeEtudiants() {
        Etudiant* temp = tete;
        while (temp) {
            Etudiant* suivant = temp->suivant;
            delete temp;
            temp = suivant;
        }
    }
};


int main() {
    ListeEtudiants liste;
    int choix;

    do {
        cout << "\nMenu :\n";
        cout << "1 - Ajouter un étudiant\n";
        cout << "2 - Mettre à jour un étudiant\n";
        cout << "3 - Supprimer un étudiant\n";
        cout << "4 - Afficher tous les étudiants\n";
        cout << "5 - Quitter\n";
        cout << "Votre choix : ";
        cin >> choix;

        switch (choix) {
            case 1: {
                string matricule, nom, prenom;
                char sexe;
                int age;
                float note1, note2, note3;
                cout << "Matricule : ";
                cin >> matricule;
                cout << "Nom : ";
                cin >> nom;
                cout << "Prénom : ";
                cin >> prenom;
                cout << "Sexe (M/F) : ";
                cin >> sexe;
                cout << "Âge : ";
                cin >> age;
                cout << "Note 1 : ";
                cin >> note1;
                cout << "Note 2 : ";
                cin >> note2;
                cout << "Note 3 : ";
                cin >> note3;
                liste.ajouterEtudiant(matricule, nom, prenom, sexe, age, note1, note2, note3);
                break;
            }
            case 2: {
                string matricule;
                cout << "Matricule de l'étudiant à mettre à jour : ";
                cin >> matricule;
                liste.mettreAJourEtudiant(matricule);
                break;
            }
            case 3: {
                string matricule;
                cout << "Matricule de l'étudiant à supprimer : ";
                cin >> matricule;
                liste.supprimerEtudiant(matricule);
                break;
            }
            case 4:
                liste.afficherEtudiants();
                break;
            case 5:
                cout << "Au revoir !" << endl;
                break;
            default:
                cout << "Choix invalide !" << endl;
        }
    } while (choix != 5);

    return 0;
}


}






