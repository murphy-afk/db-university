## Selezionare tutti gli studenti nati nel 1990

```
SELECT *
FROM `students`
WHERE year(`date_of_birth`) = 1990;
```

## Selezionare tutti i corsi che valgono più di 10 crediti

```
SELECT *
FROM `courses`
WHERE `cfu` > 10
ORDER BY `cfu`;
```

## Selezionare tutti gli studenti che hanno più di 30 anni

```
SELECT *
FROM `students`
WHERE TIMESTAMPDIFF(YEAR, `date_of_birth`, CURDATE()) > 30;
```

## Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea

```
SELECT *
FROM `courses`
WHERE `period` = 'I semestre'
AND `year` = 1;
```

## Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020

```
SELECT *
FROM `exams`
WHERE `date` = "2020-06-20"
AND `hour` > "14:00";
```

## Selezionare tutti i corsi di laurea magistrale

```
SELECT *
FROM `degrees`
WHERE `level` = "magistrale";
```

## Da quanti dipartimenti è composta l'università?

```
SELECT COUNT(id)
FROM `departments`;
```

## Quanti sono gli insegnanti che non hanno un numero di telefono?

```
SELECT COUNT(id)
FROM `teachers`
WHERE `phone` IS NULL;
```

# BONUS

## Contare quanti iscritti ci sono stati ogni anno

```
SELECT COUNT(`id`)
FROM `students` 
GROUP BY YEAR(`enrolment_date`) 
```

in ordine per anno:

```
SELECT YEAR(`enrolment_date`) AS `enrolment_year`,
COUNT(`id`) AS `students_count`
FROM `students` 
GROUP BY YEAR(`enrolment_date`) 
ORDER BY `enrolment_year`;
```

## Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```
SELECT `office_address`,
COUNT(id) as `teachers_count` 
FROM `teachers`
GROUP BY `office_address`;
```

uffici con solo un insegnate:

```
SELECT `office_address`,
COUNT(id) as `teachers_count` 
FROM `teachers`
GROUP BY `office_address`
HAVING `teachers_count` = 1;
```

## Calcolare la media dei voti di ogni appello d'esame

```
SELECT `exam_id` AS `exam`,
AVG(`vote`) AS `average_vote`
FROM `exam_student`
GROUP BY `exam_id`;
```

## Contare quanti corsi di laurea ci sono per ogni dipartimento

```
SELECT `department_id` as `department`,
COUNT(`id`) AS `degrees`
FROM `degrees`
GROUP BY `department_id`;
```