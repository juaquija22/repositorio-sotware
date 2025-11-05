-- Crear base de datos
CREATE DATABASE `muertes-database` CHARACTER SET utf8mb4];
USE `muertes-database`;

-- Tabla MAYOR_MENOR
CREATE TABLE MAYOR_MENOR (
    idMayorMenor INT PRIMARY KEY AUTO_INCREMENT,
    tipoEdad VARCHAR(20) NOT NULL UNIQUE
) ENGINE=InnoDB;

-- Tabla GRUPO_EDAD_QUINQUENAL
CREATE TABLE GRUPO_EDAD_QUINQUENAL (
    idGrupoEdad INT PRIMARY KEY AUTO_INCREMENT,
    nombreGrupo VARCHAR(20) NOT NULL UNIQUE
) ENGINE=InnoDB;

-- Tabla DEPARTAMENTO
CREATE TABLE DEPARTAMENTO (
    idDepartamento INT PRIMARY KEY AUTO_INCREMENT,
    nombreDepartamento VARCHAR(100) NOT NULL,
    codigoDaneDepartamento VARCHAR(10) NOT NULL UNIQUE
) ENGINE=InnoDB;

-- Tabla MUNICIPIO
CREATE TABLE MUNICIPIO (
    idMunicipio INT PRIMARY KEY AUTO_INCREMENT,
    nombreMunicipio VARCHAR(100) NOT NULL,
    codigoDaneMunicipio VARCHAR(10) NOT NULL UNIQUE,
    idDepartamento INT NOT NULL,
    FOREIGN KEY (idDepartamento) REFERENCES DEPARTAMENTO(idDepartamento)
        ON DELETE RESTRICT ON UPDATE CASCADE
) ENGINE=InnoDB;

-- Tabla PERSONA
CREATE TABLE PERSONA (
    id INT PRIMARY KEY AUTO_INCREMENT,
    idMayorMenor INT,
    estadoCivil VARCHAR(50),
    ancestroRacial VARCHAR(50),
    puebloIndigena VARCHAR(100),
    identidadGenero VARCHAR(50),
    orientacionSexual VARCHAR(50),
    paisNacimiento VARCHAR(100),
    escolaridad VARCHAR(50),
    transgenero VARCHAR(10),
    edad INT,
    idGrupoEdad INT,
    sexo VARCHAR(20),
    FOREIGN KEY (idMayorMenor) REFERENCES MAYOR_MENOR(idMayorMenor)
        ON DELETE SET NULL ON UPDATE CASCADE,
    FOREIGN KEY (idGrupoEdad) REFERENCES GRUPO_EDAD_QUINQUENAL(idGrupoEdad)
        ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

-- Tabla HECHO
CREATE TABLE HECHO (
    idHecho INT PRIMARY KEY AUTO_INCREMENT,
    idPersona INT NOT NULL,
    derecho VARCHAR(100),
    actividadDurante VARCHAR(100),
    mecanismo VARCHAR(100),
    circunstancia VARCHAR(200),
    maneraMuerte VARCHAR(100),
    diagnostico VARCHAR(200),
    FOREIGN KEY (idPersona) REFERENCES PERSONA(id)
        ON DELETE RESTRICT ON UPDATE CASCADE
) ENGINE=InnoDB;

-- Tabla FECHA
CREATE TABLE FECHA (
    idFecha INT PRIMARY KEY AUTO_INCREMENT,
    idHecho INT NOT NULL UNIQUE,
    mesHecho VARCHAR(20),
    diaHecho VARCHAR(2),
    anoHecho VARCHAR(4),
    rangoHora VARCHAR(50),
    FOREIGN KEY (idHecho) REFERENCES HECHO(idHecho)
        ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;

-- Tabla UBICACION
CREATE TABLE UBICACION (
    idUbicacion INT PRIMARY KEY AUTO_INCREMENT,
    idHecho INT NOT NULL UNIQUE,
    localidad VARCHAR(100),
    idMunicipio INT,
    zonaHecho VARCHAR(50),
    escenarioHecho VARCHAR(100),
    FOREIGN KEY (idHecho) REFERENCES HECHO(idHecho)
        ON DELETE CASCADE ON UPDATE CASCADE,
    FOREIGN KEY (idMunicipio) REFERENCES MUNICIPIO(idMunicipio)
        ON DELETE SET NULL ON UPDATE CASCADE
) ENGINE=InnoDB;

-- Índices para mejorar el rendimiento
CREATE INDEX idx_persona_mayormenor ON PERSONA(idMayorMenor);
CREATE INDEX idx_persona_grupoedad ON PERSONA(idGrupoEdad);
CREATE INDEX idx_hecho_persona ON HECHO(idPersona);
CREATE INDEX idx_fecha_hecho ON FECHA(idHecho);
CREATE INDEX idx_ubicacion_hecho ON UBICACION(idHecho);
CREATE INDEX idx_ubicacion_municipio ON UBICACION(idMunicipio);
CREATE INDEX idx_municipio_departamento ON MUNICIPIO(idDepartamento);

-- Insertar datos iniciales en MAYOR_MENOR
INSERT INTO MAYOR_MENOR (tipoEdad) VALUES 
    ('Menor de edad'),
    ('Mayor de edad');

-- Insertar datos iniciales en GRUPO_EDAD_QUINQUENAL
INSERT INTO GRUPO_EDAD_QUINQUENAL (nombreGrupo) VALUES 
    ('0-4 años'),
    ('5-9 años'),
    ('10-14 años'),
    ('15-19 años'),
    ('20-24 años'),
    ('25-29 años'),
    ('30-34 años'),
    ('35-39 años'),
    ('40-44 años'),
    ('45-49 años'),
    ('50-54 años'),
    ('55-59 años'),
    ('60-64 años'),
    ('65-69 años'),
    ('70-74 años'),
    ('75-79 años'),
    ('80+ años');