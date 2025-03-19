# API REST para Sensores IoT

## Descripción
Este proyecto es una API REST desarrollada para la asignatura de **Ecosistemas Móviles y Distribuidos (EMD)**. La API permite gestionar sensores IoT y sus lecturas, proporcionando funcionalidades CRUD para ambos. Está diseñada para ser utilizada en aplicaciones distribuidas que requieren la recopilación y análisis de datos de sensores.

## Características
- Gestión de sensores (crear, leer, actualizar y eliminar).
- Gestión de lecturas de sensores (crear, leer, eliminar).
- Filtrado de lecturas por rango de fechas.
- Sanitización de entradas para prevenir inyecciones en MongoDB.
- Scripts para importar y exportar datos de la base de datos.

## Tecnologías utilizadas
- **Node.js**: Entorno de ejecución.
- **Express.js**: Framework para la creación de la API REST.
- **MongoDB**: Base de datos NoSQL.
- **Mongoose**: ODM para MongoDB.
- **Moment.js**: Manejo de fechas.
- **Mongo-sanitize**: Protección contra inyecciones.

## Estructura del proyecto
```. 
├── config/             # Configuración de la base de datos
├── controllers/        # Lógica de negocio de la API
├── models/             # Modelos de datos (Mongoose)
├── resources/          # Recursos adicionales y datos de ejemplo
├── routes/             # Definición de rutas de la API
├── server.js           # Punto de entrada de la aplicación
├── package.json        # Dependencias y metadatos del proyecto
└── README.md           # Documentación del proyecto
```

## Instalación
1. Clona el repositorio:
```bash
git clone https://github.com/tu-usuario/API_EMD.git
cd API_EMD
```

2. Instala las dependencias:
```bash
npm install
```

3. Configura la base de datos:
- Edita el archivo `.env` con las credenciales de tu base de datos MongoDB:
```
MONGO_CREDENTIALS=mongodb://TU_NOMBRE:TUCONTRASEÑA@localhost:27017/sensores?authSource=admin
PORT=3000
```

4. Inicia el servidor:
```bash
node server.js
```

## Endpoints

### Sensores
| Método | URL             | Descripción                       |
|--------|-----------------|-----------------------------------|
| GET    | `/sensors`      | Obtener todos los sensores        |
| GET    | `/sensors/:id`  | Obtener un sensor por su ID       |
| POST   | `/sensors`      | Crear un nuevo sensor             |
| PUT    | `/sensors/:id`  | Actualizar un sensor existente    |
| DELETE | `/sensors/:id`  | Eliminar un sensor                |

### Lecturas
| Método | URL                          | Descripción                                |
|--------|------------------------------|--------------------------------------------|
| GET    | `/readings/:sensorId`        | Obtener todas las lecturas de un sensor    |
| GET    | `/readings/time/:sensorId`   | Obtener lecturas por rango de fechas       |
| POST   | `/readings`                  | Crear una nueva lectura                    |
| DELETE | `/readings/:sensorId`        | Eliminar todas las lecturas de un sensor   |

## Modelos de datos

### Sensor
```json
{
  "name": "string",       // Nombre del sensor
  "type": "string",       // Tipo de sensor (Temperatura, Humedad, etc.)
  "location": "string",   // Ubicación física del sensor
  "createdAt": "Date"     // Fecha de creación del registro
}
```

### Lectura
```json
{
  "sensorId": "string",   // ID del sensor asociado
  "value": "number",      // Valor de la lectura
  "unit": "string",       // Unidad de medida (°C, %RH, ppm, etc.)
  "timestamp": "Date"     // Fecha/hora de la lectura
}
```

## Scripts de utilidad

### Exportar datos
```bash
bash resources/export_data.sh
```
Este script exporta los datos de sensores y lecturas a los archivos `sensors_back.json` y `readings_back.json`.

### Importar datos
```bash
bash resources/import_data.sh
```
Este script importa datos desde los archivos `sensors.json` y `readings.json` a la base de datos.

## Seguridad
La API utiliza el paquete `mongo-sanitize` para proteger contra inyecciones en MongoDB. Además, las credenciales sensibles se almacenan en un archivo `.env` que está excluido del repositorio mediante `.gitignore`.

## Pruebas
Incluye una colección de Postman para probar los endpoints de la API:
- Archivo: `resources/API Datos.postman_collection.json`

## Licencia
Este proyecto está licenciado bajo la licencia ISC.

## Autor
Jose Aveleira