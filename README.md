# RestAPI - Proyecto Integrador

Project de REST API para gestionar clientes, productos y ventas usando Python, PostgreSQL y Flask.

## Requisitos previos

- Python 3.8+
- PostgreSQL instalado y en funcionamiento
- pip (gestor de paquetes de Python)

## Pasos de instalación

### 1. Clonar o descargar el proyecto

```bash
cd /ruta/del/proyecto
```

### 2. Crear y activar el ambiente virtual

```bash
# Crear el ambiente virtual
python -m venv .venv

# Activar el ambiente (macOS/Linux)
source .venv/bin/activate

# Activar el ambiente (Windows)
# .venv\Scripts\activate
```

### 3. Instalar las dependencias

```bash
pip install -r requirements.txt
```

### 4. Configurar las variables de entorno

Copia el archivo `.env.example` a `.env`:

```bash
cp .env.example .env
```

Luego edita el archivo `.env` con tus credenciales de PostgreSQL:

```dotenv
DB_HOST=localhost          # Host de tu base de datos
DB_PORT=5432              # Puerto (por defecto 5432)
DB_NAME=store_db          # Nombre de la base de datos
DB_USER=postgres          # Usuario de PostgreSQL
DB_PASSWORD=tu_contraseña # Tu contraseña de PostgreSQL
```

**Importante:** Asegúrate de que:
- PostgreSQL está corriendo
- La base de datos `store_db` existe (o crea una nueva)
- Las credenciales sean correctas

### 5. Ejecutar el seed (populated la base de datos)

```bash
# Primera ejecución (crea tablas e inserta datos)
python scripts/seed_db_postgres.py

# Para reiniciar y recrear las tablas:
python scripts/seed_db_postgres.py --reset
```

Esto creará 3 tablas:
- **clients**: 5 clientes de ejemplo
- **products**: 6 productos de ejemplo
- **sales**: 12 transacciones de ejemplo

## Estructura del proyecto

```
RestAPI/
├── scripts/
│   └── seed_db_postgres.py    # Script para poblar la base de datos
├── .env.example               # Plantilla de variables de entorno
├── .env                       # Variables de entorno (no commitear a Git)
├── .venv/                     # Ambiente virtual (no commitear a Git)
├── requirements.txt           # Dependencias del proyecto
└── README.md                  # Este archivo
```

## Solución de problemas

### Error: "Missing environment variable"
- Verifica que existe el archivo `.env`
- Comprueba que todas las variables requeridas están configuradas correctamente

### Error: "could not connect to server"
- Asegúrate que PostgreSQL está corriendo (`brew services start postgresql` en macOS)
- Verifica el host y puerto en `.env`

### Error: "Seed skipped: data already exists"
- Usa `python scripts/seed_db_postgres.py --reset` para recrear desde cero

## Datos de ejemplo

Después de ejecutar el seed, tendrás:

**Clientes:**
- Ana García
- Luis Pérez
- María López
- Carlos Sánchez
- Sofía Ramírez

**Productos:**
- Teclado Mecánico ($899)
- Mouse Inalámbrico ($399)
- Termo Acero ($249)
- Playera Deportiva ($299)
- Cuaderno A4 ($79)
- Chocolate 70% ($59)

**Ventas:** 12 transacciones de ejemplo con diferentes estados (PAID, PENDING, CANCELLED)

---

**Autor:** Diplomado en Java y Python - Universidad Anáhuac Mayab  
**Fecha:** 2026
