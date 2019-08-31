# SQL-task-RubyCourses
answers for SQL task from RG

1/ Get all statuses, not repeating, alphabetically ordered:

SELECT DISTINCT status 
FROM tasks
ORDER BY status;   


2/  Get the count of all tasks in each project, order by tasks count descending:

SELECT COUNT (tasks.id)
FROM projects
INNER JOIN tasks ON projects.id = tasks.project_id
GROUP BY projects.id
ORDER BY COUNT (tasks.id) DESC;

3/ Get the count of all tasks in each project, order by projects names:

SELECT COUNT(tasks.id)
FROM projects
INNER JOIN tasks ON projects.id = tasks.project_id
GROUP BY projects.id
ORDER BY projects.name;

4/ Get the tasks for all projects having the name beginning with “N” letter:
SELECT *
FROM tasks
WHERE name LIKE 'N%';

5/ Get the list of all projects containing the ‘a’ letter in the middle of the name, and show the tasks count near each project. Mention that there can exist projects without tasks and tasks with project_id=NULL:

SELECT projects.name, COUNT(projects.id = tasks.project_id)
FROM projects
FULL OUTER JOIN tasks on projects.id = tasks.project_id
WHERE projects.name LIKE '%a%'
GROUP BY projects.name;

6/ Get the list of tasks with duplicate names. Order alphabetically:

SELECT name, COUNT(*)
FROM tasks
GROUP BY name
HAVING COUNT(*) > 1
ORDER BY name ;

7/ Get the list of tasks having several exact matches of both name and status, from the project ‘Garage’. Order by matches count:

SELECT tasks.name, COUNT(tasks.name = tasks.status)  
FROM tasks
INNER JOIN projects ON projects.name = 'Garage'
WHERE tasks.name = tasks.status
GROUP BY tasks.name
ORDER BY COUNT(tasks.name = tasks.status) DESC;


8/ Get the list of project names having more than 10 tasks in status ‘completed’. Order by project_id:

SELECT projects.id, COUNT(tasks.status = 'completed') 
FROM projects
INNER JOIN tasks ON projects.id = tasks.project_id
WHERE tasks.status = 'completed'
GROUP BY projects.id
HAVING COUNT(*) > 10
ORDER BY projects.id;
