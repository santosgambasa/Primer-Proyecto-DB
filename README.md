# CRUD de Libros en Consola (MongoDB + TypeScript)

CLI pequeña desarrollada en TypeScript para gestionar un catálogo de libros usando MongoDB y Mongoose. 

> **Contexto:** Proyecto de práctica donde reutilicé y adapté la estructura de un CRUD de productos anterior para trabajar con una entidad distinta (libros).

---

## Funcionalidades principales

Operaciones básicas que maneja la consola:

- **Creación** de registros.
- **Lectura** de la lista completa o filtrada por `_id`.
- **Edición** parcial o total de los datos de un libro.
- **Baja** de registros.

---

## Tecnologias

- **TypeScript** + **Node.js**
- **MongoDB** con **Mongoose** como ODM
- **dotenv** para la gestión de variables de entorno

---

## Modelo de datos

El proyecto apunta a la base de datos `biblioteca` dentro de la colección `libros`.

### Documento de ejemplo

```json
{
  "_id": "68dd1234567890abcdef1234",
  "titulo": "El Principito",
  "autor": "Antoine de Saint-Exupéry",
  "precio": 15000,
  "stock": 10
}
```

---

## Requisitos previos e instalación

Para replicar este proyecto o configurarlo desde cero en tu entorno local, podés seguir estos pasos de instalación y configuración de dependencias.

### 1. Instalación de dependencias

El proyecto utiliza **Mongoose** y **dotenv** como dependencias de producción, y **TypeScript** con los tipos de Node.js en desarrollo:

```bash
# Instalar dependencias del proyecto
npm install mongoose dotenv

# Instalar dependencias de desarrollo
npm install -D typescript @types/node

### 2. Configurar el entorno
Crea un archivo `.env` en la raíz (puedes tomar de base `.env.example`) y define tu string de conexión:

```env
URI_DB=mongodb://127.0.0.1:27017/biblioteca
```

## Configuración del Proyecto

### `package.json`

El proyecto utiliza **ES Modules (`"type": "module"`)** y define los scripts de compilación y ejecución:

```json
{
  "name": "TP Base de Datos",
  "version": "1.0.0",
  "description": "Una evaluacion de Base de Datos N1",
  "main": "./dist/index.js",
  "type": "module",
  "scripts": {
    "dev": "node ./src/index.ts",
    "build": "tsc",
    "start": "node ./dist/index.js"
  },
  "devDependencies": {
    "@types/node": "^26.6.2",
    "typescript": "^7.0.2"
  },
  "dependencies": {
    "dotenv": "^18.0.5",
    "mongoose": "^9.10.2"
  }
}
```

### `tsconfig.json`

Configuración de TypeScript adaptada a `nodenext` y `esnext`:

```json
{
  "compilerOptions": {
    "rootDir": "./src",
    "outDir": "./dist",
    "module": "nodenext",
    "target": "esnext",
    "types": [
      "node"
    ],
    "sourceMap": true,
    "declaration": true,
    "declarationMap": true,
    "noUncheckedIndexedAccess": true,
    "exactOptionalPropertyTypes": true,
    "strict": true,
    "jsx": "react-jsx",
    "verbatimModuleSyntax": true,
    "isolatedModules": true,
    "noUncheckedSideEffectImports": true,
    "moduleDetection": "force",
    "skipLibCheck": true
  }
}
```

---

## Ejemplos de uso

Los comandos corren mediante `npm run dev`:

### Agregar un libro
```bash
npm run dev -- create titulo="El Principito" autor="Antoine de Saint-Exupéry" precio=15000 stock=10
```

### Listar libros
```bash
# Ver todo el catálogo
npm run dev -- show

# Buscar uno en particular por su ID
npm run dev -- show 68dd1234567890abcdef1234
```

### Editar un libro
Pasa el ID seguido de las propiedades que quieras actualizar:

```bash
# Actualizar stock y precio
npm run dev -- update 68dd1234567890abcdef1234 precio=18000 stock=15

# Modificar texto
npm run dev -- update 68dd1234567890abcdef1234 titulo="El Principito" autor="Antoine de Saint-Exupéry"
```

### Borrar un libro
```bash
npm run dev -- delete 68dd1234567890abcdef1234
```

---

## Apuntes del desarrollo

La idea del trabajo fue afianzar la integración entre Node/TypeScript y MongoDB sin depender de un framework web como Express, resolviendo la interacción directamente desde la terminal.

Puntos clave que me sirvieron para practicar:
- Parseo de argumentos por consola usando `process.argv`.
- Modelado de esquemas y tipos estáticos con Mongoose y TypeScript.
- Búsquedas y validaciones trabajando con `ObjectId` nativos de Mongo.