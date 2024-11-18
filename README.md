<h1 align="center" id="title">Plantilla de Documentación del Proyecto - Mock Faker</h1>
<div align="center" id="top"> 
  <img src="./test/logo.png" alt="logo" />
</div>
<p align="center">
  <a href="#descripcion">Descripción</a> &#xa0; | &#xa0; 
  <a href="#tecnologias">Tecnologias</a> &#xa0; | &#xa0;
  <a href="#env">env</a> &#xa0; | &#xa0;
  <a href="#instalacion">Instalacion</a> &#xa0; | &#xa0;
  <a href="#rutas">Rutas</a> &#xa0; | &#xa0;
  <a href="#codigo">Código</a> &#xa0; | &#xa0;
  <a href="#dependencias">Dependencias</a> &#xa0; | &#xa0;
  <a href="#test">Test</a> &#xa0; | &#xa0; 
</p>

<br>


## Descripcion ##

Este proyecto es una API desarrollada con Node.js y Express.js que utiliza @faker-js/faker para generar datos simulados. El objetivo principal es proporcionar rutas para simular grandes volúmenes de datos de usuarios y mascotas, útiles para pruebas y desarrollo.

<a href="#title">Volver al inicio</a>


## Tecnologias ##
- **Node.js**: Plataforma para la ejecución de JavaScript del lado del servidor.
- **Express.js**: Framework para la creación de aplicaciones web y API REST.
- **MongoDB**: Base de datos NoSQL para la persistencia de la información.
- **Mongoose**: ODM (Object Data Modeling) para la conexión y manipulación de MongoDB.
- **Nodemailer**: Librería para el envío de correos electrónicos.
- **JWT (JSON Web Tokens)**: Para la autenticación y autorización.
- **dotenv**: Manejo de variables de entorno.

<a href="#title">Volver al inicio</a>


## .env ##
- MONGODB_URI=mongodb+srv://cri2024:cri2024@cluster0.mswsapd.mongodb.net/bkd3_mocks?retryWrites=true&w=majority&appName=Cluster0
- PORT=8080
- MOCK_USER_PASSWORD=coder123
#
**⚠️ Nota: información confidencial:** El archivo `.env` ha sido proporcionado únicamente para facilitar la evaluación de este proyecto por parte del profesor.

<a href="#title">Volver al inicio</a>

## Instalacion ##

```bash
# Clonar repositorio:
$ git clone https://github.com/codercriosogut/backend3-preentrega1osorio.git

# Accede al directorio del proyecto:
$ cd .\backend3-preentrega1osorio\

# Instala las dependencias:
$ npm install
$ npm list

├── @faker-js/faker@9.2.0
├── bcrypt@5.1.0
├── chai@4.3.7
├── cookie-parser@1.4.6
├── dotenv@16.4.5
├── express@4.18.2
├── jsonwebtoken@8.5.1
├── mocha@10.1.0
├── mongoose@6.7.5
├── multer@1.4.5-lts.1
└── supertest@6.3.3

# Ejecuta el servidor
$ npm start

# Utilizar Postman
```
<a href="#title">Volver al inicio</a>


## Codigo ##
#### Generación de Datos Simulados: El proyecto utiliza @faker-js/faker para crear datos de prueba:
- `GET /api/mocks/mockingpets`
- ***Genera mascotas con propiedades como***: name, specie, birthDate, adopted, owner, e image.

```json
import { faker } from '@faker-js/faker';

export const generateMockPets = (numPets) => {
    let pets = [];
    for (let i = 0; i < numPets; i++) {
        pets.push({
            name: faker.person.firstName(),
            specie: faker.animal.type(),
            birthDate: faker.date.past(5),
            adopted: false,
            owner: null,
            image: faker.image.url()
        });
    }
    return pets;
};
```
#
- `GET /api/mocks/mockingpets`
- ***Genera usuarios con propiedades como***: first_name, last_name, email, password, role, y pets.
```json
import { faker } from '@faker-js/faker';
import { createHash } from './index.js';

export const generateMockUsers = async (numUsers) => {
    const users = [];
    for (let i = 0; i < numUsers; i++) {
        users.push({
            first_name: faker.person.firstName(),
            last_name: faker.person.lastName(),
            email: faker.internet.email(),
            password: await createHash('coder123'),
            role: Math.random() < 0.5 ? 'user' : 'admin',
            pets: []
        });
    }
    return users;
};

```
#

