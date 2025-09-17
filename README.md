Database università


Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:
sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
ogni Corso può essere tenuto da diversi Insegnanti;
ogni Corso prevede più appelli d'Esame;
ogni Studente è iscritto ad un solo Corso di Laurea;
ogni Studente può iscriversi a più appelli di Esame;
per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente.
Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

Utilizzare https://www.drawio.com/ per la creazione dello schema.
Esportare quindi il diagramma in jpg e caricarlo nella repo.


--------------------------

Dopo aver creato un nuovo database nel vostro MySQL Workbench e aver importato lo schema allegato, eseguite le query del file allegato.

Cosa consegnare?
Dopo aver testato le vostre query con MySQL Workbench, riportatele in un file txt e caricatelo nella vostra repo. (E' la stessa di venerdì)

Consigli
Se vi bloccate su una query, non perdeteci troppo tempo, andate avanti alle successive. Per alcune sarà necessario fare un minimo di ricerca nella documentazione


1. Contare quanti iscritti ci sono stati ogni anno

SELECT `enrolment_date` AS `anno`, COUNT(*) AS `numero_iscritti`
FROM `students`
GROUP BY `enrolment_date`
ORDER BY `anno`



2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT LEFT(`office_address`, 1) AS edificio, COUNT(*)
FROM `teachers`
GROUP BY edificio
ORDER BY edificio



3. Calcolare la media dei voti di ogni appello d'esame

SELECT AVG(vote) AS `media_voti`
FROM `exam_student`




4. Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECT COUNT(*) 
FROM `degrees`
GROUP BY `department_id` 


1. Selezionare tutti gli studenti nati nel 1990 (160)

SELECT * 
FROM `students`
WHERE YEAR(date_of_birth) = 1990


2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

SELECT *
FROM courses
WHERE cfu > 10


3. Selezionare tutti gli studenti che hanno più di 30 anni

SELECT *
FROM students
where year (curdate()) - year(date_of_birth) > 30


4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)

SELECT * 
FROM courses
where period = 'I semestre' and year = 1


5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)

SELECT * 
FROM exams
where date = '2020-06-20' and time_format(hour, "%H" ) >= "14"


6. Selezionare tutti i corsi di laurea magistrale (38)

SELECT * 
FROM degrees
where level = "magistrale"


7. Da quanti dipartimenti è composta l'università? (12)

SELECT count(*) AS 'dipartimenti'
FROM departments



8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)


SELECT Count(*) as 'senza_numero' 
FROM teachers
where phone is null


-------

JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia


SELECT * 
FROM degrees
JOIN students
ON degrees.id = students.degree_id 
WHERE degrees.name = 'Corso di Laurea in Economia'


2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze

SELECT *
FROM departments
JOIN degrees
ON departments.id = degrees.department_id 
WHERE departments.name = 'Dipartimento di Neuroscienze' AND degrees.level = 'Magistrale'



3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT * 
FROM teachers
JOIN courses
ON courses.id = teachers.id
WHERE teachers.id = 44


4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome

 SELECT students.name, students.surname, students.enrolment_date, students.registration_number, degrees.name AS degree_name, departments.name AS department_name
 FROM students
JOIN degrees
ON degrees.id = students.degree_id
JOIN departments
ON departments.id = degrees.department_id
ORDER BY students.surname, students.name

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

SELECT *
FROM degrees
JOIN courses
ON degrees.id = courses.degree_id
JOIN teachers
ON courses.id = teachers.id


6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)

SELECT DISTINCT teachers.name, teachers.surname, teachers.phone, teachers.office_address, teachers.office_number, teachers.email
FROM teachers
JOIN course_teacher ON course_teacher.teacher_id = teachers.id
JOIN courses ON course.id = course_teacher.course_id
JOIN degrees ON degrees.id = courses.degree_id
JOIN departments ON departments.id = degrees.department_id
WHERE departments.name = 'Dipartimento di Matematica'


7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18