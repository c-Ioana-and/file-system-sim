# file-system-sim

Această aplicație are ca scop simularea unui sistem de fișiere folosind arbori binari de căutare. Pentru simplificare, avem în vedere doar legăturile dintre directoare si fișiere, precum
și ierarhia lor.

Fiecare director are următoarea structură:
- nume (șir de caractere)
- părinte (pointer către directorul părinte)
- fișier (pointer către rădăcina arborelui de fișiere)
- directories (pointer către rădăcina arborelui de subdirectoare)
- st (pointer către următorul director cu nume mai mic lexicografic decât el)
- dr (pointer către următorul director cu nume mai mare lexicografic decât el)
  
Iar pentru fișiere:
- nume (șir de caractere)
- părinte (pointer către directorul de care aparține)
- st (pointer către următorul fișier cu nume mai mic lexicografic decât el)
- dr (pointer către următorul fișier cu nume mai mare lexicografic decât el)

## Implementare

  Am folosit in aceasta implementare arborii binari de cautare, initializand
inainte de orice operatie/task un director parinte (root), precum si un pointer
la directorul curent (denumit tot curent in program).
  Pentru efectuarea comenzilor am folosit doua variabile: _command_ pentru
retinerea task-ului de efectuat, si _nume_ pentru retinerea numelor fisierelor
sau directoarelor.

- Pentru adaugarea unui fisier, am apelat mai intai functia CautaDirArb care
cauta in directorul curent un director cu numele fisierului dat. Daca exista un
director cu acelasi nume, nu pot creea fisierul. Altfel, apelez functia
InserareFisier care insereaza fisierul in arborele de fisiere al folder-ului
curent, avand grija sa nu adaug duplicate si sa eliberez memoria in acest caz.
    
- Pentru adaugarea de directoare, am apelat functia CautaFisier pentru a
verifica daca exista deja un fisier cu acel nume. Daca da, nu creez fisierul.
Altfel, apelez functia InserareSubdirector care adauga directorul in arborele
de subdirectoare din folder-ul curent.
    
- Pentru afisarea subdirectoarelor si fisierelor din folder-ul curent, am
apelat functia SRD pentru cei doi arbori din directorul curent care ii parcurge
in ordinea stanga-radacina-dreapta (pentru o afisare lexicografica).
    
- Pentru instructiunea cd: Daca numele dat este "..", mut pointerul curent
la directorul parinte al folder-ului in care ma aflu. Altfel, caut folder-ul
cu numele dat si, daca il gasesc, mut pointerul curent la directorul gasit.
Daca nu l-am gasit, afisez "Directory not found".
    
- Pentru comanda pwd, am folosit o functie cu acelasi nume care parcurge
invers arborele, de la folder-ul curent la root, folosind pointerul catre
parintele directorului (din structura directorului, setat la fiecare inserare).
    
- Pentru comanda rm, caut fisierul in directorul curent si, daca l-am gasit,
apelez functia StergereFisier, care sterge acel fisier daca nu este radacina
arborelui de fisiere.
    Daca fisierul este radacina, functia fie va returna adresa subarborelui
ramas dupa eliminare (stang sau drept, dupa caz, daca fisierul are un singur
copil), fie va interschimba valoarea din radacina cu cea minima din subarborele
drept si va sterge nodul in care se afla valoarea minima.
   
- Analog si pentru rmdir, doar ca elimin subdirectoare si continutul lor
folosind functia DistrArb, care asigura ca si arborii de subdirectoare si
fisiere vor fi eliminati.
    
- Pentru comanda find, am creat doua functii, FindFisier si FindDir, care
cauta in toate subdirectoarele fisierul/directorul dat.
    La comanda quit distrug directorul root impreuna cu toate subdirectoarele
si fisierele create.
