//# Programme qui gére les patients d'un hopital//
#include <iostream>
#include <stdlib.h>
#include <stdio.h>
#include <conio.h>
#include <cstdio>
#include <string.h>
using namespace std;
typedef struct date
{
    int jour,mois,annee;
};
typedef struct patient
{
   string T[7],Nom,Prenom;
   int cle,Age;
   date daten;
   int np_symptome;
};
FILE * f9=NULL; // decleration hors de fonction pour les utiliser dans tout les fonctions //

int ajouter (FILE *f1, int j, char x[15])
{
char c,d;
int i=0;
patient z;
       if (x[1]=='1')
       {
           f9 = fopen ("setting.txt", "rt");
           fscanf (f9, "%s ", x);

           fclose(f9);
       }
      f1 = fopen (x, "ab"); // ouvrir le fichier en mode ecriture //
     do
     {
        z.cle=2022*1000+j+1;
        cout << " Veuillez enter le nom de patient " << endl;
        cin >> z.Nom;
        cout << " Veuillez enter le prenom de patient " << endl;
        cin >> z.Prenom;
        do
        {
        cout << " Veuillez enter l'age de patient " << endl;
        cin >> z.Age; }
        while ( z.Age<=0);

        cout << " Veuillez enter la date d'admission du patient " << endl;
        cout << "\n" << endl;
        do
        {
            cout << " Enter le jour " << endl;
            cin >> z.daten.jour;
        }
        while (z.daten.jour<=0 || z.daten.jour>=32 ); // boucle repeter pour le controle de saise //

        do
        {
            cout << " Enter le mois " << endl;
            cin >> z.daten.mois;
        }
        while (z.daten.mois<=0 || z.daten.mois>=13 ); // boucle repeter pour le controle de saise //

        do
        {
        cout << " Enter l'annee " << endl;
        cin >> z.daten.annee;
        }
        while ( z.daten.annee<=0);

         i=1;
         do
         {
              cout << " Enter le symptome de patient " << endl;
              cin >> z.T[i];
              i++;
           cout << " Vous vouelz ajouter un symptome , Taper '1' pour oui et '0' pour non  " << endl;
           cin >> d;
         }
        while(i<=7 && d=='1');
        z.np_symptome=i; // sauvegarder le nombre de symptome //

        fwrite (&z,sizeof(z),1,f1); // ecrire l'enregistrement dans le fichier //

      cout << " voulez vous ajouter un patient , Taper '1' pour oui et '0' pour non " << endl;
      cin >> c;
      j++;
     }

     while ( c=='1');

fclose(f1);
return (j); // Renvoie le nombre des patients ajoutées //

};

FILE * f6=NULL; // decleration hors de fonction pour les utiliser dans tout les fonctions //
 void mis_a (FILE *f1,int code5 , char x[15])
{
  int k,l=0;
  patient p,z;

  if (x[1]=='1')
       {
           f9 = fopen ("setting.txt", "rt");
           fscanf (f9, "%s ", x);

           fclose(f9);
       }

  f1=fopen (x, "rb");
  if (f1==NULL)
  {
      cout << " impossible d'ouvrir le fichier " << endl;

  }
  else
  {
      f6=fopen ("patient6.dat", "wb");
      while ( !feof(f1))
      {
        k=fread (&p,sizeof(p),1,f1);
        if (k==1) // la lecture correcte //
        {
          if ( p.cle==code5) // code5 c'est la cle de patient pour mettre a jour ces information //
          { l=1; // l=1 ca veut dire la mis a jour va etre effectuer avec succes //
                 // Remplir l'enregistrement par les nouvelles informations  dans f6 //
            cout << " Veuillez enter le nom de patient " << endl;
        cin >> p.Nom;
        cout << " Veuillez entrer le prenom de patient " << endl;
        cin >> p.Prenom;
        do
        {
        cout << " Veuillez entrer l'age de patient " << endl;
        cin >> p.Age; }
        while ( p.Age<=0);

        cout << " Veuillez entrer la date d'admission du patient " << endl;
        cout << "\n" << endl;
        do
        {
            cout << " Entrer le jour " << endl;
            cin >> p.daten.jour;
        }
        while (p.daten.jour<=0 || p.daten.jour>=32 );

        do
        {
            cout << " Entrer le mois " << endl;
            cin >> p.daten.mois;
        }
        while (p.daten.mois<=0 || p.daten.mois>=13 );

        cout << " Entrer l'annee " << endl;
        cin >> p.daten.annee;
         k=0;
         do
         {
              cout << " Entrer le symptome de patient " << endl;
              cin >> p.T[k];
              k++;
           cout << " Vous voulez ajouter un symptome , Taper '1' pour oui et '0' pour non  " << endl;
           cin >> z.cle;

         }
        while(k<=7 && z.cle);
        p.np_symptome=k;
        fwrite (&p,sizeof(p),1,f6); //
          }
          else
          {
            fwrite (&p,sizeof(p),1,f6);

          }
        }

      }
fclose(f6);
  }
fclose(f1);
  f6=fopen ("patient6.dat", "rb");
  if ( f6==NULL)
  {
      cout << " impossible d'ouvrir le fichier " << endl;

  }
  else
  {
      f1=fopen (x, "wb");
      while ( !feof(f6))
      {
          k=fread (&p,sizeof(p),1,f6);
          if (k==1) // la lecture correcte //
          {
              fwrite (&p,sizeof(p),1,f1); // ecraser  f1 par f6 //
          }
      }
      fclose(f1);
  }

  fclose(f6);
if (l==0)
{    // si l==0 alors la code de patient saiser par clavier n'est pas correct ou bien n'existe pas //
    cout << " Le patient n'existe pas " << endl;
    cout << " la mis a jour n'est pas effectue avec succes " << endl;
}
else
{ // l==1 //
   cout << " la mis a jour a ete effectue avec succes :) " << endl;
}

}

