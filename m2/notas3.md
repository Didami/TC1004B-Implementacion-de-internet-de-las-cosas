# Módulo Software

---

## Creación de BD:

### Crear base de datos:

```sql
create database testTec;
```

### Crear tabla:

- Crear tabla `employees`

```sql
CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(40) UNIQUE,
    hire_date DATE,
    salary DECIMAL(8, 2),
    department_id INT
);
```

- Crear tabla `departments`

```sql
CREATE TABLE departments (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

- Crear tabla `employees` con clave foránea

```sql
CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(40) UNIQUE,
    hire_date DATE,
    salary DECIMAL(8, 2),
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES departments(id)
);
```

- Crear tabla `events`

```sql
CREATE TABLE events (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    event_date DATE, -- yyyy-mm-dd
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP -- yyyy-mm-dd HH:MM:SS
);
```

- Crear tabla `orders`

```sql
CREATE TABLE orders (
    id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT NOT NULL,
    name VARCHAR(100) NOT NULL
);
```

- Crear tabla `customers`

```sql
CREATE TABLE customers (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

### e.g. Insertar una fila:

```sql
INSERT INTO events (name, event_date)
VALUE ('Conferencia LOREAL', "2026-10-12");
```

### Obtener información de la tabla:

- Describir tabla:

```sql
DESC events;
```

- Mostrar cómo fue creada la tabla:

```sql
SHOW CREATE TABLE events;
```

### Actualizar tabla:

#### Agregar columna:

```sql
ALTER TABLE employees ADD COLUMN birthdate DATE;
```

#### Eliminar columna:

```sql
ALTER TABLE employees DROP COLUMN birthdate DATE;
```

#### Cambiar nombre a columna:

```sql
ALTER TABLE employees CHANGE COLUMN birthdate dob DATE;
```

#### Modificar columna:

```sql
ALTER TABLE employees MODIFY COLUMN salary DECIMAL(10, 2) NOT NULL;
```

#### Cambiar nombre a columna:

```sql
ALTER TABLE employees CHANGE COLUMN birthdate dob DATE;
```

#### Cambiar nombre a tabla:

```sql
ALTER TABLE employees RENAME TO staff;
```

#### Agregar clave primaria:

```sql
ALTER TABLE employees ADD PRIMARY KEY (id);
```

#### Agregar clave foránea:

```sql
ALTER TABLE orders
ADD CONSTRAINT fk_customer
FOREIGN KEY (customer_id) REFERENCES customers(id);
```

#### Eliminar clave foránea:

```sql
ALTER TABLE orders
DROP FOREIGN KEY fk_customer;
```

## Respaldo:

```sql
/Applications/XAMPP/xamppfiles/bin/mysqldump -u root -p testTec > /Users/didami/Desktop/respaldoTec.sql
```
