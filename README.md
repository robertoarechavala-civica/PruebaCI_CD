# PruebaCI_CD
Repositorio para probar funcionalidades CI/CD en TinyBird.

## Ingerir datos desde Mockingbird

La datasource más clara para empezar en este repo es [datasources/prueba.datasource](/home/usuario/PruebaCI_CD/datasources/prueba.datasource), que espera estas columnas:

- `timestamp` `DateTime`
- `event_type` `String`
- `user_id` `String`
- `value` `Float64`

### 1. Genera los datos en Mockingbird

En `https://mockingbird.tinybird.co/` crea un dataset con estas columnas:

- `timestamp`
- `event_type`
- `user_id`
- `value`

Un ejemplo válido de filas sería como el archivo [fixtures/prueba.csv](/home/usuario/PruebaCI_CD/fixtures/prueba.csv).

### 2. Exporta el resultado

Descarga el dataset como `CSV` y guárdalo como `fixtures/prueba.csv` o con otro nombre dentro de `fixtures/`.

### 3. Construye el proyecto en Tinybird

Si usas Tinybird Local:

```bash
tb build
```

Si prefieres Tinybird Cloud, primero autentícate:

```bash
tb login
tb --cloud build
```

### 4. Ingresa los datos

Para Tinybird Local:

```bash
tb datasource append prueba --file fixtures/prueba.csv
```

Para Tinybird Cloud:

```bash
tb --cloud datasource append prueba --file fixtures/prueba.csv
```

### 5. Verifica

```bash
tb sql "SELECT * FROM prueba LIMIT 10"
```

Si consultas Cloud:

```bash
tb --cloud sql "SELECT * FROM prueba LIMIT 10"
```

## Nota sobre este entorno

En esta máquina no pude completar la ingesta real porque:

- no hay acceso de red a Tinybird Cloud
- Tinybird Local no está disponible porque Docker no está levantado

En cuanto tengas una de esas dos opciones activa, los comandos anteriores deberían funcionar con este repo.
