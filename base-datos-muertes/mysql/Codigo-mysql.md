-- ============================================
-- CREACIÓN DE TABLAS DEL MODELO ENTIDAD-RELACIÓN
-- ============================================

CREATE DATABASE muertes_accidentales;
USE muertes_accidentales;

-- === CATÁLOGOS PERSONA ===

CREATE TABLE ESTADO_CIVIL (
    idEstadoCivil INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL
);

CREATE TABLE ANCESTRO_RACIAL (
    idAncestroRacial INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL
);

CREATE TABLE PUEBLO_INDIGENA (
    idPuebloIndigena INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL
);

CREATE TABLE IDENTIDAD_GENERO (
    idIdentidadGenero INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL
);

CREATE TABLE ORIENTACION_SEXUAL (
    idOrientacionSexual INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL
);

CREATE TABLE PAIS (
    idPais INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    codigoISO VARCHAR(10)
);

CREATE TABLE ESCOLARIDAD (
    idEscolaridad INT PRIMARY KEY AUTO_INCREMENT,
    nivel VARCHAR(100) NOT NULL
);

CREATE TABLE TRANSGENERO (
    idTransgenero INT PRIMARY KEY AUTO_INCREMENT,
    descripcion VARCHAR(100) NOT NULL
);

CREATE TABLE SEXO (
    idSexo INT PRIMARY KEY AUTO_INCREMENT,
    tipoSexo VARCHAR(50) NOT NULL
);

CREATE TABLE MAYOR_MENOR (
    idMayorMenor INT PRIMARY KEY AUTO_INCREMENT,
    tipoEdad VARCHAR(50) NOT NULL
);

CREATE TABLE GRUPO_EDAD_QUINQUENAL (
    idGrupoEdad INT PRIMARY KEY AUTO_INCREMENT,
    nombreGrupo VARCHAR(100) NOT NULL
);

-- === DEPARTAMENTO Y MUNICIPIO ===

CREATE TABLE DEPARTAMENTO (
    idDepartamento INT PRIMARY KEY AUTO_INCREMENT,
    nombreDepartamento VARCHAR(100) NOT NULL,
    codigoDaneDepartamento VARCHAR(20),
    idPais INT,
    FOREIGN KEY (idPais) REFERENCES PAIS(idPais)
);

CREATE TABLE MUNICIPIO (
    idMunicipio INT PRIMARY KEY AUTO_INCREMENT,
    nombreMunicipio VARCHAR(100) NOT NULL,
    codigoDaneMunicipio VARCHAR(20),
    idDepartamento INT,
    FOREIGN KEY (idDepartamento) REFERENCES DEPARTAMENTO(idDepartamento)
);

-- === ENTIDAD PRINCIPAL: PERSONA ===

CREATE TABLE PERSONA (
    id INT PRIMARY KEY AUTO_INCREMENT,
    idMayorMenor INT,
    idEstadoCivil INT,
    idAncestroRacial INT,
    idPuebloIndigena INT,
    idIdentidadGenero INT,
    idOrientacionSexual INT,
    idPaisNacimiento INT,
    idEscolaridad INT,
    idTransgenero INT,
    idGrupoEdad INT,
    idSexo INT,
    edad INT,

    FOREIGN KEY (idMayorMenor) REFERENCES MAYOR_MENOR(idMayorMenor),
    FOREIGN KEY (idEstadoCivil) REFERENCES ESTADO_CIVIL(idEstadoCivil),
    FOREIGN KEY (idAncestroRacial) REFERENCES ANCESTRO_RACIAL(idAncestroRacial),
    FOREIGN KEY (idPuebloIndigena) REFERENCES PUEBLO_INDIGENA(idPuebloIndigena),
    FOREIGN KEY (idIdentidadGenero) REFERENCES IDENTIDAD_GENERO(idIdentidadGenero),
    FOREIGN KEY (idOrientacionSexual) REFERENCES ORIENTACION_SEXUAL(idOrientacionSexual),
    FOREIGN KEY (idPaisNacimiento) REFERENCES PAIS(idPais),
    FOREIGN KEY (idEscolaridad) REFERENCES ESCOLARIDAD(idEscolaridad),
    FOREIGN KEY (idTransgenero) REFERENCES TRANSGENERO(idTransgenero),
    FOREIGN KEY (idGrupoEdad) REFERENCES GRUPO_EDAD_QUINQUENAL(idGrupoEdad),
    FOREIGN KEY (idSexo) REFERENCES SEXO(idSexo)
);

-- === HECHO Y SUS DEPENDENCIAS ===

CREATE TABLE HECHO (
    idHecho INT PRIMARY KEY AUTO_INCREMENT,
    idPersona INT,
    descripcionDerecho VARCHAR(255),
    actividadDurante VARCHAR(255),
    mecanismo VARCHAR(255),
    circunstancia VARCHAR(255),
    maneraMuerte VARCHAR(255),
    diagnostico VARCHAR(255),

    FOREIGN KEY (idPersona) REFERENCES PERSONA(id)
);

CREATE TABLE FECHA (
    idFecha INT PRIMARY KEY AUTO_INCREMENT,
    idHecho INT,
    dia INT,
    mes INT,
    ano INT,
    rangoHora VARCHAR(50),
    FOREIGN KEY (idHecho) REFERENCES HECHO(idHecho)
);

CREATE TABLE UBICACION (
    idUbicacion INT PRIMARY KEY AUTO_INCREMENT,
    idHecho INT,
    localidad VARCHAR(100),
    idMunicipio INT,
    zonaHecho VARCHAR(100),
    escenarioHecho VARCHAR(100),
    FOREIGN KEY (idHecho) REFERENCES HECHO(idHecho),
    FOREIGN KEY (idMunicipio) REFERENCES MUNICIPIO(idMunicipio)
);