FILE *f2=NULL; // decleration hors de fonction pour les utiliser dans tout les fonctions //
FILE *f3=NULL;

void sortieguerison(FILE *f1, int code2, char x[15], char y[15] )
{
    int k,l=0;
    patient p;


     if (x[1]=='1')
       {
           f9 = fopen ("setting.txt", "rt");
           fscanf (f9, "%s ", x);
           fclose(f9);
       }
      if (y[1]=='1')
       { // lire deux fois le contenu de fichier setting.txt //
        f9 = fopen ("setting.txt", "rt");
        fscanf (f9, "%s ", y);
        fscanf (f9, "%s ", y); // récupérer le nom de fichier 02 //
        fclose(f9);
       }


    f1=fopen (x, "rb");
    if ( f1==NULL)
    {
        cout << " Impossible d'ouvrir le fichier " << endl;
    }
    else
    {
        f2=fopen (y, "ab"); // fichier geuris //
        f3=fopen (" patient3.dat ", "wb"); // fichier supplimentaire pour transferer les inforamtion du f1 vers f3 //
        while (!feof(f1))
        {
            k=fread (&p,sizeof(p),1,f1);
            if (k==1 ) // la lecture correcte //
            {
                if (p.cle==code2) // code2 c'est la cle de patient gueris  qui va sortir //
                {    l=1;
                    fwrite (&p,sizeof(p),1,f2); // copier le patient gueris vers fichier gueris ( f2)
                }
              else
            {
                fwrite (&p,sizeof(p),1,f3); // copier les informations de tout les patients a par le patient gueris vers f3 //
            }

            }

        }
        fclose(f2);
        fclose(f3);
    }
    fclose(f1);
    f3=fopen (" patient3.dat ", "rb");
      if (f3==NULL)
      {
          cout << " impossible d'ouvrir le fichier " << endl;
      }
      else
      {
          f1=fopen (x, "wb");
          while (!feof(f3))
          {
              k=fread (&p,sizeof(p),1,f3);
              if(k==1) // la lecture correcte //
              {
                  fwrite (&p,sizeof(p),1,f1); // ecraser f1 par f3 //
              }

          }
          fclose(f1);
      }
      fclose(f3);
      if (l==0)
      {
          cout << " CE PATIENT N'EXISTE PAS  " << endl;
      }

}

