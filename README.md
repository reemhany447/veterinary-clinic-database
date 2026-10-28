# veterinary-clinic-database
A relational MySQL database for managing veterinarians, pet owners, pets, and appointments in a veterinary clinic.

DROP DATABASE IF EXISTS PetClinicDB;
CREATE DATABASE PetClinicDB;
USE PetClinicDB;

CREATE TABLE Owners(
    OwnersID INT UNIQUE,
    Name VARCHAR(20) NOT NULL,
    DateOfBirth DATE,
    PhoneNumber VARCHAR(15),
    CONSTRAINT uq_PhoneNumber UNIQUE (PhoneNumber),
    PRIMARY KEY (OwnersID)
);

CREATE TABLE Pets(
    PetsID INT UNIQUE,
    Name VARCHAR(15) NOT NULL,
    Weight INT,
    Type VARCHAR(20) DEFAULT 'Cat',
    CONSTRAINT chk_Weight CHECK (Weight > 0),
    PRIMARY KEY (PetsID)
);

CREATE TABLE Own(
    OwnersID INT,
    PetsID INT,
    Name VARCHAR(20),
    DateOfBirth DATE,
    PhoneNumber VARCHAR(15),
    PRIMARY KEY (OwnersID, PetsID),
    FOREIGN KEY (OwnersID) REFERENCES Owners(OwnersID),
    FOREIGN KEY (PetsID) REFERENCES Pets(PetsID)
);

INSERT INTO Owners
VALUES (1, 'Karim Hassan', '1990-03-15', '01012345678'),
       (2, 'Salma Nabil',  '1995-07-08', '01198765432'),
       (3, 'Ziad Kamal',   '1988-11-02', NULL);

INSERT INTO Pets
VALUES (1, 'Max',   12, 'Dog'),
       (2, 'Luna',  4,  'Cat'),
       (3, 'Bella', 3,  'Rabbit'),
       (4, 'Simba', 5,  DEFAULT);

SELECT OwnersID, Name, DateOfBirth, PhoneNumber
FROM Owners;

SELECT PetsID, Name, Weight, Type
FROM Pets
WHERE Weight BETWEEN 3 AND 5;
