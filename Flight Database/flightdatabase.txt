CREATE TABLE addf038_Airport(
    Airport_ID VARCHAR(30) NOT NULL PRIMARY KEY,
    City VARCHAR(255) NOT NULL,
    Full_Name VARCHAR(100) NOT NULL,
    Timezone VARCHAR(10) NOT NULL,
    Country VARCHAR(30) NOT NULL
);

CREATE TABLE addf038_Destination(
    Destination_ID INTEGER(10) NOT NULL AUTO_INCREMENT PRIMARY KEY,
    Departure_Airport VARCHAR(30) NOT NULL,
    Arrival_Airport VARCHAR(30) NOT NULL,
    Travel_Time time NOT NULL,
    FOREIGN KEY(Departure_Airport)REFERENCES addf038_Airport(Airport_ID),
    FOREIGN KEY(Arrival_Airport)REFERENCES addf038_Airport(Airport_ID));


CREATE TABLE addf038_Plane(
    Aircraft_Registration_Number VARCHAR(10) NOT NULL PRIMARY KEY,
    Model_Number VARCHAR(8) NOT NULL,
    Staff_Required INTEGER(2) NOT NULL,
    Number_Of_Seats INTEGER(3) NOT NULL,
    Doors INTEGER(2) NOT NULL,
    `Condition` VARCHAR(10) NOT NULL,
    Milage INTEGER(10) NOT NULL,
    Brand VARCHAR(10) NOT NULL,
    Maximum_Speed INTEGER(8) NOT NULL,
    Weight_capacity INTEGER(5) NOT NULL,
    Engine_Type VARCHAR(15) NOT NULL,
    Required_Fuel float(5) NOT NULL,
    Model_Name VARCHAR(20) NOT NULL);

CREATE TABLE addf038_Flights(
    Flight_Number INTEGER(10) NOT NULL PRIMARY KEY,
    Flight_Departure TIME NOT NULL,
    Flight_Arrival TIME NOT NULL,
    Destination_ID INTEGER(10) NOT NULL,
    Aircraft_Registration_Number VARCHAR(10) NOT NULL,
    FOREIGN KEY(Destination_ID)REFERENCES addf038_Destination(Destination_ID),
    FOREIGN KEY(Aircraft_Registration_Number)REFERENCES addf038_Plane(Aircraft_Registration_Number));

    
CREATE TABLE addf038_Customer(
    Phone_Number VARCHAR(12) NOT NULL PRIMARY KEY,
    Name VARCHAR(20) NOT NULL,
    Middle_Name VARCHAR(20),
    Surname VARCHAR(20) NOT NULL,
    Postcode VARCHAR(15) NOT NULL,
    Gender ENUM('M','F','OTHER') NOT NULL,
    Email VARCHAR(40) NOT NULL,
    Date_Of_Birth INTEGER(8) NOT NULL,
    Flight_Number INTEGER(10) NOT NULL,
    FOREIGN KEY(Flight_Number) REFERENCES addf038_Flights(Flight_Number));

CREATE TABLE addf038_Staff(
    Email VARCHAR(30) NOT NULL PRIMARY KEY,
    Name VARCHAR(20) NOT NULL,
    Surname VARCHAR(20) NOT NULL,
    Phone_Number VARCHAR(12) NOT NULL,
    Postcode VARCHAR(15) NOT NULL,
    Job_Role VARCHAR(25) NOT NULL,
    Salary FLOAT(6) NOT NULL,
    Address VARCHAR(150) NOT NULL,
    Flight_Number INTEGER(10) NOT NULL,
    Supervisor_Email VARCHAR(30),
    FOREIGN KEY(Supervisor_Email) REFERENCES addf038_Staff(Email));