FILE *f4=NULL; // decleration hors de fonction pour les utiliser dans tout les fonctions //
FILE *f5=NULL;
void sortiedecede (FILE *f1, int code3, char x[15] , char z[15])
{
int a=0,k=0;
patient p;

f9 = fopen ("setting.txt", "rt");
     if (x[1]=='1')
       {
           fscanf (f9, "%s ", x);
       }


     if (z[1]=='1')
       { // lire deux fois le contenu de fichier setting.txt //
           fscanf (f9, "%s ", z);
           fscanf (f9, "%s ", z); // récupérer le nom de fichier 03
       }

f1=fopen (x, "rb");




if ( f1==NULL)
{
    cout << " Impossible d'ouvrir le fichier " << endl;
}
else
{
  f4=fopen (z, "ab"); // fichier decede //
  f5=fopen ("patient5.dat", "wb");// fichier supplimentaire pour transferer les inforamtion du f1 vers f5 a par la patient decede //
   while (!feof(f1))
   {
       k=fread (&p,sizeof(p),1,f1);
       if (k==1) // la lecture correcte //
       {
           if(p.cle==code3) // code3 c'est la cle de patient decede //
           { a=1; // la patient decede est trouve alors le patient existe //

               fwrite (&p,sizeof(p),1,f4); // ecrire ce patient dans fichier decede //
           }
           else
           {
            fwrite (&p,sizeof(p),1,f5); // sauvgarder tout les patients qui sont non decede vers f5 //
           }
       }

   }
   fclose(f4);
   fclose(f5);
}
fclose(f1);
f5=fopen ("patient5.dat", "rb");
if (f5==NULL)
{
 cout << " impossible d'ouvrir le fichier " << endl;

}
else
{
    f1=fopen (x, "wb");
    while (!feof(f5))
    {
    k=fread (&p,sizeof(p),1,f5);
    if(k==1) // la lecture correcte //
    {
    fwrite (&p,sizeof(p),1,f1); // ecraser f1 par f5 //
    }
    }
    fclose(f1);

}
fclose(f5);
if ( a==0)
{
    cout << " CE PATIENT N'EXISTE PAS  " << endl;
}

}



void afficherhospi (FILE *f1,int choix , char x[15])
{
int aage,k;
patient p,m;
string path;
date date1;

 if (x[1]=='1')
       {
           f9 = fopen ("setting.txt", "rt");
           fscanf (f9, "%s ", x);

           fclose(f9);
       }



f1= fopen (x, "rb");
if ( choix==1)
{
   // Affichage selon l'age //
  cout << " enter l'age " << endl;
  cin >> aage;
  if ( f1==NULL)
  {
      cout << " impossible d'ouvrir le fichier " << endl;
  }
  else
  {
      while ( !feof(f1))
             {
              k=fread (&p,sizeof(p),1,f1);
                    if ( k==1) // la lecture correcte
                    {
                        if (p.Age==aage )
                    { m.Age=1; // Une variable pour vérifier l'existance  d'un patient dans le fichier //
         cout << "La cle de patient est : " << p.cle << endl;
         cout <<"Le nom de patient est : " <<  p.Nom << endl;
         cout << "Le prenom de patient est : " << p.Prenom << endl;
         cout << "L'age de patient est : " << p.Age << " ans" <<endl;
         cout <<"La date d'admission de patient est : " << p.daten.jour<<"/"<<p.daten.mois<<"/"<<p.daten.annee << endl;
               cout << "\n";
                        }
                    }


             }


  }
   fclose(f1);

}
else
{
    if ( choix==2)
    {  // Affichage selon la pathologie //

        cout << " enter la pathologie " << endl;
        cin >> path;
        if( f1==NULL)
        {
            cout << "Impossible d'ouvrir le fichier " << endl;

        }
        else
        {
        while ( !feof(f1))
        {
            k=fread (&p,sizeof(p),1,f1);
           if (k==1) // la lecture correcte //
           {
            k=1;
            for(k=1;k<=p.np_symptome;k++)
            {
             if (p.T[k]==path)
             {
                  m.Age=1;  // Une variable pour vérifier l'existance  d'un patient dans le fichier //

         cout << "La cle de patient est : " << p.cle << endl;
         cout <<"Le nom de patient est : " <<  p.Nom << endl;
         cout << "Le prenom de patient est : " << p.Prenom << endl;
         cout << "L'age de patient est : " << p.Age << " ans" <<endl;
         cout <<"La date d'admission de patient est : " << p.daten.jour<<"/"<<p.daten.mois<<"/"<<p.daten.annee << endl;
               cout << "\n";
             }
            }

           }
        }
        }
        fclose(f1);

    }
    else
    {
        cout << " enter la date d'admission " << endl;
        cin >>date1.jour >> date1.mois >> date1.annee;
        if (f1==NULL)
        {
            cout << " impossible d'ouvrir le fichier  " << endl;

        }
        else
        {
            while (!feof(f1))
            {
                k=fread (&p,sizeof(p),1,f1);
                if (k==1) // la lecture correcte
                {  // Affichage selon la date d'admission //
                    if (p.daten.annee== date1.annee && p.daten.jour==date1.jour && p.daten.mois==date1.mois )
                    { m.Age=1; // Une variable pour vérifier l'existance  d'un patient dans le fichier //
                cout << "La cle de patient est : " << p.cle << endl;
                cout <<"Le nom de patient est : " <<  p.Nom << endl;
                cout << "Le prenom de patient est : " << p.Prenom << endl;
                cout << "L'age de patient est : " << p.Age << " ans" <<endl;
                cout <<"La date d'admission de patient est : " << p.daten.jour<<"/"<<p.daten.mois<<"/"<<p.daten.annee << endl;

                cout << "\n";
                    }
                }
            }
        }

    }


}
if (m.Age!=1 )
{
    cout << " Ce patient n'existe pas " << endl;
}

}


