# Employee-Payroll-System
My Project is based on Employee Payroll System - 
mini project about it it may be ok project remain same
CREATE DATABASE EmployeePayrollDB;
USE EmployeePayrollDB;
CREATE TABLE Department (
    department_id INT PRIMARY KEY AUTO_INCREMENT,
    department_name VARCHAR(50) NOT NULL UNIQUE
);
CREATE TABLE Designation (
    designation_id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(50) NOT NULL
);
CREATE TABLE Role (
    role_id INT PRIMARY KEY AUTO_INCREMENT,
    role_name VARCHAR(30) NOT NULL UNIQUE
);
CREATE TABLE User (
    user_id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(100) NOT NULL,
    role_id INT,
    FOREIGN KEY (role_id) REFERENCES Role(role_id)
);
CREATE TABLE Employee (
    employee_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    cnic VARCHAR(15) UNIQUE NOT NULL,
    email VARCHAR(100),
    phone VARCHAR(15),
    hire_date DATE,
    department_id INT,
    designation_id INT,
    FOREIGN KEY (department_id) REFERENCES Department(department_id),
    FOREIGN KEY (designation_id) REFERENCES Designation(designation_id)
);
 CREATE TABLE Salary (
    salary_id INT PRIMARY KEY AUTO_INCREMENT,
    employee_id INT UNIQUE,
    basic_salary DECIMAL(10,2) CHECK (basic_salary > 0),
    allowances DECIMAL(10,2),
    deductions DECIMAL(10,2),
    net_salary DECIMAL(10,2),
    FOREIGN KEY (employee_id) REFERENCES Employee(employee_id)
);
CREATE TABLE Payroll (
    payroll_id INT PRIMARY KEY AUTO_INCREMENT,
    employee_id INT,
    salary_month VARCHAR(20),
    payment_date DATE,
    FOREIGN KEY (employee_id) REFERENCES Employee(employee_id)
);
CREATE TABLE Attendance (
    attendance_id INT PRIMARY KEY AUTO_INCREMENT,
    employee_id INT,
    date DATE,
    status VARCHAR(10),
    FOREIGN KEY (employee_id) REFERENCES Employee(employee_id)
);
CREATE TABLE LeaveRecord (
    leave_id INT PRIMARY KEY AUTO_INCREMENT,
    employee_id INT,
    leave_type VARCHAR(20),
    start_date DATE,
    end_date DATE,
    status VARCHAR(20),
    FOREIGN KEY (employee_id) REFERENCES Employee(employee_id)
);
CREATE TABLE Allowance (
    allowance_id INT PRIMARY KEY AUTO_INCREMENT,
    allowance_name VARCHAR(50),
    amount DECIMAL(10,2)
);
CREATE TABLE Deduction (
    deduction_id INT PRIMARY KEY AUTO_INCREMENT,
    deduction_name VARCHAR(50),
    amount DECIMAL(10,2)
);
CREATE TABLE Payment (
    payment_id INT PRIMARY KEY AUTO_INCREMENT,
    payroll_id INT,
    amount_paid DECIMAL(10,2),
    payment_method VARCHAR(20),
    FOREIGN KEY (payroll_id) REFERENCES Payroll(payroll_id)
);
CREATE TABLE Payroll_Details (
    detail_id INT PRIMARY KEY AUTO_INCREMENT,
    payroll_id INT,
    description VARCHAR(100),
    amount DECIMAL(10,2),
    FOREIGN KEY (payroll_id) REFERENCES Payroll(payroll_id)
);
CREATE TABLE Logs (
    log_id INT PRIMARY KEY AUTO_INCREMENT,
    error_message VARCHAR(255),
    log_date DATETIME DEFAULT CURRENT_TIMESTAMP
);
CREATE TABLE User_Role (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    role_id INT,
    FOREIGN KEY (user_id) REFERENCES User(user_id),
    FOREIGN KEY (role_id) REFERENCES Role(role_id)
);
-- data enterring

INSERT INTO Department (department_name) VALUES
('HR'),
('Finance'),
('IT'),
('Marketing'),
('Sales');

INSERT INTO Designation (title) VALUES
('Manager'),
('Assistant Manager'),
('Senior Developer'),
('Junior Developer'),
('Accountant');