INSERT INTO addf038_Plane (Aircraft_Registration_Number, Model_Number, Staff_Required, Number_Of_Seats, Doors, `Condition`, Milage, Brand, Maximum_Speed, Weight_capacity, Engine_Type, Required_Fuel, Model_Name) VALUES ('B777X123', 'B777', 5, 300, 4, 'Good', 12000, 'Boeing', 600, 200, 'Jet', 50.5, 'Dreamliner'),
('A350X789', 'A350', 4, 250, 2, 'Excellent', 10000, 'Airbus', 550, 180, 'Jet', 40.2, 'XWB'),
('B737NG456', 'B737', 3, 180, 2, 'Average', 8000, 'Boeing', 500, 150, 'Jet', 60.8, 'Next Gen'),
('A320X999', 'A320', 2, 150, 4, 'Good', 9500, 'Airbus', 580, 185, 'Jet', 45.5, 'Neo'),
('B787ABC789', 'B787', 5, 250, 4, 'Excellent', 15000, 'Boeing', 700, 220, 'Jet', 60.2, 'Dreamliner'),
('A380XYZ123', 'A380', 6, 500, 5, 'Good', 20000, 'Airbus', 650, 250, 'Jet', 80.5, 'Super Jumbo'),
('B747PQR789', 'B747', 4, 400, 3, 'Average', 18000, 'Boeing', 580, 210, 'Jet', 55.0, 'Jumbo Jet'),
('A330STU456', 'A330', 3, 250, 2, 'Good', 12000, 'Airbus', 540, 190, 'Jet', 48.5, 'Neo'),
('B767VWX999', 'B767', 4, 300, 3, 'Good', 13000, 'Boeing', 580, 200, 'Jet', 55.5, 'Widebody'),
('A321YZA987', 'A321', 2, 200, 2, 'Excellent', 10000, 'Airbus', 540, 170, 'Jet', 42.3, 'Neo'),
('B777BCD123', 'B777', 5, 300, 4, 'Good', 12000, 'Boeing', 600, 200, 'Jet', 50.5, 'Dreamliner'),
('A350EFG789', 'A350', 4, 250, 2, 'Average', 10000, 'Airbus', 550, 180, 'Jet', 40.2, 'XWB');


INSERT INTO addf038_Airport (Airport_ID, City, Full_Name, Timezone, Country) VALUES 
('LHR', 'London', 'London Heathrow Airport', 'GMT', 'United Kingdom'),
('JFK', 'New York', 'John F. Kennedy International Airport', 'EST', 'United States'),
('CDG', 'Paris', 'Charles de Gaulle Airport', 'CET', 'France'),
('SYD', 'Sydney', 'Sydney Kingsford Smith Airport', 'AEDT', 'Australia'),
('PEK', 'Beijing', 'Beijing Capital International Airport', 'CST', 'China'),
('DXB', 'Dubai', 'Dubai International Airport', 'GST', 'United Arab Emirates'),
('HND', 'Tokyo', 'Haneda Airport', 'JST', 'Japan'),
('LAX', 'Los Angeles', 'Los Angeles International Airport', 'PST', 'United States'),
('SIN', 'Singapore', 'Changi Airport', 'SGT', 'Singapore'),
('ATL', 'Atlanta', 'Hartsfield-Jackson Atlanta International Airport', 'EST', 'United States'),
('AMS', 'Amsterdam', 'Amsterdam Airport Schiphol', 'CET', 'Netherlands'),
('HKG', 'Hong Kong', 'Hong Kong International Airport', 'HKT', 'Hong Kong');





INSERT INTO addf038_Destination (
    Departure_Airport,
    Arrival_Airport,
    Travel_Time
) VALUES
('LAX', 'PEK', '13:00'),
('SIN', 'SYD', '8:20'),
('ATL', 'CDG', '8:40'),
('AMS', 'JFK', '8:20'),
('LHR', 'AMS', '1:10'),
('JFK', 'HKG', '16:00'),
('ATL', 'CDG', '9:40'),
('SYD', 'SIN', '8:20'),
('PEK', 'LAX', '12:40'),
('DXB', 'HND', '9:30'),
('HND', 'DXB', '9:30'),
('HKG', 'LHR', '13:00');




