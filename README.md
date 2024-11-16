# Lucrarea de laborator Nr. 4. Formulare și validarea datelor

## Scopul lucrării
Familiarizarea cu elementele de bază ale creării și gestionării formularelor în Laravel.

Deprinderea mecanismelor de validare a datelor pe server, utilizarea regulilor de validare predefinite și personalizate, precum și învățarea gestionării erorilor și asigurarea securității datelor.

## Condiții
În această lucrare de laborator, vom crea formulare HTML, vom implementa verificarea datelor pe partea de server și asigura interacțiunea sigură cu utilizatorul, prevenind vulnerabilități precum XSS și CSRF.


## №1. Pregătirea lucrării
1. Creați un proiect nou Laravel (dacă nu este deja instalat) sau continuați cu proiectul anterior.
2. Actualizați variabilele de mediu în .env, dacă este necesară conectarea la o bază de date.
## №2. Crearea formularului
Creați un formular pentru adăugarea unei sarcini noi:
Formularul trebuie să conțină următoarele câmpuri: Titlu, Descriere, Data limită, Categorie.
Folosiți șabloanele Blade pentru a reda formularul.
Câmpul Categorie trebuie să fie o listă derulantă, încărcată din tabelul de categorii din baza de date.
Asigurați-vă că formularul trimite date prin metoda POST către o rută creată pentru procesarea datelor.
Creați ruta POST /tasks pentru salvarea datelor din formular în baza de date. Pentru ușurință, puteți folosi un controller de tip resursă.
Actualizați controllerul TaskController:
Adăugați metoda create, care returnează vizualizarea cu formularul.
Adăugați metoda store, care procesează datele din formular și le salvează.
