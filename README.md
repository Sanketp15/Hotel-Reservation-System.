DROP DATABASE IF EXISTS Hotel;

CREATE DATABASE Hotel;


USE Hotel;

CREATE TABLE Room (
    RoomNumber INT PRIMARY KEY NOT NULL,
    RoomType VARCHAR(10) NOT NULL,
    IsADA TINYINT(1) NOT NULL,
    StandardOccupancy INT NOT NULL,
    MaximumOccupancy INT NOT NULL,
    BasePrice DECIMAL(5 , 2 ) NOT NULL,
    ExtraPerson DECIMAL(4 , 2 ) NOT NULL,
    HasJacuzzi TINYINT(1) NOT NULL
);
CREATE TABLE Amenity (
    AmenityId INT PRIMARY KEY AUTO_INCREMENT,
    AmenityType VARCHAR(30)
);
CREATE TABLE RoomAmenity (
    RoomNumber INT NOT NULL,
    AmenityId INT NOT NULL,
    PRIMARY KEY pk_RoomAmenity (RoomNumber, AmenityId),
	FOREIGN KEY fk_RoomAmenity_Room (RoomNumber)
		REFERENCES Room(RoomNumber),
	FOREIGN KEY fk_RoomAmenity_Amenity (AmenityId)
		REFERENCES Amenity(AmenityId)
);
CREATE TABLE Reservation (
	ReservationId INT PRIMARY KEY AUTO_INCREMENT,
    Adults INT NOT NULL,
    Children INT NOT NULL,
    CheckInDate DATE,
    CheckOutDate DATE,
    Total DECIMAL(8,2) NOT NULL
);
CREATE TABLE Guest (
	GuestId INT PRIMARY KEY AUTO_INCREMENT,
    FirstName varchar(50) NOT NULL,
    LastName varchar(50) NOT NULL,
    Street varchar(100),
    City varchar(50),
    State char(2),
    Zip char(5),
    Phone char(14)
);
CREATE TABLE GuestReservation (
	GuestId INT,
    ReservationId INT,
    PRIMARY KEY pk_GuestReservation (GuestId, ReservationId),
    FOREIGN KEY fk_GuestReservation_Guest (GuestId)
		REFERENCES Guest (GuestId),
	FOREIGN KEY fk_GuestReservation_Reservation (ReservationId)
		REFERENCES Reservation (ReservationId)
);
CREATE TABLE RoomReservation(
	RoomNumber INT,
    ReservationId INT,
    PRIMARY KEY pk_RoomReservation (RoomNumber, ReservationId),
    FOREIGN KEY fk_RoomReservation_Room (RoomNumber)
		REFERENCES Room (RoomNumber),
	FOREIGN KEY fk_RoomReservation_Reservation (ReservationId)
		REFERENCES Reservation (ReservationId)
);
Use Hotel;

INSERT INTO Amenity (AmenityType) VALUES 
    ('Microwave'),
    ('Refrigerator'),
    ('Oven');
INSERT INTO Room (RoomNumber, RoomType, IsADA, StandardOccupancy, MaximumOccupancy, BasePrice, ExtraPerson, HasJacuzzi) VALUES
    (201,'Double',0,2,4,199.99,10.00,1),
    (202,'Double',1,2,4,174.99,10.00,0),
    (203,'Double',0,2,4,199.99,10.00,1),
    (204,'Double',1,2,4,174.99,10.00,0),
    (205,'Single',0,2,2,174.99,0.00,1),
    (206,'Single',1,2,2,149.99,0.00,0),
    (207,'Single',0,2,2,174.99,0.00,1),
    (208,'Single',1,2,2,149.99,0.00,0),
    (301,'Double',0,2,4,199.99,10.00,1),
    (302,'Double',1,2,4,174.99,10.00,0),
    (303,'Double',0,2,4,199.99,10.00,1),
    (304,'Double',1,2,4,174.99,10.00,0),
    (305,'Single',0,2,2,174.99,0.00,1),
    (306,'Single',1,2,2,149.99,0.00,0),
    (307,'Single',0,2,2,174.99,0.00,1),
    (308,'Single',1,2,2,149.99,0.00,0),
    (401,'Suite',1,3,8,399.99,20.00,0),
    (402,'Suite',1,3,8,399.99,20.00,0);
    
    INSERT INTO RoomAmenity (RoomNumber, AmenityId) VALUES
    (201,1),
    (202,2),
    (203,1),
    (204,2),
    (205,1),
    (205,2),
    (206,1),
    (206,2),
    (207,1),
    (207,2),
    (208,1),
    (208,2),
    (301,1),
    (302,2),
    (303,1),
    (304,2),
    (305,1),
    (305,2),
    (306,1),
    (306,2),
    (307,1),
    (307,2),
    (308,1),
    (308,2),
    (401,1),
    (401,2),
    (401,3),
    (402,1),
    (402,2),
    (402,3);
    