INSERT INTO addf038_Flights (
    Flight_Number,
    Flight_Departure,
    Flight_Arrival,
    Destination_ID,
    Aircraft_Registration_Number
) VALUES
(2035, '08:30:00', '09:40:00', 1, 'B777X123'),
(4187, '15:30:00', '07:30:00', 2, 'A350X789'),
(7692, '10:30:00', '20:10:00', 3, 'B737NG456'),
(1123, '12:30:00', '20:50:00', 4, 'A320X999'),
(5654, '14:30:00', '03:10:00', 5, 'B787ABC789'),
(9276, '09:30:00', '19:00:00', 6, 'A380XYZ123'),
(3210, '11:30:00', '21:00:00', 7, 'B747PQR789'),
(8542, '07:30:00', '20:30:00', 8, 'A330STU456'),
(6441, '14:30:00', '22:50:00', 9, 'B767VWX999'),
(2198, '12:30:00', '21:10:00', 10, 'A321YZA987'),
(4823, '08:30:00', '16:50:00', 11, 'B777BCD123'),
(9365, '11:30:00', '00:30:00', 12, 'A350EFG789');




INSERT INTO addf038_Customer (Phone_Number, Name, Middle_Name, Surname, Postcode, Gender, Email, Date_Of_Birth, Flight_Number) VALUES 
('07700900123', 'John', NULL, 'Doe', 'SW1A 1AA', 'M', 'john.doe@email.com', 19900101, 2035),
('07890123456', 'Jane', 'Marie', 'Smith', 'EC1A 1BB', 'F', 'jane.smith@email.com', 19850215, 2035),
('07711223344', 'Michael', 'David', 'Johnson', 'WC1A 1DD', 'M', 'michael.johnson@email.com', 19780320, 2035),
('07555667788', 'Emily', NULL, 'Taylor', 'SE1 1EE', 'F', 'emily.taylor@email.com', 19951005, 1123),
('07990001112', 'Christopher', 'Paul', 'Miller', 'W1A 1FF', 'M', 'christopher.miller@email.com', 19801012, 1123),
('07445666777', 'Amanda', NULL, 'Clark', 'NW1A 1GG', 'F', 'amanda.clark@email.com', 19921218, 1123),
('07889990011', 'Daniel', 'Joseph', 'Williams', 'SW1E 5AG', 'M', 'daniel.williams@email.com', 19870425, 3210),
('07732987456', 'Sophia', 'Elizabeth', 'Moore', 'E1W 1BH', 'F', 'sophia.moore@email.com', 19981130, 3210),
('07986541233', 'William', NULL, 'Jones', 'EC2A 2CI', 'M', 'william.jones@email.com', 19720508, 3210),
('07987123654', 'Olivia', 'Rose', 'Brown', 'W2 2DJ', 'F', 'olivia.brown@email.com', 19970803, 2198),
('07456789012', 'Ethan', 'Andrew', 'Wilson', 'N1C 4DK', 'M', 'ethan.wilson@email.com', 19830914, 2198),
('07321012345', 'Emma', 'Charlotte', 'Anderson', 'SW1Y 4EL', 'F', 'emma.anderson@email.com', 20000122, 2198);



