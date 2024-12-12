# Lucrarea de laborator Nr. 4. Formulare și validarea datelor

## Scopul lucrării
Familiarizarea cu elementele de bază ale creării și gestionării formularelor în Laravel.

Deprinderea mecanismelor de validare a datelor pe server, utilizarea regulilor de validare predefinite și personalizate, precum și învățarea gestionării erorilor și asigurarea securității datelor.

## Condiții
În această lucrare de laborator, vom crea formulare HTML, vom implementa verificarea datelor pe partea de server și asigura interacțiunea sigură cu utilizatorul, prevenind vulnerabilități precum XSS și CSRF.



## №1. Pregătirea lucrării
1. Cream un proiect nou Laravel (dacă nu este deja instalat) sau continuam cu proiectul anterior.
2. Actualizam variabilele de mediu în `.env`, dacă este necesară conectarea la o bază de date.


   
## №2. Crearea formularului
1. Cream un formular pentru adăugarea unei sarcini noi:
 - Formularul trebuie să conțină următoarele câmpuri: `Titlu`, `Descriere`, `Data limită`, `Categorie`.
 - Folosiți șabloanele Blade pentru a reda formularul.
 - Câmpul `Categorie` trebuie să fie o listă derulantă, încărcată din tabelul de categorii din baza de date.
 - Ne siguram că formularul trimite date prin metoda POST către o rută creată pentru procesarea datelor.
2. Creați ruta `POST /tasks` pentru salvarea datelor din formular în baza de date. Pentru ușurință, puteți folosi un controller de tip resursă.
3. Actualizați controllerul `TaskController`:
 - Adăugam metoda `create`, care returnează vizualizarea cu formularul.
 - Adăugam metoda `store`, care procesează datele din formular și le salvează.



## №3. Validarea datelor pe partea de server
1. Implementam validarea datelor direct în metoda store a controllerului `TaskController`.
2. Cerințele pentru câmpuri:
 - `title` — obligatoriu, șir de caractere, lungime minimă de 3 caractere.
 - `description` — șir de caractere, opțional, lungime maximă de 500 de caractere.
 - `due_date` — obligatoriu, dată, trebuie să fie cel puțin data de astăzi.
 - `category_id` — obligatoriu, trebuie să existe în tabelul categories.
3. Gestionam erorile de validare și returnați-le la formular, afișând mesajele de eroare lângă câmpuri.
4. Verificam funcționarea corectă a validării și asigurați-vă că erorile sunt afișate corect.



## №4. Crearea unei clase de cerere personalizată (Request)
1. În a doua etapă, cream o clasă personalizată de cerere pentru validarea formularului sarcinii:
 - Folosim comanda php artisan make: `request CreateTaskRequest`
 - În clasa `CreateTaskRequest`, definim regulile de validare similare celor din controller.
 - Actualizam metoda `store` a controllerului `TaskController` pentru a folosi `CreateTaskRequest` în loc de `Request`.
   
2. Adăugam logica de validare pentru datele asociate

Verificați că valoarea `category_id` există efectiv în baza de date și aparține unei categorii specificate.

3. Ne asiguram că datele trec prin validarea `TaskRequest` și că toate erorile sunt gestionate corect și returnate la formular.



## №5. Adăugarea mesajelor flash
1. Actualizam formularul HTML pentru a afișa un mesaj de confirmare la salvarea cu succes a sarcinii (mesaj flash).
2. Actualizam metoda `store` a controllerului `TaskController` pentru a adăuga un mesaj flash la salvarea cu succes a sarcinii.


   
## №6. Protecția împotriva CSRF
1. Asigurarea securității datelor din formulare:
 - Adăugam directiva `@csrf` în formular pentru protecția împotriva atacurilor **CSRF**.
 - Ne asiguram că formularul este trimis doar prin metoda **POST**.


## №7. Actualizarea sarcinii
1. Adăugam posibilitatea de editare a sarcinii:
 - Cream un formular pentru editarea sarcinii.
 - Cream o nouă clasă Request `UpdateTaskRequest` cu reguli de validare similare.
 - Cream ruta `GET /tasks/{task}/edit` și metoda `edit` în controllerul `TaskController`.
 - Cream ruta `PUT /tasks/{task}` pentru actualizarea sarcinii.
 - Actualizam metoda `update` în controllerul `TaskController` pentru a procesa datele din formular.



## Sarcină suplimentară
1. Cream o regulă personalizată de validare pentru a verifica că `description` nu conține cuvinte interzise.
2. Folosim comanda Artisan: `php artisan make:rule NoRestrictedWords`.
3. Aplicam această regulă câmpului `description` în clasa `CreateTaskRequest`.


## Întrebări de control

**1. Ce este validarea datelor și de ce este necesară?**

Validarea datelor este procesul de verificare a datelor introduse de utilizatori pentru a se asigura că sunt corecte, complete și conforme cu cerințele aplicației. 

Este necesară pentru:
 - Prevenirea erorilor și problemelor tehnice.
 - Protecția împotriva atacurilor (ex. injecții SQL).
 - Asigurarea unei experiențe bune pentru utilizator.

**2. Cum se asigură protecția formularului împotriva atacurilor CSRF în Laravel?**

Laravel generează automat un token CSRF unic pentru fiecare sesiune a utilizatorului. Acest token este inclus în formulare și verificat la primirea cererilor POST. Dacă tokenul nu este valid, cererea este respinsă. Funcția @csrf în blade include acest token în formulare.

**3. Cum se creează și utilizează clasele personalizate de cerere (Request) în Laravel?**

Se folosește comanda  `php artisan make:request NumeRequest`.

În metoda `rules()` din clasa generată, se definesc regulile de validare. Această clasă se injectează automat în metodele de controler, de exemplu:

**4. Cum se protejează datele împotriva atacurilor XSS la afișarea în vizualizare?**

Laravel protejează automat datele afișate utilizând funcția `htmlspecialchars()` prin sintaxa Blade `{{ $variable }}`. Pentru a afișa HTML sigur, se folosește sintaxa `{!! $variable !!}`, dar cu precauție și numai pentru date curate.