INSERT INTO Role (role_name) VALUES
('Admin'),
('HR'),
('Employee');

INSERT INTO User (username, password, role_id) VALUES
('admin', 'admin123', 1),
('hr1', 'hr123', 2),
('emp1', 'emp123', 3); 

INSERT INTO Employee (name, cnic, email, phone, hire_date, department_id, designation_id) VALUES
('Ali Khan', '35202-1234567-1', 'ali.khan@example.com', '03001234567', '2020-01-15', 1, 1),
('Sara Ahmed', '35202-2345678-2', 'sara.ahmed@example.com', '03007654321', '2021-03-20', 2, 2),
('Usman Malik', '35202-3456789-3', 'usman.malik@example.com', '03005551234', '2019-07-10', 3, 3),
('Fatima Raza', '35202-4567890-4', 'fatima.raza@example.com', '03001112233', '2022-05-05', 4, 4),
('Hassan Ali', '35202-5678901-5', 'hassan.ali@example.com', '03009998877', '2021-09-01', 5, 5),
('Ayesha Khan', '35202-6789012-6', 'ayesha.khan@example.com', '03008887766', '2020-11-11', 1, 2),
('Bilal Ahmed', '35202-7890123-7', 'bilal.ahmed@example.com', '03007776655', '2021-06-22', 2, 3),
('Nadia Riaz', '35202-8901234-8', 'nadia.riaz@example.com', '03006665544', '2019-03-15', 3, 4),
('Omar Farooq', '35202-9012345-9', 'omar.farooq@example.com', '03005554433', '2022-08-05', 4, 5),
('Zainab Malik', '35202-0123456-0', 'zainab.malik@example.com', '03004443322', '2021-02-20', 5, 1),
('Kamran Shah', '35202-1122334-1', 'kamran.shah@example.com', '03003332211', '2020-04-18', 1, 3),
('Hina Iqbal', '35202-2233445-2', 'hina.iqbal@example.com', '03002221100', '2021-09-19', 2, 4),
('Adnan Tariq', '35202-3344556-3', 'adnan.tariq@example.com', '03001110099', '2019-12-01', 3, 5),
('Maria Khan', '35202-4455667-4', 'maria.khan@example.com', '03009990088', '2022-01-25', 4, 1),
('Fawad Ali', '35202-5566778-5', 'fawad.ali@example.com', '03008880077', '2020-07-30', 5, 2);

INSERT INTO Salary (employee_id, basic_salary, allowances, deductions, net_salary) VALUES
(1, 50000, 5000, 2000, 53000),
(2, 60000, 6000, 3000, 63000),
(3, 55000, 4500, 2500, 57000),
(4, 48000, 4000, 1500, 50500),
(5, 52000, 5200, 2200, 55000),
(6, 51000, 4000, 2000, 53000),
(7, 62000, 5500, 3000, 64500),
(8, 58000, 5000, 2500, 60500),
(9, 49000, 4500, 1500, 52000),
(10, 53000, 4800, 2000, 55800),
(11, 60000, 5000, 3000, 62000),
(12, 47000, 4000, 1000, 50000),
(13, 55000, 4500, 2000, 57500),
(14, 52000, 4000, 1500, 54500),
(15, 58000, 5000, 2500, 60500);

