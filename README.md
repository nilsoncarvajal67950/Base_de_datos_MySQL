# Aerolínea

# Campus-bike

# Empresa_Logistica 👨‍💼

# CÓDIGO

```sql
CREATE DATABASE Envios;
USE Envios;

CREATE TABLE Conductor (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(50),
  Telefono VARCHAR(30),
  Cedula VARCHAR(30)
);

CREATE TABLE Vehiculo (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Placa VARCHAR(30),
  Capacidad DECIMAL(10,2),
  Tipo VARCHAR(60)
);

CREATE TABLE Ruta (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Descripcion VARCHAR(120),
  IdVehiculo_fk INT,
  IdConductor_fk INT,
  CONSTRAINT FK_VehiculoRuta FOREIGN KEY (IdVehiculo_fk) REFERENCES Vehiculo(Id),
  CONSTRAINT FK_ConductorRuta FOREIGN KEY (IdConductor_fk) REFERENCES Conductor(Id)
);

CREATE TABLE Auxiliar (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(50),
  Telefono VARCHAR(13),
  Cedula VARCHAR(20)
);

CREATE TABLE Cliente (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(50),
  Correo VARCHAR(50),
  Telefono VARCHAR(20),
  Direccion VARCHAR(40),
  Cedula VARCHAR(50)
);

CREATE TABLE Pais (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(50)
);

CREATE TABLE Ciudad (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(50),
  IdPais_fk INT,
  CONSTRAINT FK_PaisCiudad FOREIGN KEY (IdPais_fk) REFERENCES Pais(Id)
);

CREATE TABLE Sucursal (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(50),
  Direccion VARCHAR(30),
  IdCiudad_fk INT,
  CONSTRAINT FK_CiudadSucursal FOREIGN KEY (IdCiudad_fk) REFERENCES Ciudad(Id)
);

CREATE TABLE Paquete (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Numero VARCHAR(50),
  Peso DECIMAL(10,2),
  Dimensiones VARCHAR(50),
  Contenido VARCHAR(100),
  Valor DECIMAL(10,2)
);

CREATE TABLE Evento (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Fecha DATE,
  Ubicacion VARCHAR(40),
  Estado VARCHAR(60),
  IdPaquete_fk INT,
  CONSTRAINT FK_PaqueteEvento FOREIGN KEY (IdPaquete_fk) REFERENCES Paquete(Id)
);

CREATE TABLE Envio (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Fecha DATE,
  Estado VARCHAR(50),
  IdCliente_fk INT,
  IdPaquete_fk INT,
  IdRuta_fk INT,
  IdSucursal_fk INT,
  IdAuxiliar_fk INT,
  CONSTRAINT FK_ClienteEnvio FOREIGN KEY (IdCliente_fk) REFERENCES Cliente(Id),
  CONSTRAINT FK_PaqueteEnvio FOREIGN KEY (IdPaquete_fk) REFERENCES Paquete(Id),
  CONSTRAINT FK_RutaEnvio FOREIGN KEY (IdRuta_fk) REFERENCES Ruta(Id),
  CONSTRAINT FK_SucursalEnvio FOREIGN KEY (IdSucursal_fk) REFERENCES Sucursal(Id),
  CONSTRAINT FK_AuxiliarEnvio FOREIGN KEY (IdAuxiliar_fk) REFERENCES Auxiliar(Id)
);
```
# BASE DE DATOS