INSERT INTO addf038_Staff (Email, Name, Surname, Phone_Number, Postcode, Job_Role, Salary, Address, Flight_Number, Supervisor_Email) VALUES
('ahmed.ali@email.com', 'Ahmed', 'Ali', '07701234567', 'SW1A 1AA', 'Pilot', 80000.00, '12 Buckingham Palace Road, London', 2035, NULL),
('yuki.ito@email.com', 'Yuki', 'Ito', '07982345678', 'W2 2DJ', 'Flight Attendant', 45000.00, '18 Paddington Street, London', 3210, NULL),
('sophie.martin@email.com', 'Sophie', 'Martin', '07892345678', 'EC1A 1BB', 'Cabin Crew', 45000.00, '8 Newgate Street, London', 2035, 'ahmed.ali@email.com'),
('yusuf.kim@email.com', 'Yusuf', 'Kim', '07783456789', 'WC1A 1DD', 'Cabin Crew', 42000.00, '15 High Holborn, London', 1123, 'yuki.ito@email.com'),
('rania.abbas@email.com', 'Rania', 'Abbas', '07550123456', 'SE1 1EE', 'Ground Crew', 38000.00, '25 Southwark Street, London', 1123, 'ahmed.ali@email.com'),
('matteo.rossi@email.com', 'Matteo', 'Rossi', '07987654321', 'W1A 1FF', 'Pilot', 90000.00, '10 Regent Street, London', 1123, 'yuki.ito@email.com'),
('hiroshi.tanaka@email.com', 'Hiroshi', 'Tanaka', '07451234567', 'NW1A 1GG', 'Flight Attendant', 44000.00, '5 Camden High Street, London', 3210, 'ahmed.ali@email.com'),
('noura.hamid@email.com', 'Noura', 'Hamid', '07890001122', 'SW1E 5AG', 'Co-Pilot', 75000.00, '20 Victoria Street, London', 3210, 'yuki.ito@email.com'),
('andrei.popov@email.com', 'Andrei', 'Popov', '07731234567', 'E1W 1BH', 'Pilot', 72000.00, '3 Tower Hill, London', 2198, 'ahmed.ali@email.com'),
('ji-won.kim@email.com', 'Ji-Won', 'Kim', '07981234567', 'EC2A 2CI', 'Cabin Crew', 48000.00, '7 Bishopsgate, London', 2198, 'yuki.ito@email.com'),
('anwar.khouri@email.com', 'Anwar', 'Khouri', '07456789012', 'N1C 4DK', 'Cabin Crew', 45000.00, '22 King\'s Cross Road, London', 2035, 'ahmed.ali@email.com'),
('mei.lin@email.com', 'Mei', 'Lin', '07321012345', 'SW1Y 4EL', 'Cabin Crew', 42000.00, '5 Piccadilly Circus, London', 2198, 'yuki.ito@email.com');






UPDATE addf038_Staff
SET Supervisor_Email = 'yuki.ito@email.com'
WHERE Email = 'rania.abbas@email.com';

UPDATE addf038_Customer
SET Middle_Name = 'Henry'
WHERE Name = 'Jane' AND Surname = 'Smith';
    




/* SECTION 4 - SINGLE TABLE SELECT STATEMENTS */


/* 1) Find out which Flight has the customer Amanda Clark has been on. */

SELECT Flight_Number
FROM addf038_Customer
WHERE Name = 'Amanda' AND Surname = 'Clark';

/* 2) Find destinations with travel time less than 9 hours: */

SELECT Departure_Airport, Arrival_Airport, Travel_Time 
FROM addf038_Destination
WHERE HOUR(Travel_Time)*3600 + MINUTE(Travel_Time)*60 + SECOND(Travel_Time) < 32400;


/* 3) List all the names that are Supervisors */

SELECT Name
FROM addf038_Staff
WHERE Supervisor_Email IS NULL;


/* 4) List all the customers who have Middle names (In Ascending order) */

SELECT *
FROM addf038_Customer
WHERE Middle_Name IS NOT NULL
ORDER BY Middle_Name ASC;

/* 5) List all the Timezones that begin with 'E' or 'G'*/

SELECT DISTINCT Timezone
FROM addf038_Airport
WHERE Timezone LIKE 'E%' OR Timezone LIKE 'G%';



/* 6) Retrieve name, surname and email addresses of staff members who have a salary greater than the average salary of all staff. */

SELECT Name, Surname, Email
FROM addf038_Staff
WHERE Salary > (SELECT AVG(Salary) FROM addf038_Staff);


/* SECTION 5 MULTIPLE TABLE SELECT StATEMENTS */

/* 1) List the names of all customers who have been on the same plane as Ahmed Ali */