## Rutas ## 
### POSTMAN

#### La API proporciona varias rutas para manejar la generación de datos:


### mascotas 
- `GET /api/mocks/mockingpets`: Devuelve una lista de mascotas simuladas.
- ***Query Params:***: num (opcional), el número de mascotas a generar.
#
- `GET /api/mocks/mockingusers`: Devuelve una lista de usuarios simulados.
- ***Query Params:***: num (opcional), el número de usuarios a generar.
#
- `POST /api/mocks/generateData`: Inserta datos simulados de usuarios y mascotas en la base de datos.
- ***Body Params:***: {"users": 5,"pets": 5}
#
<a href="#title">Volver al inicio</a>

## Directorios ##
```markdown
📦src
 ┣ 📂controllers
 ┣ 📂dao
 ┣ 📂repository
 ┣ 📂routes
 ┃ ┣ 📜mocks.router.js
 ┣ 📂services
 ┣ 📂utils
 ┃ ┣ 📜mockPets.js
 ┃ ┣ 📜mockUsers.js
 ┃ ┗ 📜index.js
 ┗ 📜app.js

```
#
## Dependencias ##
El proyecto utiliza las siguientes dependencias clave:

- **@faker-js/faker**: Generación de datos falsos.
- **bcrypt**: Hasheo de contraseñas.
- **dotenv**: Manejo de variables de entorno.
- **express**: Framework web.
- **mongoose**: Modelado de objetos MongoDB.
#
<a href="#title">Volver al inicio</a>

##
#
#
## Test ##
### Generar Mascotas Simuladas
- **Método**: GET
- **URL**: `http://localhost:8080/api/mocks/mockingpets?num=5`
- **Query Params**: num 5

#### Respuesta:
```json
{
    "status": "success",
    "payload": [
        {
            "name": "Janick",
            "specie": "cow",
            "birthDate": "2024-07-18T07:50:38.825Z",
            "adopted": false,
            "owner": null,
            "image": "https://picsum.photos/seed/6EhZx/3521/2314"
        },
        {
            "name": "Nadia",
            "specie": "koala",
            "birthDate": "2024-03-30T10:48:45.527Z",
            "adopted": false,
            "owner": null,
            "image": "https://loremflickr.com/855/2821?lock=7163701206650140"
        },
        {
            "name": "Lauryn",
            "specie": "polar bear",
            "birthDate": "2024-09-03T05:46:20.163Z",
            "adopted": false,
            "owner": null,
            "image": "https://loremflickr.com/3743/1853?lock=512772578769504"
        },
        {
            "name": "Pauline",
            "specie": "gorilla",
            "birthDate": "2024-10-19T07:09:32.781Z",
            "adopted": false,
            "owner": null,
            "image": "https://picsum.photos/seed/kWzXQ/108/2909"
        },
        {
            "name": "Vincent",
            "specie": "eagle",
            "birthDate": "2024-01-02T21:32:53.171Z",
            "adopted": false,
            "owner": null,
            "image": "https://picsum.photos/seed/FnfUuFOP/3741/2619"
        }
    ]
}
```
#
### Insertar Datos Simulados en la Base de Datos Mongodb
##
- **Método**: POST
- **URL**: `http://localhost:8080/api/mocks/generateData`
- **Body**: raw/JSON
#### Enviar:
```json
{
    "users": 5,
    "pets": 5 
}
```
#### Respuesta:
```json
{
    "status": "success",
    "message": "5 users and 5 pets inserted into the database"
}
```
#### MongodbAtlas:
<div align="center" id="top">
    <img src="./src/public/img/Screenshot_1.png" alt="businesses" />
</div>

#
#### Decrypt Checker Bcrypt generator:
<div align="center" id="top">
    <img src="./src/public/img/Screenshot_2.png" alt="businesses" />
</div>
<div align="center" id="top">
    <img src="./src/public/img/Screenshot_3.png" alt="businesses" />
</div>



##
<a href="#title">Volver al inicio</a>
##