# Modificări și teste

## Buguri corectate

| # | Fișier | Problemă | Corecție |
|---|--------|----------|----------|
| 1 | src/pages/TaskDetails.jsx | După ștergerea unei sarcini, aplicația naviga la `/task` (rută inexistentă) și ajungea la Overview | Navigare la `/tasks` |
| 2 | src/pages/TaskDetails.jsx | La editare, `projectId` rămânea text (`"1"`) în loc de număr, iar sarcina își pierdea proiectul în liste | Conversie cu `Number(form.projectId)` |
| 3 | src/pages/Dashboard.jsx | Linkul „View all" ducea la `/task` (rută inexistentă) | Link către `/tasks` |
| 4 | src/pages/Dashboard.jsx | Contorul „In progress" arăta 0, deoarece compara cu `'In Progress'` în loc de `'In progress'` | Valoarea corectată la `'In progress'` |
| 5 | src/pages/Projects.jsx | Butonul „View project" ducea la `/project/:id`, ruta corectă fiind `/projects/:id` | Link către `/projects/:id` |
| 6 | src/pages/Tasks.jsx | Filtrul de status „In progress" nu returna nicio sarcină (conversie greșită la `'In Progress'`) | Comparare directă `task.status === status` |
| 7 | src/pages/Tasks.jsx | Căutarea după persoană ținea cont de litere mari/mici și putea da eroare dacă lipsea persoana | `(task.assignee \|\| '').toLowerCase().includes(query)` |
| 8 | src/components/TaskForm.jsx | Un titlu format doar din spații trecea de validare | Validare cu `!form.title.trim()` |
| 9 | src/pages/Dashboard.jsx, src/pages/Projects.jsx | La eroare de API, pagina rămânea goală, fără mesaj | Adăugat `.catch` și mesaj de eroare |
| 10 | src/components/TaskForm.jsx | Formularul putea fi trimis de mai multe ori (dublu-clic) și crea sarcini duplicate | Stare `submitting`, buton dezactivat în timpul salvării |

## Funcționalitate nouă

Filtrare după prioritate (Low / Medium / High) în pagina Tasks (`src/pages/Tasks.jsx`). Filtrul se combină cu filtrul de status și cu căutarea, iar butonul „Clear filters" îl resetează.

## Teste efectuate (manual)

- [x] Citire: Overview, lista de sarcini, detalii sarcină, Projects, detalii proiect
- [x] Creare: titlu gol, titlu din spații, dată lipsă (mesaje de eroare), creare validă
- [x] Actualizare: editarea unei sarcini, inclusiv schimbarea proiectului
- [x] Ștergere: sarcina dispare, redirecționare la `/tasks`
- [x] Navigare: meniu lateral, „View all", „View project", rută inexistentă (redirecționare la Overview)
- [x] Filtre: status, prioritate, combinație status + prioritate, „Clear filters"
- [x] Căutare: după titlu și după persoană, fără diferență între litere mari și mici
- [x] API oprit: se afișează mesaj de eroare pe Overview și Projects