INSERT INTO Guest (FirstName, LastName, Street, City, State, Zip, Phone) VALUES
    ('Eric','Riddle','555 Imaginary Ln.', 'Loserville', 'KY', '55514','(555) 555-5555'),
    ('Mack','Simmer','379 Old Shore Street','Council Bluffs','IA',51501,'(291) 553-0508'),
    ('Bettyann','Seery','750 Wintergreen Dr.','Wasilla','AK',99654,'(478) 277-9632'),
    ('Duane','Cullison','9662 Foxrun Lane','Harlingen','TX',78552,'(308) 494-0198'),
    ('Karie','Yang','9378 W. Augusta Ave.','West Deptford','NJ',8096,'(214) 730-0298'),
    ('Aurore','Lipton','762 Wild Rose Street','Saginaw','MI',48601,'(377) 507-0974'),
    ('Zachery','Luechtefield','7 Poplar Dr.','Arvada','CO',80003,'(814) 485-2615'),
    ('Jeremiah','Pendergrass','70 Oakwood St.','Zion','IL',60099,'(279) 491-0960'),
    ('Walter','Holaway','7556 Arrowhead St.','Cumberland','RI',2864,'(446) 396-6785'),
    ('Wilfred','Vise','77 West Surrey Street','Oswego','NY',13126,'(834) 727-1001'),
    ('Maritza','Tilton','939 Linda Rd.','Burke','VA',22015,'(446) 351-6860'),
    ('Joleen','Tison','87 Queen St.','Drexel Hill','PA',19026,'(231) 893-2755');
        
INSERT INTO Reservation (Adults, Children, CheckInDate, CheckOutDate, Total) VALUES
    (1,0,'2023-02-02 00:00:00','2023-02-04 00:00:00',299.98),
    (2,1,'2023-02-05 00:00:00','2023-02-10 00:00:00',999.95),
    (2,0,'2023-02-22 00:00:00','2023-02-24 00:00:00',349.98),
    (2,2,'2023-03-06 00:00:00','2023-03-07 00:00:00',199.99),
    (1,1,'2023-03-17 00:00:00','2023-03-20 00:00:00',524.97),
    (3,0,'2023-03-18 00:00:00','2023-03-23 00:00:00',924.95),
    (2,2,'2023-03-29 00:00:00','2023-03-31 00:00:00',349.98),
    (2,0,'2023-03-31 00:00:00','2023-04-05 00:00:00',874.95),
    (1,0,'2023-04-09 00:00:00','2023-04-13 00:00:00',799.96),
    (1,1,'2023-04-23 00:00:00','2023-04-24 00:00:00',174.99),
    (2,4,'2023-05-30 00:00:00','2023-06-02 00:00:00',1199.97),
    (2,0,'2023-06-10 00:00:00','2023-06-14 00:00:00',599.96),
    (1,0,'2023-06-10 00:00:00','2023-06-14 00:00:00',599.96),
    (3,0,'2023-06-17 00:00:00','2023-06-18 00:00:00',184.99),
    (2,0,'2023-06-28 00:00:00','2023-07-02 00:00:00',699.96),
    (3,1,'2023-07-13 00:00:00','2023-07-14 00:00:00',184.99),
    (4,2,'2023-07-18 00:00:00','2023-07-21 00:00:00',1259.97),
    (2,1,'2023-07-28 00:00:00','2023-07-29 00:00:00',199.99),
    (1,0,'2023-08-30 00:00:00','2023-09-01 00:00:00',349.98),
    (2,0,'2023-09-16 00:00:00','2023-09-17 00:00:00',149.99),
    (2,2,'2023-09-13 00:00:00','2023-09-15 00:00:00',399.98),
    (2,2,'2023-11-22 00:00:00','2023-11-25 00:00:00',1199.97),
    (2,0,'2023-11-22 00:00:00','2023-11-25 00:00:00',449.97),
    (2,2,'2023-11-22 00:00:00','2023-11-25 00:00:00',599.97),
    (2,0,'2023-12-24 00:00:00','2023-12-28 00:00:00',699.96);

