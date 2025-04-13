# API Endpoints Documentation

Este documento describe todos los endpoints y herramientas disponibles en el proyecto langchain-mcp-context.

## Herramientas de Memoria Compartida

### 1. readFileInProject
- **Descripción**: Lee el contenido de un archivo de un proyecto en Memoria Compartida
- **Parámetros**:
  - `project` (string): Proyecto del cual leer el archivo
  - `filePath` (string): Ruta al archivo a leer
- **Respuesta**: Contenido del archivo o mensaje de error

### 2. listProjectFiles
- **Descripción**: Lista los archivos en un proyecto de memoria compartida
- **Parámetros**:
  - `project` (string): Proyecto del cual listar los archivos (opcional)
- **Respuesta**: Árbol de archivos en formato JSON o mensaje de error

### 3. deleteFileInProject
- **Descripción**: Elimina un archivo de un proyecto en memoria compartida
- **Parámetros**:
  - `project` (string): Proyecto del cual eliminar el archivo
  - `filePath` (string): Ruta al archivo a eliminar
- **Respuesta**: Confirmación de eliminación o mensaje de error

### 4. createProject
- **Descripción**: Crea un nuevo proyecto en memoria compartida
- **Parámetros**:
  - `name` (string): Nombre del proyecto
  - `description` (string): Descripción del proyecto
- **Respuesta**: Confirmación de creación o mensaje de error

### 5. createFileInProject
- **Descripción**: Crea un nuevo archivo en un proyecto en memoria compartida
- **Parámetros**:
  - `project` (string): Proyecto en el cual crear el archivo
  - `filePath` (string): Ruta donde crear el archivo
  - `content` (string): Contenido a escribir en el archivo
- **Respuesta**: Confirmación de creación o mensaje de error

## Recursos de Reglas de Cursor

### 1. Cursor Rules Resource
- **Descripción**: Proporciona acceso a las reglas de Cursor de repositorios GitHub
- **URI Base**: `github-cursor-rules://all`
- **Formato de URI para reglas específicas**: `github-cursor-rules://rule/{repo_name}/{path}`
- **Respuesta**: Lista de reglas de Cursor con sus contenidos

## Configuración por Defecto

El sistema está configurado para usar un repositorio por defecto con las siguientes características:
- **Nombre**: shared-memory
- **Propietario**: S4M3R
- **Rama por defecto**: main

## Integración con GitHub

El sistema utiliza la integración con GitHub para:
- Gestionar archivos y proyectos
- Extraer reglas de Cursor
- Mantener la persistencia de datos

## Manejo de Errores

Todas las herramientas incluyen manejo de errores robusto que:
- Captura y reporta errores específicos
- Proporciona mensajes de error descriptivos
- Mantiene la consistencia del sistema en caso de fallos

## Notas de Uso

- Todas las rutas de archivo deben ser relativas al proyecto especificado
- Los nombres de proyecto deben ser únicos
- Se recomienda usar nombres de archivo descriptivos y seguir las convenciones de nomenclatura estándar