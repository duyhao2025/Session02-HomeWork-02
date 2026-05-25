CREATE DATABASE UniversityDB
CREATE SCHEMA university;
CREATE TABLE university.students (
    student_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    birth_date DATE,
    email VARCHAR(100) NOT NULL UNIQUE
);
ALTER TABLE university.students
ADD CONSTRAINT chk_student_age
CHECK (
    EXTRACT(YEAR FROM AGE(CURRENT_DATE, birth_date)) >= 18
);
CREATE TABLE university.courses (
    course_id SERIAL PRIMARY KEY,
    course_name VARCHAR(100) NOT NULL,
    credits INT
);
CREATE TABLE university.enrollments (
    enrollment_id SERIAL PRIMARY KEY,
    student_id INT,
    course_id INT,
    enroll_date DATE,

    CONSTRAINT fk_student
        FOREIGN KEY (student_id)
        REFERENCES university.students(student_id),

    CONSTRAINT fk_course
        FOREIGN KEY (course_id)
        REFERENCES university.courses(course_id)
);
DROP TABLE university.enrollments;

DROP TABLE university.courses;

DROP TABLE university.students;