INSERT INTO GuestReservation (GuestId, ReservationId) VALUES
    (2,1),
    (3,2),
    (4,3),
    (5,4),
    (1,5),
    (6,6),
    (7,7),
    (8,8),
    (9,9),
    (10,10),
    (11,11),
    (12,12),
    (12,13),
    (6,14),
    (1,15),
    (9,16),
    (10,17),
    (3,18),
    (3,19),
    (2,20),
    (5,21),
    (4,22),
    (2,23),
    (2,24),
    (11,25); 
    
 INSERT INTO RoomReservation (RoomNumber, ReservationId) VALUES
    (308,1),
    (203,2),
    (305,3),
    (201,4),
    (307,5),
    (302,6),
    (202,7),
    (304,8),
    (301,9),
    (207,10),
    (401,11),
    (206,12),
    (208,13),
    (304,14),
    (205,15),
    (204,16),
    (401,17),
    (303,18),
    (305,19),
    (208,20),
    (203,21),
    (401,22),
    (206,23),
    (301,24),
    (302,25);
    
-- Removing Jeremiah Pendergrass and his reservations
    DELETE FROM GuestReservation WHERE GuestId = 8;
    DELETE FROM Guest WHERE GuestId = 8;
    DELETE FROM RoomReservation WHERE ReservationId = 8;
	DELETE FROM Reservation WHERE ReservationId = 8;

USE Hotel;

-- QUERY 1
-- Write a query that returns a list of reservations that end in July 2023, 
-- including the name of the guest, the room number(s), and the reservation dates.
--------------------
SELECT 
	Guest.FirstName,
    Guest.LastName,
    Room.RoomNumber,
    Reservation.CheckInDate,
    Reservation.CheckOutDate
FROM Guest
INNER JOIN GuestReservation ON Guest.GuestId = GuestReservation.GuestId
INNER JOIN Reservation ON  GuestReservation.ReservationId = Reservation.ReservationId
INNER JOIN RoomReservation ON Reservation.ReservationId = RoomReservation.ReservationId
INNER JOIN Room ON RoomReservation.RoomNumber = Room.RoomNumber
WHERE CheckOutDate BETWEEN '2023-07-01' AND '2023-07-31';

-- QUERY 2
-- Write a query that returns a list of all reservations for rooms with a jacuzzi, 
-- displaying the guest's name, the room number, and the dates of the reservation.
--------------------
SELECT
	Guest.FirstName,
    Guest.LastName,
    Room.RoomNumber,
    Reservation.CheckInDate,
    Reservation.CheckOutDate
FROM Room
INNER JOIN RoomReservation ON Room.RoomNumber = RoomReservation.RoomNumber
INNER JOIN Reservation ON RoomReservation.ReservationId = Reservation.ReservationId
INNER JOIN GuestReservation ON Reservation.ReservationId = GuestReservation.ReservationId
INNER JOIN Guest ON GuestReservation.GuestId = Guest.GuestId
WHERE HasJacuzzi = 1;

