# Confirmación RSVP con Supabase

Las confirmaciones se guardan en una base de datos en Supabase (gratis). Puedes ver los datos como tabla y **exportar a CSV** para abrirlo en Excel.

---

## Paso 1: Crear cuenta en Supabase (2 minutos)

1. Ve a [supabase.com](https://supabase.com) y crea una cuenta (puedes usar tu cuenta de Google/GitHub)
2. Haz clic en **"New Project"**
3. Configura:
   - **Name**: `boda-confirmaciones` (o lo que quieras)
   - **Database Password**: pon una contraseña cualquiera y guárdala
   - **Region**: elige la más cercana (ej: East US)
4. Haz clic en **Create new project** y espera ~1 minuto

---

## Paso 2: Crear la tabla (1 minuto)

1. En tu proyecto de Supabase, ve a **SQL Editor** (menú izquierdo)
2. Haz clic en **"New query"**
3. Pega esto y haz clic en **Run**:

```sql
CREATE TABLE confirmaciones (
  id BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  nombre TEXT NOT NULL,
  num_invitados INTEGER NOT NULL DEFAULT 1,
  asistencia BOOLEAN NOT NULL DEFAULT true,
  mensaje TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Permisos: cualquiera puede insertar y leer (lectura protegida por contraseña en la web)
ALTER TABLE confirmaciones ENABLE ROW LEVEL SECURITY;

CREATE POLICY "Permitir inserciones públicas"
  ON confirmaciones FOR INSERT TO anon
  WITH CHECK (true);

CREATE POLICY "Permitir lectura pública"
  ON confirmaciones FOR SELECT TO anon
  USING (true);
```

Deberías ver un mensaje verde de éxito.

---

## Paso 3: Obtener las credenciales (30 segundos)

1. Ve a **Project Settings** (ícono de engranaje abajo a la izquierda)
2. Haz clic en **API** (en la sección Data API, bajo Configuration)
3. Copia estos dos valores:
   - **Project URL** → algo como `https://abcdefgh.supabase.co`
   - **anon public key** → una cadena larga que empieza con `eyJ...`

---

## Paso 4: Configurar en el proyecto (30 segundos)

Abre `src/components/RsvpForm.vue` y reemplaza las dos líneas de configuración:

```javascript
const SUPABASE_URL = 'https://abcdefgh.supabase.co'         // Tu Project URL
const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIs...'         // Tu anon public key
```

---

## Paso 5: Probar

1. Ejecuta `npm run dev`
2. Ve a la sección de confirmación y llena el formulario
3. En Supabase, ve a **Table Editor** → tabla `confirmaciones` → ahí verás los datos

---

## Exportar a CSV (para Excel)

### Opción 1: Desde la página web (recomendado)

1. Abre tu invitación y agrega `?admin` a la URL:
   ```
   https://tu-sitio.com/?admin
   ```
2. Ingresa la contraseña (por defecto: `boda2026`)
3. Verás una tabla con todas las confirmaciones y estadísticas
4. Haz clic en **"Descargar CSV"** para abrir en Excel

> Para cambiar la contraseña, edita `src/components/AdminPanel.vue` línea donde dice:
> `const ADMIN_PASSWORD = 'boda2026'`

### Opción 2: Desde Supabase

1. En Supabase, ve a **Table Editor** → `confirmaciones`
2. Haz clic en **Export** → **Export to CSV**

---

## Resumen de datos que se guardan

| Columna | Ejemplo |
|---------|---------|
| nombre | Familia García López |
| num_invitados | 4 |
| asistencia | true / false |
| mensaje | ¡Felicidades! |
| created_at | 2026-03-15 14:30:00 |

---

## ¿Es seguro?

La `anon key` es pública por diseño — permite insertar y leer filas. Nadie puede modificar ni borrar datos. El panel de administración está protegido con contraseña, así que solo tú puedes ver las confirmaciones desde la web.
