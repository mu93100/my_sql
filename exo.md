# Exercices sur les selections avec conditions.

## Niveau 1
---
- Afficher le nom et prenom de tous les élèves.
```sql
SELECT last_name, first_name
FROM student;
```
- Afficher toutes les données des élèves dont le prénom est "Alice".
```sql
SELECT * 
FROM student 
WHERE first_name='Alice';
```
- Affichier les noms, prénoms et moyennes des élèves dont le nom de famille est "Lemoine".
```sql
SELECT first_name, last_name, average_grade
FROM student
WHERE last_name='Lemoine';
```
## Niveau 2
---
- Afficher le nombre d'élèves.
```sql
SELECT COUNT(*) AS student
FROM student;
```
- Afficher le nombre d'élèves dont la moyenne est suppérieur à 14.
```sql
SELECT COUNT(*) 
from student
WHERE average_grade>14;
```
- Afficher le nombe d'élèves dont la moyenne est comprise entre 8 et 11.
```sql
SELECT COUNT(*) 
FROM student 
WHERE average_grade>=8 AND average_grade<=11;
```
- Afficher le nom, le prenom et la moyenne de l'élève ayant la moyenne la plus haute.
```sql
SELECT first_name, last_name, average_grade 
FROM student 
ORDER BY average_grade DESC 
LIMIT 1;
```
- Afficher le nom, le prenom et la moyenne de l'élève ayant la moyenne la plus basse.
```sql
SELECT first_name, last_name, average_grade 
FROM student 
ORDER BY average_grade ASC 
LIMIT 1;
```
- Afficher la somme de la moyenne de tous les élèves du campus ayant plus de 9 de moyenne.
```sql
SELECT SUM(average_grade) FROM student WHERE average_grade>9;
```
- Afficher la moyenne de la moyenne de tous les élèves du campus dont la moyenne est inférieur à 16.
```sql
SELECT AVG(average_grade) 
FROM student 
WHERE average_grade<16;
```
## Niveau 3
---
- Afficher les noms, prenoms et moyenne des élèves triés par ordre alphabetique du nom de famille.
```sql
SELECT first_name, last_name, average_grade 
FROM student 
ORDER BY last_name ASC;
```
- Afficher les noms, prenoms et moyenne des dix élèves ayant la moyenne la plus haute, triés par notes décroissantes.
```sql
SELECT first_name, last_name, average_grade 
FROM student 
ORDER BY average_grade DESC 
LIMIT 10;
```
- Afficher les noms et prenoms des 10 élèves ayant la moyenne la plus basse, triés par notes croissantes.
```sql
SELECT first_name, last_name 
FROM student 
ORDER BY average_grade ASC 
LIMIT 10;
```
## Niveau 4
- afficher par age 22 et moy décroissantes
```sql
SELECT first_name, last_name, age, average_grade
FROM student
WHERE age IN ('22')
ORDER BY average_grade DESC;
```
- Afficher le nom et le prénom de tous les élèves dont le nom de famille commence par la lettre "C".
```sql
SELECT first_name, last_name 
FROM student 
WHERE last_name LIKE 'c%';
```
- Afficher le nom et le prénom de tous les élèves dont le nom de famille se termine par la lettre "a".
```sql
SELECT first_name, last_name
FROM student
WHERE last_name LIKE '%a';
```
- Afficher le nom et le prénom de tous les élèves dont le nom de famille contient la lettre "e".
```sql
SELECT first_name, last_name 
FROM student 
WHERE last_name 
LIKE '%e%';
```
- Afficher le nom et le prénom de tous les éléves dont le nom de famille contient la lettre "e" et qui ont plus de 10 de moyenne.
```sql
SELECT first_name, last_name
FROM student
WHERE last_name LIKE '%e%'AND average_grade>10;
```
- Afficher le nom et le prénom de tous les élèves dont le prénom commence par la lettre "c" et se termine par la lettre "e".
```sql
SELECT first_name, last_name 
FROM student 
WHERE first_name LIKE 'c%' AND first_name LIKE '%e';
```
- Afficher le nom, prénom et numéro de téléphone des élèves dont le nom est Bouvier, Lemoine ou Dupuis
```sql
SELECT first_name, last_name, phone_number 
FROM student 
WHERE last_name IN ('Lemoine', 'bouvier', 'Dupuis') 
ORDER BY last_name ASC, first_name ASC;
```
- Afficher le nom, prénom et numéro de téléphone des élèves dont le numéro de téléphone n'est pas 0605060708 ou 0605566778
```sql
SELECT first_name, last_name, phone_number 
FROM student 
WHERE phone_number NOT IN ('0605060708', '0605566778');
```
## Niveau 5