void affichergueris ( FILE *f2, char y[15])
{
int j=0,k;
patient p;

f9=fopen ("setting.txt", "rt");
if (y[1]=='1')
       {
        fscanf (f9, "%s ", y);
        fscanf (f9, "%s ", y);
       }
       fclose(f9);

f2=fopen (y, "rb");
if (f2==NULL)
{
    cout << "impossible d'ouvrir le fichier " << endl;

}
else
{
 while (!feof(f2))
 {
     k=fread (&p,sizeof(p),1,f2);
     if (k==1) // la lecture correcte //
     { // Afficher les patient geuris //
         j=1;
         cout << "La cle de patient est : " << p.cle << endl;
         cout <<"Le nom de patient est : " <<  p.Nom << endl;
         cout << "Le prenom de patient est : " << p.Prenom << endl;
         cout << "L'age de patient est : " << p.Age << " ans" <<endl;
         cout <<"La date d'admission de patient est : " << p.daten.jour<<"/"<<p.daten.mois<<"/"<<p.daten.annee << endl;
         cout << "Les symptomes de ce patient sont : ";
         for (j=1;j<=p.np_symptome;j++)
         {
          cout << p.T[j] << " " ;
         }
     }
   cout << "\n" << endl;
 }

}
if (j==0)
{
    cout << " Y'as aucun patient gueris  " << endl;
}
fclose(f2);
}

void afficherdecede ( FILE *f4, char z[15] )
{
    int j=0,k;
    patient p;

f9=fopen ("setting.txt", "rt");
if (z[1]=='1')
       {
        fscanf (f9, "%s ", z);
        fscanf (f9, "%s ", z);
        fscanf (f9, "%s ", z);

       }

       fclose(f9);

f4=fopen (z, "rb");
if ( f4==NULL )
{
    cout << " impossible d'ouvrir le fichier " << endl;

}
else
{
 while ( !feof(f4))
 {
     k=fread (&p,sizeof(p),1,f4);
     if (k==1) // la lecture correcte //
     {  // Afficher les patient decedes //
         j=1; // il existe des patients dans le fichier //
         cout << "La cle de patient est : " << p.cle << endl;
         cout <<"Le nom de patient est : " <<  p.Nom << endl;
         cout << "Le prenom de patient est : " << p.Prenom << endl;
         cout << "L'age de patient est : " << p.Age << " ans" <<endl;
         cout <<"La date d'admission de patient est : " << p.daten.jour<<"/"<<p.daten.mois<<"/"<<p.daten.annee << endl;
         cout << "Les symptomes de ce patient sont : ";
         for (j=1;j<=p.np_symptome;j++)
         {
          cout << p.T[j] << " " ;
         }
     }
    cout << "\n" << endl;
 }

    }
    if (j==0)
    {
        cout << " Y'as aucun patient decede " << endl;
    }
    fclose(f4);
}