SELECT Name, Surname
FROM addf038_Customer
WHERE Flight_Number IN (
SELECT Flight_Number
FROM addf038_Staff
WHERE Email = 'ahmed.ali@email.com');

/* 2) Which airport did the customer John Doe Arrive from and what was his flight number? */

SELECT addf038_Airport.Full_Name, addf038_Customer.Flight_Number
FROM addf038_Customer
JOIN addf038_Flights ON addf038_Customer.Flight_Number = addf038_Flights.Flight_Number
JOIN addf038_Destination ON addf038_Flights.Destination_ID = addf038_Destination.Destination_ID
JOIN addf038_Airport ON addf038_Destination.Arrival_Airport = addf038_Airport.Airport_ID
WHERE addf038_Customer.Name = 'John' AND addf038_Customer.Surname = 'Doe' AND addf038_Customer.Middle_Name IS NULL;


/* 3 List the names of customers who have booked flights departing from Los Angeles International Airport */

SELECT Name, Surname
FROM addf038_Customer
JOIN addf038_Flights ON addf038_Customer.Flight_Number = addf038_Flights.Flight_Number
JOIN addf038_Destination ON addf038_Flights.Destination_ID = addf038_Destination.Destination_ID
JOIN addf038_Airport ON addf038_Destination.Departure_Airport = addf038_Airport.Airport_ID
WHERE addf038_Airport.Airport_ID = 'LAX';

/* 4 List names of the Pilots who are flying planes more than 150 seats and their average salary */

SELECT addf038_Staff.Name, addf038_Staff.Surname, AVG(addf038_Staff.Salary) AS AverageSalary
FROM addf038_Staff 
JOIN addf038_Flights ON addf038_Staff.Flight_Number = addf038_Flights.Flight_Number
JOIN addf038_Plane ON addf038_Flights.Aircraft_Registration_Number = addf038_Plane.Aircraft_Registration_Number
WHERE addf038_Staff.Job_Role = 'Pilot' AND addf038_Plane.Number_Of_Seats > 150
GROUP BY addf038_Staff.Name, addf038_Staff.Surname
HAVING AverageSalary > 70000; 


/* 5 Find the Aircraft registration Number of all planes where there is atleast 1 supervisor on the plane, and the Aircraft reservation Number starts with A */

SELECT addf038_Plane.Aircraft_Registration_Number
FROM addf038_Plane
JOIN addf038_Flights ON addf038_Plane.Aircraft_Registration_Number = addf038_Flights.Aircraft_Registration_Number
JOIN addf038_Staff ON addf038_Flights.Flight_Number = addf038_Staff.Flight_Number
WHERE addf038_Staff.Supervisor_Email IS NULL AND addf038_Plane.Aircraft_Registration_Number LIKE 'B%';


/* 6 for each city thats being used show the amount of customers flying to/from it*/

SELECT City, COUNT(DISTINCT Phone_Number) AS Customer_Count
FROM (
    SELECT a.City, c.Phone_Number
    FROM addf038_Customer c
    JOIN addf038_Flights f ON c.Flight_Number = f.Flight_Number
    JOIN addf038_Destination d ON f.Destination_ID = d.Destination_ID
    JOIN addf038_Airport a ON (d.Departure_Airport = a.Airport_ID OR d.Arrival_Airport = a.Airport_ID)
) AS CustomerFlights
GROUP BY City
ORDER BY Customer_Count DESC;



/* SECTION 6 - DELETE ROWS 

DELETE FROM addf038_Customer 
WHERE Middle_Name = 'Taylor';

DELETE FROM addf038_Staff 
WHERE Email = 'rania.abbas@email.com' AND Phone_Number = '07550123456';

*/


/* SECTION 7 DROP TABLES (make sure the SQL is commented out in this section)

DROP TABLE addf038_Customer;
DROP TABLE addf038_Staff;
DROP TABLE addf038_Flights;
DROP TABLE addf038_Destination;
DROP TABLE addf038_Airport;
DROP TABLE addf038_Plane;

*/