-- QUERY 3
-- Write a query that returns all the rooms reserved for a specific guest, 
-- including the guest's name, the room(s) reserved, the starting date of the reservation, 
-- and how many people were included in the reservation. (Choose a guest's name from the existing data.)
--------------------
SELECT
	Guest.FirstName,
    Guest.LastName,
    Room.RoomNumber,
    Reservation.CheckInDate,
    Reservation.CheckOutDate,
    Reservation.Adults + Reservation.Children AS TotalPeople
FROM Guest
INNER JOIN GuestReservation ON Guest.GuestId = GuestReservation.GuestId
INNER JOIN Reservation ON  GuestReservation.ReservationId = Reservation.ReservationId
INNER JOIN RoomReservation ON Reservation.ReservationId = RoomReservation.ReservationId
INNER JOIN Room ON RoomReservation.RoomNumber = Room.RoomNumber
WHERE Guest.GuestId = 2;

-- QUERY 4
-- Write a query that returns a list of rooms, reservation ID, and per-room cost for each reservation. 
-- The results should include all rooms, whether or not there is a reservation associated with the room.
--------------------
SELECT
	Room.RoomNumber,
    Reservation.ReservationId,
    CASE
		WHEN (((Room.RoomNumber BETWEEN '201' AND '204') OR (Room.RoomNumber BETWEEN '301' AND '304')) AND Reservation.Adults <= 2)
			THEN ((Room.BasePrice) * DATEDIFF(Reservation.CheckOutDate, Reservation.CheckInDate))
		 WHEN (((Room.RoomNumber BETWEEN '201' AND '204') OR (Room.RoomNumber BETWEEN '301' AND '304')) AND Reservation.Adults > 2)
			 THEN ((Room.BasePrice + ((Reservation.Adults - Room.StandardOccupancy) * 10) * DATEDIFF(Reservation.CheckOutDate, Reservation.CheckInDate)))
		WHEN ((Room.RoomNumber BETWEEN '205' AND '208') OR (Room.RoomNumber BETWEEN '305' AND '308'))
			 THEN ((Room.BasePrice) * DATEDIFF(Reservation.CheckOutDate, Reservation.CheckInDate))
		WHEN (((Room.RoomNumber BETWEEN '401' AND '402')) AND Reservation.Adults <= 3)
			THEN ((Room.BasePrice) * DATEDIFF(Reservation.CheckOutDate, Reservation.CheckInDate))
		WHEN (((Room.RoomNumber BETWEEN '401' AND '402')) AND Reservation.Adults > 3)
			THEN ((Room.BasePrice + ((Reservation.Adults - Room.StandardOccupancy) * 20) * DATEDIFF(Reservation.CheckOutDate, Reservation.CheckInDate)))
	END AS Total
FROM Guest
RIGHT OUTER JOIN GuestReservation ON Guest.GuestId = GuestReservation.GuestId
RIGHT OUTER JOIN Reservation ON  GuestReservation.ReservationId = Reservation.ReservationId
RIGHT OUTER JOIN RoomReservation ON Reservation.ReservationId = RoomReservation.ReservationId
RIGHT OUTER JOIN Room ON RoomReservation.RoomNumber = Room.RoomNumber;
    
-- QUERY 5
-- Write a query that returns all the rooms accommodating at least 
-- three guests and that are reserved on any date in April 2023.
SELECT 
	Room.RoomNumber
FROM RESERVATION
INNER JOIN RoomReservation ON Reservation.ReservationId = RoomReservation.ReservationId
INNER JOIN Room ON RoomReservation.RoomNumber = Room.RoomNumber
WHERE 	(Reservation.Adults + Reservation.Children) > 2
		AND ((Reservation.CheckInDate BETWEEN '2023-04-01' AND '2023-04-30')
		OR (Reservation.CheckOutDate BETWEEN '2023-04-01' AND '2023-04-30'));    

-- QUERY 6
-- Write a query that returns a list of all guest names and the number of reservations per guest, 
-- sorted starting with the guest with the most reservations and then by the guest's last name.
--------------------
SELECT 
	g.Firstname,
    g.Lastname,
    COUNT(gr.GuestId) AS TotalReservations
FROM Reservation r
INNER JOIN GuestReservation gr ON r.ReservationId = gr.ReservationId
INNER JOIN Guest g ON gr.GuestId = g.GuestId
GROUP BY g.FirstName
ORDER BY TotalReservations DESC, g.LastName; 

-- QUERY 7
-- Write a query that displays the name, address, and phone number of a guest 
-- based on their phone number. (Choose a phone number from the existing data.)
--------------------
SELECT 
	g.FirstName,
    g.LastName,
    g.Street,
    g.City,
    g.State,
    g.Zip,
    g.Phone
FROM GUEST g
WHERE g.Phone LIKE '%(291) 553-0508%';       
    
    