void parametre( char a[15] , char b[15], char c[15])
{ int d=0;
  cout << " Voulez-vous changer le fichier 01 ? " << endl;
  cin >>d;
  if ( d==1)
  {
    cout << " entrer le nouveau nom de fichier " << endl;
    cin >> a;
  }
  d=0;
  cout << " Voulez-vous changer le fichier 02 ? " << endl;
  cin >>d;
  if ( d==1)
  {
    cout << " entrer le nouveau nom de fichier " << endl;
    cin >> b;
  }
  d=0;
  cout << " Voulez-vous changer le fichier 03 ? " << endl;
  cin >>d;
  if ( d==1)
  {
    cout << " entrer le nouveau nom de fichier " << endl;
    cin >> c;
  }


}

FILE * f8=NULL;

void filesetting (FILE *f8)
{
   char c[15];

   f8=fopen ("setting.txt", "wt");

   strcpy (c, "patient.dat");
   fprintf (f8, " %s ", c);
   strcpy (c, "gueris.dat");
   fprintf (f8, " %s ", c);
   strcpy (c, "decede.dat");
   fprintf (f8, " %s ", c);

   fclose(f8);

}



void showMenu();

int main(void)
{   FILE * f=NULL;

int nombre=0,code,b;    // b pour le choix d'affichage ( procedure 05 ) // // nombre : c'est le nombre des patients ajouter //
        // code : une variable pour le code des patients a afficher ou bien a mettre a jour //
    char c,x[15],y[15],z[15]; // X,Y,Z un tableau de carectere pour les nom  des fichier 01 , 02 , 03 //

        x[1]='1'; y[1]='1'; z[1]='1';
     filesetting(f8); // fonction qui register les noms des 3 fichiers dans fihcier setting //
    do
    {
        showMenu();
        cin>>c;
        switch(c)
        {
        case '1':
            system("cls");
            nombre=ajouter(f,nombre,x); // Renvoie la nombre des patients ajouter //
            cout << " Le nombre des patients ajouter dans ce fichier  est  " << nombre << endl;
            getche();
            break;
        case '2':
            system("cls");
            cout << " Entrer le code du patient " << endl;
            cin >> code;
            mis_a(f,code,x);
            getche();
            break;
        case '3':
            system("cls");
            cout << " Entrer le code du patient " << endl;
            cin >> code;
            sortieguerison(f,code,x,y);
            getche();
            break;
        case '4':
            system("cls");
            cout << " Entrer le code du patient " << endl;
            cin >> code;
            sortiedecede(f,code,x,z);
            getche();
            break;
        case '5':
            system("cls");
             cout << "           Menu      " << endl;
        cout << "                       " << endl;
        cout << " ################################## " << endl;
        cout << " 1. Affichage selon l'age " << endl;
        cout << " 2. Affichage selon une pathologie " << endl;
        cout << " 3. Affichage selon la date d'admission " << endl;
        cout << " ################################## " << endl;
        cout << "                     " << endl;
      do
      {
          cout << "       " <<  " Votre choix : " << endl;
          cin >> b;
      }
      while ( b>3 || b<=0);
            afficherhospi(f,b,x);
            getche();
            break;
        case '6':
            system("cls");
            affichergueris(f2,y);
            getche();
            break;
        case '7':
            system("cls");
            afficherdecede(f4,z);
            getche();
            break;
        case '8':
            system("cls");
            parametre(x,y,z);
            getche();
            break;
        case '9':
            cout<<"voulez vous quitter le programme o/n ??\n"<<endl;
            cin>>c;
            break;
        }
        system("cls");
    }
    while(c!='o');
    return 0;
}
void showMenu()
{
    cout<<"\n\n\n\n";
    cout<<"  #####################################################\n";
    cout<<"     1.  Ajouter  des patients."<<endl;
    cout<<"     2.  Mettre a jour les informations d'un patient. "<<endl;
    cout<<"     3.  Sortie d'un patient pour gu\202rison "<<endl;
    cout<<"     4.  Sortie d'un patient d\202c\202d\202 "<<endl;
    cout<<"     5.  Afficher les patients hospitalis\202s"<<endl;
    cout<<"     6.  Afficher les patients gu\202ris"<<endl;
    cout<<"     7.  Afficher les patients d\202c\202d\202s."<<endl;
    cout<<"     8.  param\212Atres"<<endl;
    cout<<"     9.  Quitter."<<endl;
    cout<<"  #####################################################"<<endl;
    cout<<"\t Votre choix :   "<<endl;
}