INSERT INTO Attendance (employee_id, date, status) VALUES
-- Employee 1
(1, '2026-01-01', 'Present'), (1, '2026-01-02', 'Present'), (1, '2026-01-03', 'Absent'),
-- Employee 2
(2, '2026-01-01', 'Present'), (2, '2026-01-02', 'Present'), (2, '2026-01-03', 'Present'),
-- Employee 3
(3, '2026-01-01', 'Present'), (3, '2026-01-02', 'Absent'), (3, '2026-01-03', 'Present'),
-- Employee 4
(4, '2026-01-01', 'Absent'), (4, '2026-01-02', 'Present'), (4, '2026-01-03', 'Present'),
-- Employee 5
(5, '2026-01-01', 'Present'), (5, '2026-01-02', 'Present'), (5, '2026-01-03', 'Absent'),
-- Employee 6
(6, '2026-01-01', 'Present'), (6, '2026-01-02', 'Present'), (6, '2026-01-03', 'Present'),
-- Employee 7
(7, '2026-01-01', 'Absent'), (7, '2026-01-02', 'Present'), (7, '2026-01-03', 'Present'),
-- Employee 8
(8, '2026-01-01', 'Present'), (8, '2026-01-02', 'Absent'), (8, '2026-01-03', 'Present'),
-- Employee 9
(9, '2026-01-01', 'Present'), (9, '2026-01-02', 'Present'), (9, '2026-01-03', 'Present'),
-- Employee 10
(10, '2026-01-01', 'Absent'), (10, '2026-01-02', 'Present'), (10, '2026-01-03', 'Present'),
-- Employee 11
(11, '2026-01-01', 'Present'), (11, '2026-01-02', 'Present'), (11, '2026-01-03', 'Present'),
-- Employee 12
(12, '2026-01-01', 'Present'), (12, '2026-01-02', 'Absent'), (12, '2026-01-03', 'Present'),
-- Employee 13
(13, '2026-01-01', 'Present'), (13, '2026-01-02', 'Present'), (13, '2026-01-03', 'Present'),
-- Employee 14
(14, '2026-01-01', 'Absent'), (14, '2026-01-02', 'Present'), (14, '2026-01-03', 'Present'),
-- Employee 15
(15, '2026-01-01', 'Present'), (15, '2026-01-02', 'Present'), (15, '2026-01-03', 'Absent');

INSERT INTO Allowance (allowance_name, amount) VALUES
('Transport', 2000),
('Housing', 3000),
('Medical', 1500),
('Bonus', 2500),
('Overtime', 1000);

INSERT INTO Deduction (deduction_name, amount) VALUES
('Tax', 2000),
('Provident Fund', 1000),
('Late Penalty', 500),
('Loan Deduction', 1500);

SELECT * FROM Payroll;
INSERT INTO Payroll_Details (payroll_id, description, amount) VALUES
(1, 'Transport Allowance', 2000),
(1, 'Medical Allowance', 1500),
(2, 'Housing Allowance', 3000),
(3, 'Tax Deduction', 2000),
(4, 'Loan Deduction', 1500);

show tables;

DELIMITER //

CREATE PROCEDURE sp_InsertPayroll (
    IN p_employee_id INT,
    IN p_salary_month VARCHAR(20),
    IN p_payment_date DATE,
    IN p_details JSON   -- JSON format: [{"description":"Transport","amount":2000}, ...]
)
BEGIN
    DECLARE last_payroll_id INT;
    DECLARE i INT DEFAULT 0;
    DECLARE n INT;

    START TRANSACTION;

    INSERT INTO Payroll (employee_id, salary_month, payment_date)
    VALUES (p_employee_id, p_salary_month, p_payment_date);

    SET last_payroll_id = LAST_INSERT_ID();

    SET n = JSON_LENGTH(p_details);

    WHILE i < n DO
        INSERT INTO Payroll_Details (payroll_id, description, amount)
        VALUES (
            last_payroll_id,
            JSON_UNQUOTE(JSON_EXTRACT(p_details, CONCAT('$[', i, '].description'))),
            JSON_EXTRACT(p_details, CONCAT('$[', i, '].amount'))
        );
        SET i = i + 1;
    END WHILE;

    COMMIT;
END;
//

DELIMITER ;

CALL sp_InsertPayroll(
    1, 
    'February 2026', 
    '2026-02-28',
    '[{"description":"Transport Allowance","amount":2000},
      {"description":"Medical Allowance","amount":1500}]'
);

DELIMITER //

CREATE PROCEDURE sp_CalculateNetSalary(IN p_employee_id INT)
BEGIN
    UPDATE Salary
    SET net_salary = basic_salary + allowances - deductions
    WHERE employee_id = p_employee_id;
END;
//

DELIMITER ;alterCALL sp_CalculateNetSalary(1);

DELIMITER //

CREATE PROCEDURE sp_MonthlyPayrollReport(IN p_salary_month VARCHAR(20))
BEGIN
    SELECT 
        e.employee_id,
        e.name AS employee_name,
        d.department_name,
        s.basic_salary,
        s.allowances,
        s.deductions,
        s.net_salary,
        p.payment_date
    FROM Payroll p
    JOIN Employee e ON p.employee_id = e.employee_id
    JOIN Department d ON e.department_id = d.department_id
    JOIN Salary s ON e.employee_id = s.employee_id
    WHERE p.salary_month = p_salary_month
    ORDER BY e.employee_id;
