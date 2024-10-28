# Aerolínea 🛬

# CÓDIGO

```sql
CREATE DATABASE aerolinea;
USE aerolinea;

-- Tabla de Países
CREATE TABLE Pais (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(30)
);

-- Tabla de Ciudades
CREATE TABLE Ciudad (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(30),
  IdPais_fk INT,
  CONSTRAINT FK_PaisCiudad FOREIGN KEY (IdPais_fk) REFERENCES Pais(Id)
);

-- Tabla de Aeropuertos
CREATE TABLE Aeropuerto (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(30),
  IdCiudad_fk INT,
  CONSTRAINT FK_CiudadAeropuerto FOREIGN KEY (IdCiudad_fk) REFERENCES Ciudad(Id)
);

-- Tabla de Puertas (Gates)
CREATE TABLE Gate (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  NroPuerta INT,
  IdAeropuerto_fk INT,
  CONSTRAINT FK_AeropuertoGate FOREIGN KEY (IdAeropuerto_fk) REFERENCES Aeropuerto(Id)
);

-- Tabla de Aerolíneas
CREATE TABLE Aerolinea (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(30)
);

-- Tabla de Roles de Tripulación
CREATE TABLE RolTripulacion (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(30)
);

-- Tabla de Empleados
CREATE TABLE Empleado (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(30),
  IdRol_fk INT,
  IdAero_fk INT,
  IdAeropuerto_fk INT,
  CONSTRAINT FK_RolEmpleado FOREIGN KEY (IdRol_fk) REFERENCES RolTripulacion(Id),
  CONSTRAINT FK_AeroEmpleado FOREIGN KEY (IdAero_fk) REFERENCES Aerolinea(Id),
  CONSTRAINT FK_AeropuertoEmpleado FOREIGN KEY (IdAeropuerto_fk) REFERENCES Aeropuerto(Id)
);

-- Tabla de Trayectos
CREATE TABLE Trayecto (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  FechaTrayecto DATE,
  Valor DOUBLE,
  CiudadOrigen VARCHAR(30),
  CiudadDestino VARCHAR(30)
);

-- Tabla de Fabricantes
CREATE TABLE Fabricante (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(40)
);

-- Tabla de Modelos de Aviones
CREATE TABLE Modelo (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(30),
  IdFabricante_fk INT,
  CONSTRAINT FK_FabricanteModelo FOREIGN KEY (IdFabricante_fk) REFERENCES Fabricante(Id)
);

-- Tabla de Estados
CREATE TABLE Estado (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(30)
);

-- Tabla de Aviones
CREATE TABLE Avion (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  NroMatricula VARCHAR(30),
  Capacidad INT,
  FechaFabricacion DATE,
  IdEstado_fk INT,
  IdModelo_fk INT,
  IdAero_fk INT,
  CONSTRAINT FK_EstadoAvion FOREIGN KEY (IdEstado_fk) REFERENCES Estado(Id),
  CONSTRAINT FK_ModeloAvion FOREIGN KEY (IdModelo_fk) REFERENCES Modelo(Id),
  CONSTRAINT FK_AeroAvion FOREIGN KEY (IdAero_fk) REFERENCES Aerolinea(Id)
);

-- Tabla de Revisiones de Aviones
CREATE TABLE Revision (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Fecha DATE,
  IdAvion_fk INT,
  CONSTRAINT FK_AvionRevision FOREIGN KEY (IdAvion_fk) REFERENCES Avion(Id)
);

-- Tabla de Empleados en Revisiones
CREATE TABLE RevEmpleado (
  IdEmpleado_fk INT,
  IdRevision_fk INT,
  CONSTRAINT FK_EmpleadoRevEmpleado FOREIGN KEY (IdEmpleado_fk) REFERENCES Empleado(Id),
  CONSTRAINT FK_RevisionEmpleado FOREIGN KEY (IdRevision_fk) REFERENCES Revision(Id)
);

-- Tabla de Reservas de Viaje
CREATE TABLE ReservaViaje (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Fecha DATE,
  IdTrayecto_fk INT,
  CONSTRAINT FK_TrayectoReserva FOREIGN KEY (IdTrayecto_fk) REFERENCES Trayecto(Id)
);

-- Tabla de Tipos de Documento
CREATE TABLE TipoDocumento (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(30)
);

-- Tabla de Clientes
CREATE TABLE Cliente (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Edad INT,
  IdTipo_fk INT,
  CONSTRAINT FK_TipoCliente FOREIGN KEY (IdTipo_fk) REFERENCES TipoDocumento(Id)
);

-- Tabla de Tarifas de Vuelo
CREATE TABLE TarifaVuelo (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  Descripcion VARCHAR(100),
  Valor DECIMAL(10, 2)
);

-- Tabla de Detalles de Reserva
CREATE TABLE DetalleReserva (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  IdCliente_fk INT,
  IdTarifa_fk INT,
  IdReserva_fk INT,
  ValorTarifa DOUBLE,
  CONSTRAINT FK_DetalleCliente FOREIGN KEY (IdCliente_fk) REFERENCES Cliente(Id),
  CONSTRAINT FK_DetalleTarifa FOREIGN KEY (IdTarifa_fk) REFERENCES TarifaVuelo(Id),
  CONSTRAINT FK_DetalleReserva FOREIGN KEY (IdReserva_fk) REFERENCES ReservaViaje(Id)
);

-- Tabla de Escalas
CREATE TABLE Escala (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  IdTrayecto_fk INT,
  IdAvion_fk INT,
  IdGate_fk INT,
  IdAeropuerto_fk INT,
  NroVuelo VARCHAR(20),
  CONSTRAINT FK_TrayectoEscala FOREIGN KEY (IdTrayecto_fk) REFERENCES Trayecto(Id),
  CONSTRAINT FK_EscalaAvion FOREIGN KEY (IdAvion_fk) REFERENCES Avion(Id),
  CONSTRAINT FK_GateEscala FOREIGN KEY (IdGate_fk) REFERENCES Gate(Id),
  CONSTRAINT FK_AeropuertoEscala FOREIGN KEY (IdAeropuerto_fk) REFERENCES Aeropuerto(Id)
);

-- Tabla de Tripulación en Trayectos
CREATE TABLE TrayectoTripulacion (
  IdEmpleado_fk INT,
  IdEscala_fk INT,
  CONSTRAINT FK_EmpleadoTrayecto FOREIGN KEY (IdEmpleado_fk) REFERENCES Empleado(Id),
  CONSTRAINT FK_EscalaTrayecto FOREIGN KEY (IdEscala_fk) REFERENCES Escala(Id)
);

-- Tabla de Detalles de Revisión
CREATE TABLE DetalleRevision (
  Id INT AUTO_INCREMENT PRIMARY KEY,
  IdRevision_fk INT,
  Descripcion VARCHAR(50),
  FechaRev DATE,
  IdEmpleado_fk INT,
  CONSTRAINT FK_RevisionDetalle FOREIGN KEY (IdRevision_fk) REFERENCES Revision(Id),
  CONSTRAINT FK_EmpleadoDetalle FOREIGN KEY (IdEmpleado_fk) REFERENCES Empleado(Id)
);
```
# Campus-bike 🚴

