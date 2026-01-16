# SQL QUERIES PARTE 2

## Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```
SELECT students.*, degrees.name
FROM students
INNER JOIN degrees
ON students.degree_id = degrees.id
WHERE degrees.name = "Corso di Laurea in Economia"
```

##  Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```
SELECT *
FROM degrees
INNER JOIN departments
ON degrees.department_id = departments.id
WHERE degrees.level = "magistrale"
AND departments.name = "Dipartimento di Neuroscienze"
```

## Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```
SELECT teachers.id AS teacher_id, teachers.name AS teacher_name, teachers.surname AS teacher_surname, courses.*
FROM teachers
INNER JOIN course_teacher
ON teachers.id = course_teacher.teacher_id
INNER JOIN courses
ON course_teacher.course_id = course_id
WHERE teachers.id = 44
```

## Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```
SELECT *
FROM students
INNER JOIN degrees 
ON students.degree_id = degrees.id
INNER JOIN departments
ON degrees.department_id = department_id
ORDER BY students.name, students.surname;
```

## Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti


```
SELECT degrees.name AS degree, courses.name AS course, teachers.name AS teacher_name, teachers.surname AS teacher_surname
FROM courses
INNER JOIN degrees
ON courses.degree_id = degree_id
INNER JOIN course_teacher 
ON courses.id = course_teacher.course_id
INNER JOIN teachers
ON course_teacher.teacher_id = teachers.id
```

## Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```
SELECT teachers.*, departments.name
FROM teachers
INNER JOIN course_teacher
ON teachers.id = course_teacher.teacher_id
INNER JOIN courses
ON course_teacher.course_id = courses.id
INNER JOIN degrees
ON courses.degree_id = degrees.id
INNER JOIN departments
ON degrees.department_id = departments.id
WHERE departments.name = "Dipartimento di Matematica"
GROUP BY teachers.id
```

## BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami

correzione: 
```
SELECT students.id, students.name, students.surname, COUNT(exam_student.vote), MAX(exam_student.vote), courses.id, courses.name
FROM students
INNER JOIN exam_student
ON students.id = exam_student.student_id
INNER JOIN exams 
ON exams.id = exam_student.exam_id
INNER JOIN courses
ON exams.course_id = courses.id
GROUP BY students.id, courses.id 
HAVING MAX(exam_student.vote) >= 18
ORDER BY students.id

```