END;
//

DELIMITER ;
CALL sp_MonthlyPayrollReport('January 2026');

DELIMITER //

CREATE TRIGGER trg_UpdateNetSalary
BEFORE UPDATE ON Salary
FOR EACH ROW
BEGIN
    SET NEW.net_salary = NEW.basic_salary + NEW.allowances - NEW.deductions;
END;
//

DELIMITER ;
UPDATE Salary 
SET basic_salary = 60000, allowances = 5000, deductions = 2000 
WHERE employee_id = 1;

DELIMITER //

CREATE TRIGGER trg_SalaryUpdateLog
AFTER UPDATE ON Salary
FOR EACH ROW
BEGIN
    INSERT INTO Logs (error_message)
    VALUES (CONCAT('Salary updated for Employee ID: ', NEW.employee_id, 
                   ', old net_salary: ', OLD.net_salary, 
                   ', new net_salary: ', NEW.net_salary));
END;
//

DELIMITER ;
START TRANSACTION;

-- 1. Insert into Payroll
INSERT INTO Payroll (employee_id, salary_month, payment_date)
VALUES (1, 'March 2026', '2026-03-31');

SET @last_payroll_id = LAST_INSERT_ID();

-- Insert into Payroll_Details
INSERT INTO Payroll_Details (payroll_id, description, amount)
VALUES
(@last_payroll_id, 'Transport Allowance', 2000),
(@last_payroll_id, 'Medical Allowance', 1500);

-- Commit transaction
COMMIT;

START TRANSACTION;

-- Update basic salary
UPDATE Salary
SET basic_salary = 60000, allowances = 5000
WHERE employee_id = 2;

-- Update deductions
UPDATE Salary
SET deductions = 2500
WHERE employee_id = 2;

-- Recalculate net salary
UPDATE Salary
SET net_salary = basic_salary + allowances - deductions
WHERE employee_id = 2;

COMMIT;

START TRANSACTION;

--  leave
UPDATE LeaveRecord
SET status = 'Approved'
WHERE leave_id = 1;

-- 2. Update attendance to 'On Leave' for the same dates
UPDATE Attendance a
JOIN LeaveRecord l ON a.employee_id = l.employee_id
SET a.status = 'On Leave'
WHERE l.leave_id = 1 AND a.date BETWEEN l.start_date AND l.end_date;

COMMIT;

SELECT 
    d.department_name,
    e.employee_id,
    e.name AS employee_name,
    s.basic_salary,
    s.allowances,
    s.deductions,
    s.net_salary
FROM Employee e
JOIN Department d ON e.department_id = d.department_id
JOIN Salary s ON e.employee_id = s.employee_id
ORDER BY d.department_name, e.employee_id;

SELECT 
    e.employee_id,
    e.name AS employee_name,
    SUM(CASE WHEN a.status='Present' THEN 1 ELSE 0 END) AS Days_Present,
    SUM(CASE WHEN a.status='Absent' THEN 1 ELSE 0 END) AS Days_Absent,
    SUM(CASE WHEN a.status='On Leave' THEN 1 ELSE 0 END) AS Days_OnLeave
FROM Attendance a
JOIN Employee e ON a.employee_id = e.employee_id
GROUP BY e.employee_id, e.name
ORDER BY e.employee_id;

SELECT 
    e.employee_id,
    e.name AS employee_name,
    l.leave_type,
    l.start_date,
    l.end_date,
    l.status
FROM LeaveRecord l
JOIN Employee e ON l.employee_id = e.employee_id
WHERE l.status = 'Pending'
ORDER BY l.start_date;

SELECT 
    p.salary_month,
    e.employee_id,
    e.name AS employee_name,
    SUM(pd.amount) AS total_allowances_deductions,
    s.basic_salary,
    s.net_salary
FROM Payroll p
JOIN Employee e ON p.employee_id = e.employee_id
JOIN Salary s ON e.employee_id = s.employee_id
LEFT JOIN Payroll_Details pd ON p.payroll_id = pd.payroll_id
GROUP BY p.salary_month, e.employee_id
ORDER BY p.salary_month, e.employee_id;