# CÓDIGO

```sql
CREATE DATABASE Campus_bike;
USE Campus_bike;

CREATE TABLE Pais (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(100)
);

CREATE TABLE Region (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(100),
  idPais_fk INT,
  CONSTRAINT FK_PaisRegion FOREIGN KEY (idPais_fk) REFERENCES Pais(id)
);

CREATE TABLE Ciudad (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(100),
  idRegion_fk INT,
  CONSTRAINT FK_RegionCiudad FOREIGN KEY (idRegion_fk) REFERENCES Region(id)
);

CREATE TABLE Sucursal (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(100),
  Direccion VARCHAR(100),
  idCiudad_fk INT,
  CONSTRAINT FK_CiudadSucursal FOREIGN KEY (idCiudad_fk) REFERENCES Ciudad(id)
);

CREATE TABLE TotalVentas (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Total DECIMAL(10,2),
  Fecha DATE,
  idSucursal_fk INT,
  CONSTRAINT FK_SucursalTotalVentas FOREIGN KEY (idSucursal_fk) REFERENCES Sucursal(id)
);

CREATE TABLE SectorVentas (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(100),
  idSucursal_fk INT,
  CONSTRAINT FK_SucursalSectorVentas FOREIGN KEY (idSucursal_fk) REFERENCES Sucursal(id)
);

CREATE TABLE Empleado (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(100),
  Cargo VARCHAR(50),
  Telefono VARCHAR(13),
  Email VARCHAR(100),
  idSucursal_fk INT,
  CONSTRAINT FK_SucursalEmpleado FOREIGN KEY (idSucursal_fk) REFERENCES Sucursal(id)
);

CREATE TABLE Proveedor (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(100),
  Telefono VARCHAR(13),
  Direccion VARCHAR(255),
  Email VARCHAR(100),
  idPais_fk INT,
  CONSTRAINT FK_PaisProveedor FOREIGN KEY (idPais_fk) REFERENCES Pais(id)
);

CREATE TABLE Repuesto (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(100),
  Precio DECIMAL(10,2),
  idProveedor_fk INT,
  CONSTRAINT FK_ProveedorRepuesto FOREIGN KEY (idProveedor_fk) REFERENCES Proveedor(id)
);

CREATE TABLE CuentaSaldar (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Monto DECIMAL(10,2),
  FechaVencimiento DATE,
  Estado VARCHAR(50),
  idProveedor_fk INT,
  CONSTRAINT FK_ProveedorCuentaSaldar FOREIGN KEY (idProveedor_fk) REFERENCES Proveedor(id)
);

CREATE TABLE Producto (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(100),
  Categoria VARCHAR(100),
  Precio DECIMAL(10,2),
  Stock INT,
  idProveedor_fk INT,
  CONSTRAINT FK_ProveedorProducto FOREIGN KEY (idProveedor_fk) REFERENCES Proveedor(id)
);

CREATE TABLE Bicicleta (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Marca VARCHAR(100),
  Tipo VARCHAR(50),
  Valor DECIMAL(10,2),
  idProveedor_fk INT,
  CONSTRAINT FK_ProveedorBicicleta FOREIGN KEY (idProveedor_fk) REFERENCES Proveedor(id)
);

CREATE TABLE Stock (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Cantidad INT,
  idProducto_fk INT,
  idSucursal_fk INT,
  CONSTRAINT FK_ProductoStock FOREIGN KEY (idProducto_fk) REFERENCES Producto(id),
  CONSTRAINT FK_SucursalStock FOREIGN KEY (idSucursal_fk) REFERENCES Sucursal(id)
);

CREATE TABLE Estado (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Transito VARCHAR(30),
  Entrega VARCHAR(30),
  Entregado VARCHAR(30),
  idProducto_fk INT,
  CONSTRAINT FK_ProductoEstado FOREIGN KEY (idProducto_fk) REFERENCES Producto(id)
);

CREATE TABLE Cliente (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Nombre VARCHAR(50),
  Direccion VARCHAR(50),
  Telefono VARCHAR(13),
  Email VARCHAR(150),
  idPais_fk INT,
  CONSTRAINT FK_PaisCliente FOREIGN KEY (idPais_fk) REFERENCES Pais(id)
);

CREATE TABLE Pedido (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Cantidad INT,
  Fecha DATE,
  idEstado_fk INT,
  idCliente_fk INT,
  idProducto_fk INT,
  CONSTRAINT FK_EstadoPedido FOREIGN KEY (idEstado_fk) REFERENCES Estado(id),
  CONSTRAINT FK_ClientePedido FOREIGN KEY (idCliente_fk) REFERENCES Cliente(id),
  CONSTRAINT FK_ProductoPedido FOREIGN KEY (idProducto_fk) REFERENCES Producto(id)
);

CREATE TABLE Fecha (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Fecha DATE,
  Descripcion VARCHAR(50)
);

CREATE TABLE Venta (
  id INT AUTO_INCREMENT PRIMARY KEY,
  idFecha_fk INT,
  Cantidad INT,
  Total DECIMAL(20,2),
  idCliente_fk INT,
  idBicicleta_fk INT,
  idEmpleado_fk INT,
  CONSTRAINT FK_FechaVenta FOREIGN KEY (idFecha_fk) REFERENCES Fecha(id),
  CONSTRAINT FK_ClienteVenta FOREIGN KEY (idCliente_fk) REFERENCES Cliente(id),
  CONSTRAINT FK_EmpleadoVenta FOREIGN KEY (idEmpleado_fk) REFERENCES Empleado(id)
);

CREATE TABLE Pago (
  id INT AUTO_INCREMENT PRIMARY KEY,
  TipoPago VARCHAR(50),
  Monto DECIMAL(20,2),
  Fecha DATE,
  idVenta_fk INT,
  CONSTRAINT FK_VentaPago FOREIGN KEY (idVenta_fk) REFERENCES Venta(id)
);

CREATE TABLE Facturacion (
  id INT AUTO_INCREMENT PRIMARY KEY,
  Total DECIMAL(20,2),
  idVenta_fk INT,
  CONSTRAINT FK_VentaFacturacion FOREIGN KEY (idVenta_fk) REFERENCES Venta(id)
);
```
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
