### GIORNO 2
```

```

## Selezionare tutti i corsi del Corso di Laurea in Informatica (22)

```
SELECT *
FROM `courses`
INNER JOIN `degrees`
ON `courses`.`degree_id` = `degrees`.`id`
HAVING `degrees`.`name` = "Corso di Laurea in Informatica"
```

## Selezionare le informazioni sul corso con id = 144, con tutti i relativi appelli d’esame

```
SELECT *
FROM `exams`
INNER JOIN `courses`
ON `exams`.`course_id` = `courses`.`id`
HAVING `courses`.`id` = 144
```

## Selezionare a quale dipartimento appartiene il Corso di Laurea in Diritto dell'Economia
```
SELECT *
FROM `degrees`
INNER JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `degrees`.`name` = "Corso di Laurea in Diritto dell'Economia"
```

## Selezionare tutti gli appelli d'esame del Corso di Laurea Magistrale in Fisica del primo anno

```
SELECT *
FROM `exams`
INNER JOIN `courses`
ON `exams`.`course_id` = `courses`.`id`
INNER JOIN `degrees`
ON `courses`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = "Corso di Laurea Magistrale in Fisica"
AND `courses`.`year` = 1;
```

## Selezionare tutti i docenti che insegnano nel Corso di Laurea in Lettere

```
SELECT *
FROM teachers
INNER JOIN course_teacher
ON teachers.id = course_teacher.teacher_id
inner join courses
on course_teacher.course_id = courses.id
inner join degrees
on courses.degree_id = degrees.id
where degrees.name = "Corso di Laurea in Lettere"
```
