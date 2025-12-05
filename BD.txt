-- Create database
CREATE DATABASE IF NOT EXISTS grade_management;
USE grade_management;

-- Create users table
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Create UEs table
CREATE TABLE ues (
    id VARCHAR(10) PRIMARY KEY,
    code VARCHAR(10) NOT NULL,
    nom VARCHAR(100) NOT NULL,
    credit INT NOT NULL
);

-- Create ECUEs table
CREATE TABLE ecues (
    id VARCHAR(10) PRIMARY KEY,
    ue_id VARCHAR(10) NOT NULL,
    nom VARCHAR(150) NOT NULL,
    coef FLOAT NOT NULL,
    FOREIGN KEY (ue_id) REFERENCES ues(id)
);

-- Create grades table
CREATE TABLE grades (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    ecue_id VARCHAR(10) NOT NULL,
    cc FLOAT,
    tp FLOAT,
    examen FLOAT,
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (ecue_id) REFERENCES ecues(id),
    UNIQUE KEY unique_user_ecue (user_id, ecue_id)
);

-- Insert sample data
INSERT INTO ues (id, code, nom, credit) VALUES
('uef310', 'UEF310', 'Probabilité', 4),
('uef320', 'UEF320', 'Automates et Optimisation', 4),
('uef330', 'UEF330', 'CPOO', 7),
('uef340', 'UEF340', 'Bases de données et Réseaux', 5),
('uet310', 'UET310', 'Langue et Culture d''Entreprise', 4),
('ueo310', 'UEO310', 'Unité optionnelle', 6);

INSERT INTO ecues (id, ue_id, nom, coef) VALUES
('uef311', 'uef310', 'ECUEF311 – Probabilité et statistique', 2),
('uef321', 'uef320', 'ECUEF321 – Théorie des langages et Automates', 1),
('uef322', 'uef320', 'ECUEF322 – Graphes et optimisation', 1),
('uef331', 'uef330', 'ECUEF331 – Conception des Systèmes d''Information', 1.5),
('uef332', 'uef330', 'ECUEF332 – Programmation Java', 2),
('uef341', 'uef340', 'ECUEF341 – Ingénierie des Bases de Données', 1.5),
('uef342', 'uef340', 'ECUEF342 – Services des Réseaux', 1),
('uet311', 'uet310', 'ECUET311 – Anglais 3', 1),
('uet312', 'uet310', 'ECUET312 – Gestion d''entreprise', 1),
('ueo311', 'ueo310', 'ECUEO311 – Génie Logiciel', 1.5),
('ueo312', 'ueo310', 'ECUEO312 – Design Graphique', 1.5);