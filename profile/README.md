
## Numele și grupa membrilor echipei:
- Amza Andreea-Georgiana 343C3
- Cioban George-Adrian 343C3
- Damian Robert-Eugen 342C2
- Vasile Patricia 343C3
 
## Descrierea tematicii și funcționalităților aplicației 

Aceasta este o aplicatie de tip e-commerce/e-shop prin care utilizatorii au oportunitatea de a achizitiona diverse culori (printre multe altele rosu, verde sau chiar albastru). 
Arhitectura aplicatiei este una bazata pe microservicii, printre care notam:
- autentificare
- baza de date
- utilitar pentru baza de date
- serviciu ce face management pe catalogul de produse
- serviciu ce valideaza si proceseaza comenzi
- serviciu de file storage (Minio) pentru stocarea pozelor produselor
- serviciu ce serveste interfata utilizatorului
Prima interactiune a utilizatorului cu aceasta platforma este serviciul de autentificare prin care acesta se poate loga fie ca simplu utilizator ce poate achizitiona culori, fie ca administrator ce poate adauga noi produse sau poate modifica pagina unui produs existent. 
 
In urma logarii utilizatorul poate accesa catalogul magazinului dar dispune si de o bara de cautare.pentru o filtrare minimalista a produselor.
Din acest punct utilizatorul poate selecta un produs si ajunge pe pagina acestuia unde sunt oferite mai multe detalii si exista si un buton de add to cart. 
In momentul apasarii butonului de add to cart se face o verificare a stocului si produsul este rezervat o perioada limitata de timp. Daca utilizatorul se duce pe pagina cosului propriu de cumparaturi si decide sa achizitoneze produsul acesta trebuie sa isi completeze datele de livrare, plata facandu-se exclusiv ramburs.

Diagrama arhitecturala a aplicatiei

![](https://i.imgur.com/HnxAHYc.png)

## Descrierea componentelor aplicatiei si a tehnologiilor utilizate
### API Gateway 
Așa cum este specificat și în cerințele proiectului vom avea un API Gateway, singurul către care clientul face request-uri. Aceasta componenta se ocupă cu rutarea și transmiterea mai departe a requesturilor către microservicii astfel toate request-urile client side pot fi făcute către o singura adresa.

### Auth
Acest microserviciu realizeaza autentificarea utilizatorilor pe baza unei parole si a unui nume de utilizator, transmite un JWT asociat sesiunii pe baza datelor valide, adauga datele de inregistrare in baza de date in momentul inregistrarii unui utilizator nou, precum si valideaza un JWT existent, validitate necesara microserviciilor de comenzi si produse. Componenta va fi implementata in Node.js.

### Stocare de fisiere
Serviciul de File Storage va fi implementat cu ajutorul MinIO, care este un Object Storage ce este compatibil cu Amazon S3. În acesta vom reține imaginile produselor noastre, urmand ca dupa upload link-ul sa fie introdus în baza de date in tabela specifica produsului. Ca și limbaj de programare am ales JavaScript, urmand sa folosim Client API-ul specific.

### Database și ORM
Pentru partea de stocare am ales sa folosim PostgreSQL împreuna cu Prisma pentru partea de ORM pentru a ne ușura lucrul cu baza de date.

### Product service
Acest serviciu se ocupă de verificarea inventarului atunci cand se cere validarea unei comenzi, sa obținem o lista a produselor din catalog dar și să obținem detalii despre un anumit produs specific pentru a le afișa pe o pagina proprie produsului. Pentru aceasta componenta vom folosi Node.js.

### Order service
Microserviciul de comenzi de culori pe care am ales sa il implementam folosind Express.js, un framework popular pentru crearea de RESTful API uri cu Node.js, va gestiona urmatoarele functionalitati: Microserviciul de comenzi va gestiona următoarele funcționalități:
Crearea de comenzi: Clienții pot plasa comenzi prin adăugarea culorii dorite în coșul de cumpărături și finalizarea procesului de checkout. Microserviciul va valida datele, cum ar fi disponibilitatea produsului și informațiile de plată (prin ramburs), și va crea o nouă comandă în sistem.
Modificarea stării comenzii
Interacțiunea cu alte microservicii

### FrontEnd server
Aceasta componenta servește o interfata grafica utilizatorului din care se pot efectua request-uri către celelalte servicii.

### Portainer
Vom folosi Portainer, care ofera o interfata grafica web pentru gestionarea containerelor.
Portainer este o soluție open-source de gestionare a containerelor, care oferă o interfață grafică web ușor de utilizat pentru administrarea și monitorizarea mediilor Docker.. 

### Swarm
Docker Swarm este o solutie nativa de clustering si orchestrare pentru Docker, care ne permite sa cream si gestionam un swarm de noduri Docker pe care sa ne desfasuram serviciile. 

O scurtă descriere a responsabilităților fiecărui membru al echipei în cadrul proiectului
### Amza Andreea-Georgiana 343C3
- Setup Database, ORM, Portainer
- File storage microservice
- Frontend tasks
### Cioban George-Adrian 343C3
- Setup API Gateway
- Product microservice
- Frontend tasks
- Creere organizatie GitHub și repository-uri
### Damian Robert-Eugen 342C2
- Setup swarm
- Auth microservice
- Frontend tasks
### Vasile Patricia 343C3
- Setup Database, ORM, Portainer
- Order microservice
- Frontend Tasks

> Nota: În timpul discuțiilor am stabilit ca alocarea de mai sus reprezinta mai mult un “ownership” pe o anumita componenta insa toti membrii echipei vor trece mai mult sau mai puțin prin toate componentelor, fie la debugging fie la adaugare de features
