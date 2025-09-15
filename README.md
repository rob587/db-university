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


4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)


5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)


6. Selezionare tutti i corsi di laurea magistrale (38)


7. Da quanti dipartimenti è composta l'università? (12)


8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)




