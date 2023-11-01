# PushUpEnvia

Prueba

<h1>Comandos DDL</1h>

- CREATE = Crear
- ALTER = Modificar
- DROP = Eliminar
- TRUNCATE = Eliminar todos los registros
- RENAME = Cambiar el nombre de un objeto existente

<h1>Comandos DML</h1>

- SELECT = Recuperar datos de una o varias tablas
- INSERT = Insertar nuevos registros en una tabla
- UPDATE = Actualizar valores de uno o varios regritros de una tabla
- DELETE = Eliminar uno o varios registros de una tabla

<h1>Comandos DQL</h1>

- SELECT = Seleccionar y recuperar
- FROM = Se utiliza junto a el comando SELECT para especificar la tabla o tablas desde las cuales se deben recuperar los datos
- WHERE = filtrar los registros que cumplen ciertas condiciones en una consulta.

# COMANDOS DE MySql
CREATE DATABASE Envia;
SHOW DATABASES;
USE Envia;

CREATE TABLE Usuarios (
  ID_usuario INT PRIMARY KEY,
  Nombre VARCHAR(255),
  Direccion VARCHAR(255),
  Correo_electronico VARCHAR(255),
  Contraseña VARCHAR(255)
);

CREATE TABLE Direcciones (
  ID_direccion INT PRIMARY KEY,
  Direccion VARCHAR(255)
);


CREATE TABLE Detalles_Paquetes (
  ID_detalle INT PRIMARY KEY,
  Descripcion VARCHAR(255),
  ID_paquete INT,
  FOREIGN KEY (ID_paquete) REFERENCES Paquetes(ID_paquete)
);
CREATE TABLE Paquetes (
  ID_paquete INT PRIMARY KEY,
  Peso DECIMAL(10,2),
  Dimensiones VARCHAR(255),
  ID_usuario INT,
  ID_direccion_origen INT,
  ID_direccion_destino INT,
  FOREIGN KEY (ID_usuario) REFERENCES Usuarios(ID_usuario),
  FOREIGN KEY (ID_direccion_origen) REFERENCES Direcciones(ID_direccion),
  FOREIGN KEY (ID_direccion_destino) REFERENCES Direcciones(ID_direccion)
);


CREATE TABLE Seguimientos (
  ID_seguimiento INT PRIMARY KEY,
  ID_paquete INT,
  Estado VARCHAR(255),
  Ubicacion VARCHAR(255),
  Fecha_hora DATETIME,
  FOREIGN KEY (ID_paquete) REFERENCES Paquetes(ID_paquete)
);


CREATE TABLE Rutas (
  ID_ruta INT PRIMARY KEY,
  ID_direccion_origen INT,
  ID_direccion_destino INT,
  Distancia DECIMAL(10,2),
  Duracion_estimada TIME,
  FOREIGN KEY (ID_direccion_origen) REFERENCES Direcciones(ID_direccion),
  FOREIGN KEY (ID_direccion_destino) REFERENCES Direcciones(ID_direccion)
);


CREATE TABLE Transportistas (
  ID_transportista INT PRIMARY KEY,
  Nombre VARCHAR(255),
  Tipo_servicio VARCHAR(255),
  Tarifa DECIMAL(10,2)
);

CREATE TABLE Envios (
  ID_envio INT PRIMARY KEY,
  ID_paquete INT,
  ID_transportista INT,
  Fecha_envio DATE,
  FOREIGN KEY (ID_paquete) REFERENCES Paquetes(ID_paquete),
  FOREIGN KEY (ID_transportista) REFERENCES Transportistas(ID_transportista)
);

Tabla "Facturas":
CREATE TABLE Facturas (
  ID_factura INT PRIMARY KEY,
  ID_envio INT,
  Monto DECIMAL(10,2),
  Fecha_factura DATE,
  FOREIGN KEY (ID_envio) REFERENCES Envios(ID_envio)
);