- Afficher le nom et prénom des élèves n'ayant pas renseignés leurs addresse mail.
```sql
SELECT first_name, last_name 
FROM student 
WHERE email IS NULL;
```
- Afficher le nom, le prénom et l'âge des élèves dont l'âge est compris 18 et 25 ans
```sql
SELECT first_name, last_name, age
FROM student
WHERE age BETWEEN 18 AND 25;
```
- Afficher le nom, prénom et l'email des élèves ayant bien renseignés leurs addresse mail.
```sql
SELECT first_name, last_name, email 
FROM student WHERE email IS NOT NULL;
```
- Afficher le nom, le prénom et l'âge des élèves dont l'âge n'est pas compris entre 23 et 36 ans.
```sql
SELECT first_name, last_name, age FROM student WHERE age NOT BETWEEN 23 AND 36;
```
## Niveau 6
- Afficher le nom, prénom et l'âge des élèves triés par âge.
```sql
SELECT first_name, last_name, age
FROM student
ORDER BY age;
```
- Afficher le nom, prénom, la moyenne et l'âge des élèves triés par âge et ayant plus de 14 de moyenne.
```sql
SELECT first_name, last_name, age, average_grade 
FROM student 
WHERE average_grade>14 
ORDER BY age ASC;
toujours mettre ASC ça marche sans ASC masi mieux pour compréhension, collègues...
```
- Afficher la ville des élèves sans doublon de ville.
```sql
SELECT DISTINCT city 
FROM student;
```
- Afficher toutes les données des élèves, mais renommer les colonnes en français. (sans accents)
```sql
SELECT student_id AS identifiant, first_name AS prenom, last_name AS nom, age, average_grade AS moyenne, city AS ville, email, phone_number AS telephone 
FROM student;
```
## Niveau 7
- Afficher le nom, prénom et notes (table note) de tous les élèves.
```sql
SELECT student.first_name, student.last_name, note.grade
FROM student
INNER JOIN note ON student.student_id= note.student_id
```
- Afficher le nom, prénom et spécialisations (department) de tous les élèves.
```sql
SELECT student.first_name, student.last_name, department.department_name
FROM student
INNER JOIN student_department ON student.student_id= student_department.student_id
INNER JOIN department ON department.department_id= student_department.department_id;
```
- Afficher le nom, prénom et notes de tous les élèves en utilisant LEFT JOIN.
```sql
SELECT student.first_name, student.last_name, note.grade
FROM student
LEFT JOIN note ON student.student_id=note.student_id;
```
- Afficher les spécialisations ainsi que les matières (subject) associé en utilisant RIGHT JOIN.
```sql
SELECT department.department_name,subject.subject_name
FROM department
RIGHT JOIN subject ON subject.department_id=department.department_id;
```

exos en + :::
Affichez le prénom, le nom et la moyenne des notes de chaque étudiant. (Joindre les tables student et note).
```sql
SELECT student.first_name, student.last_name, note.grade, AVG(note.grade) AS moyenne
FROM student
INNER JOIN note ON note.student_id=student.student_id
GROUP BY student.last_name;
```
Affichez le prénom, le nom de l'étudiant et le nom de chaque matière qu'ils ont suivie.
```sql
SELECT student.first_name, student.last_name, subject.subject_name
FROM student
INNER JOIN note ON note.student_id = student.student_id
INNER JOIN subject ON note.subject_id = subject.subject_id;
```
Affichez le nom de chaque département et le nombre d'étudiants qui y sont inscrits.
```sql
SELECT department.department_name, COUNT(student_department.department_id) AS nombre_eleves
FROM student_department
LEFT JOIN department ON student_department.department_id = department.department_id
GROUP BY department_name;
```
Affichez le prénom, le nom de chaque étudiant, le nom de la matière et la note qu'ils ont obtenue, triée par note décroissante
```sql
SELECT student.last_name, student.first_name, subject.subject_name, note.grade
FROM student
INNER JOIN note ON student.student_id = note.student_id
INNER JOIN subject ON note.subject_id = subject.subject_id
ORDER BY note.grade DESC;
```
- **Facultatif** : essayer le CROSS JOIN
```sql

```
## Niveau 8

- Ajoutez vous à la table élèves (données factices). Prénom, Nom, âge, email, numéro de téléphone, ville
```sql
INSERT INTO student(first_name, last_name, age, email, phone_number, city)
VALUES ('Martin', 'Pierre', '25', 'pierre.martin@email.com', '0656565656', 'nantes');
```
- Ajouter des emails au élèves dont l'adresse mail est NULL. (Regarder SQL CASE)
```sql
récupérer les id des email NULL
UPDATE student
set email='pompom@nouveau-email.com'
WHERE student_id= 12, 15

2nd temps :::
UPDATE student
SET email = 'pierre.martin@nouveau-email.com'
WHERE student_id=11;

sheezad :::
INSERT INTO student (first_name, average_grade, email,age,last_name,city)

VALUES ('Eon', '20', 'eon@test.com','20','007','gotham city');

arnaud ::: 
SELECT 
    first_name, last_name, 
    CONCAT(LOWER(first_name), '.', LOWER(last_name), '@example.com') AS suggested_email
FROM student
WHERE email IS NULL;
```
- Supprimer l'élève suivant : Hugo Tissot, via son id
```sql
select student_id
FROM student
WHERE last_name = 'tissot'
+++
DELETE FROM student
WHERE id = '78'
```
- Ajouter à votre élève sa spécialisation.
```sql
INSERT INTO student_department(student_id, department_id)
VALUE(44,1);
```