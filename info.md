//Crea el archivo json
npm init -y

//Instalo
npm install express ejs nodemon
npm -g install nodemon

//Controladores sqlitecloud
npm install @sqlitecloud/drivers 

//Comando de ejecucioon node
node app(es el nombre del archivo js), limitado a detener la ejecucion para los cambios
o
nodemon app, ejecuta los cambios en tiempo real.


//Base de datos

CREATE TABLE banderas (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nombre TEXT NOT NULL
);

CREATE TABLE tipos (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    clase TEXT NOT NULL
    subclase TEXT NOT NULL
);

CREATE TABLE medios_gc (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nombre TEXT NOT NULL
);

CREATE TABLE buques (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nombre TEXT NOT NULL,
    bandera_id INTEGER,
    mmsi TEXT,
    imo TEXT,
    call_sign TEXT,
    tipo_id INTEGER,  -- Cambié el nombre de la columna a tipo_id para reflejar la clave foránea
    medio_gc_id INTEGER,
    latitud REAL,
    longitud REAL,
    detalle TEXT,
    FOREIGN KEY (bandera_id) REFERENCES banderas(id),
    FOREIGN KEY (tipo_id) REFERENCES tipos(id),  -- Actualizado el nombre de la tabla y la columna
    FOREIGN KEY (medio_gc_id) REFERENCES medios_gc(id)
);


INSERT INTO buques (nombre, bandera_id, mmsi, imo, call_sign, tipo_id, medio_gc_id, latitud, longitud, detalle)
VALUES 
    ("FU YUAN YU 9996", (SELECT id FROM banderas WHERE nombre = "China"), "412331265", "8795655", "BTR34", (SELECT id FROM tipos WHERE clase = "Pesquero" AND subclase = "Polivalente"), (SELECT id FROM medios_gc WHERE nombre = "GC-28 DERBES"), 44.632, -57.286, "No detectado en infracción");


-----------Insertando datos

INSERT INTO tipos (clase, subclase) 
VALUES 
    ("Pesquero", "Arrastrero"),
    ("Pesquero", "Palangrero"),
    ("Pesquero", "Potero"),
    ("Pesquero", "Polivalente"),
    ("Pesquero", "Pesquero no identificado");

INSERT INTO medios_gc (nombre)
VALUES 
    ("GC-24 MANTILLA"),
    ("GC-25 AZOPARDO"),
    ("GC-27 THOMPSON"),
    ("GC-28 DERBES")



  L.marker([buque.latitud, buque.longitud])
            .bindPopup('<b><%= buque.nombre %></b>')
            .addTo(mapa);