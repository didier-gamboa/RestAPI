# RestAPI - Proyecto Integrador

Proyecto de REST API para gestionar clientes, productos y ventas usando Python, FastAPI y MySQL.

## Requisitos previos

- Python 3.8+
- MySQL Server instalado y en funcionamiento (puedes usar MySQL Workbench como interfaz gráfica)
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

Luego edita el archivo `.env` con tus credenciales de MySQL:

```dotenv
DB_HOST=localhost          # Host de tu base de datos (generalmente localhost)
DB_PORT=3306              # Puerto (por defecto 3306 para MySQL)
DB_NAME=store_db          # Nombre de la base de datos
DB_USER=root              # Usuario de MySQL (por defecto root)
DB_PASSWORD=tu_contraseña # Tu contraseña de MySQL
```

**Importante:** Asegúrate de que:
- MySQL está corriendo (verifica en MySQL Workbench que el servidor local esté activo)
- La base de datos `store_db` existe o será creada automáticamente por el seed script
- Las credenciales sean correctas (usuario y contraseña que configuraste en MySQL)

### 5. Ejecutar el seed (pobla la base de datos)

```bash
# Primera ejecución (crea tablas e inserta datos)
python scripts/seed_db_mysql.py

# Para reiniciar y recrear las tablas:
python scripts/seed_db_mysql.py --reset
```

Esto creará 3 tablas:
- **clients**: 5 clientes de ejemplo
- **products**: 6 productos de ejemplo
- **sales**: 12 transacciones de ejemplo

## Estructura del proyecto

```
RestAPI/
├── scripts/
│   ├── seed_db_mysql.py       # Script para poblar la base de datos MySQL
│   └── seed_db_postgres.py    # Script para poblar la base de datos PostgreSQL (legado)
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

### Error: "[Errno 10061] No se pudo establecer conexión" o "Connection refused"
- Asegúrate que MySQL está corriendo:
  - En macOS: abre MySQL Workbench o ejecuta `brew services start mysql-community-server`
  - En Windows: verifica que el servicio MySQL está iniciado en Services
- Verifica el host y puerto en `.env` (por defecto localhost:3306)

### Error: "Access denied for user"
- Verifica que el usuario y contraseña en `.env` son correctos
- Asegúrate de que el usuario tiene permisos para crear bases de datos

### Error: "Seed skipped: data already exists"
- Usa `python scripts/seed_db_mysql.py --reset` para recrear desde cero

## Cambios de PostgreSQL a MySQL

Si anteriormente usabas PostgreSQL, ten en cuenta estos cambios:

| Aspectos | PostgreSQL | MySQL |
|----------|------------|-------|
| **Driver** | psycopg[binary] | mysql-connector-python |
| **Script seed** | seed_db_postgres.py | seed_db_mysql.py |
| **Puerto por defecto** | 5432 | 3306 |
| **Usuario por defecto** | postgres | root |

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
