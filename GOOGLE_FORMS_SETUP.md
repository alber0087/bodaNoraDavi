# Configuración con Google Forms

Esta solución usa un **Google Form** directamente (sin Apps Script). Las respuestas se guardan automáticamente en una hoja de cálculo de Google Sheets.

## Pasos para configurar:

### 1. Crear el Google Form

1. Ve a https://forms.google.com/
2. Crea un **nuevo formulario en blanco**
3. Añade estos campos **en este orden exacto**:

   **Campo 1: Nombre y Apellidos**
   - Tipo: Texto corto
   - Marca como obligatorio ✓

   **Campo 2: Asistencia**
   - Tipo: Opción múltiple
   - Opciones: "Sí" y "No"
   - Marca como obligatorio ✓

   **Campo 3: Alergias o intolerancias alimentarias**
   - Tipo: Párrafo (texto largo)
   - Opcional (no marcar como obligatorio)

   **Campo 4: ¿Quieres unas zapatillas al final de la noche?**
   - Tipo: Opción múltiple
   - Opciones: "Sí" y "No"
   - Opcional

   **Campo 5: Número de zapatilla**
   - Tipo: Opción múltiple
   - Opciones: 36, 37, 38, 39, 40, 41
   - Opcional

   **Campo 6: ¿Vas a ir al Alboroto cuando acabe la fiesta en la Finca?**
   - Tipo: Opción múltiple
   - Opciones: "Sí" y "No"
   - Opcional

4. En la parte superior derecha, haz clic en **⚙️ Configuración** → **Respuestas** → Activa **"Aceptar respuestas"**

### 2. Conectar con Google Sheets (opcional pero recomendado)

1. En el formulario, haz clic en la pestaña **Respuestas**
2. Haz clic en el icono de **Google Sheets** (icono verde)
3. Selecciona "Crear una nueva hoja" o "Seleccionar hoja existente"
4. Las respuestas se guardarán automáticamente en esa hoja

### 3. Obtener la URL y los nombres de los campos

**Método más fácil: usar "Obtener enlace de prellenado"**

1. En tu Google Form, haz clic en los **tres puntos** (⋮) en la esquina superior derecha
2. Selecciona **"Obtener enlace de prellenado"** (o "Get pre-filled link" en inglés)
3. Rellena el formulario con datos de prueba (cualquier cosa):
   - Campo 1 (Nombre): "Test"
   - Campo 2 (Asistencia): "Sí"
   - Campo 3 (Alergias): "Test"
   - Campo 4 (Zapatillas): "Sí"
   - Campo 5 (Talla): "38"
   - Campo 6 (Alboroto): "Sí"
4. Haz clic en **"Obtener enlace"** (o "Get link")
5. Te dará una URL larga que se ve así:
   ```
   https://docs.google.com/forms/d/e/XXXXX/viewform?entry.123456789=Test&entry.987654321=Sí&entry.111222333=Test&entry.444555666=Sí&entry.777888999=38&entry.000111222=Sí
   ```
6. **Copia esa URL completa** - ahí están todos los `entry.XXXXXXX` que necesitas
7. La URL de envío será la misma pero cambiando `/viewform` por `/formResponse`:
   ```
   https://docs.google.com/forms/d/e/XXXXX/formResponse?entry.123456789=Test&entry.987654321=Sí&...
   ```

**Extraer los nombres de los campos:**

De la URL que obtuviste, los nombres son los que aparecen después de `entry.` y antes del `=`:

- `entry.123456789` → Campo 1 (Nombre)
- `entry.987654321` → Campo 2 (Asistencia)
- `entry.111222333` → Campo 3 (Alergias)
- `entry.444555666` → Campo 4 (Zapatillas)
- `entry.777888999` → Campo 5 (Talla)
- `entry.000111222` → Campo 6 (Alboroto)

**Nota:** Los números `123456789`, `987654321`, etc. son solo ejemplos. Los tuyos serán diferentes. Cópialos exactamente como aparecen en tu URL.

### 4. Configurar el código

1. Abre `src/components/EncuestaSection.vue`
2. Busca la sección donde dice `GOOGLE_FORM_URL` y `GOOGLE_FORM_FIELDS`
3. Sustituye:
   - `GOOGLE_FORM_URL` por la URL que obtuviste (la que termina en `/formResponse`)
   - `GOOGLE_FORM_FIELDS` por un objeto con los nombres de los campos en este formato:

```javascript
const GOOGLE_FORM_FIELDS = {
  name: 'entry.123456789',        // Campo 1: Nombre
  attendance: 'entry.987654321',   // Campo 2: Asistencia
  allergies: 'entry.111222333',   // Campo 3: Alergias
  wants_slippers: 'entry.444555666', // Campo 4: Zapatillas
  shoe_size: 'entry.777888999',   // Campo 5: Talla
  goes_to_alboroto: 'entry.000111222' // Campo 6: Alboroto
}
```

## Ventajas de esta solución:

- ✅ **Sin código de Apps Script** - solo Google Forms
- ✅ Las respuestas se guardan automáticamente en Sheets
- ✅ Completamente gratuito
- ✅ No hay problemas de CORS ni JSON parsing
- ✅ Fácil de compartir y ver respuestas

## Vincular la hoja de cálculo a otra cuenta

Para que otra persona (otra cuenta de Google) pueda ver o editar las respuestas:

### Compartir la hoja de cálculo (Google Sheets)

1. Abre la **hoja de cálculo** donde se guardan las respuestas (desde el formulario: pestaña **Respuestas** → icono de **Google Sheets**).
2. Haz clic en **Compartir** (arriba a la derecha).
3. Añade el **correo** de la otra cuenta.
4. Elige el nivel de acceso:
   - **Lector**: solo puede ver las respuestas.
   - **Comentar**: puede ver y añadir comentarios.
   - **Editor**: puede ver y modificar la hoja (añadir columnas, borrar filas, etc.).
5. Opcional: desmarca **"Notificar a las personas"** si no quieres enviar un email.
6. Haz clic en **Enviar** (o **Compartir**).

La otra cuenta verá la hoja en su Google Drive (en "Compartidos conmigo") y las respuestas nuevas seguirán apareciendo ahí.

### Compartir también el formulario (opcional)

Si quieres que la otra cuenta pueda editar el formulario o ver la configuración:

1. Abre el **Google Form**.
2. Haz clic en **Compartir** (arriba a la derecha).
3. Añade el correo y elige **Editor** o **Lector** según lo que necesites.

**Nota:** El formulario debe seguir perteneciendo a la cuenta que lo creó para que la web siga enviando a la misma URL. Solo compartes la hoja (y opcionalmente el formulario) para que la otra persona pueda ver o gestionar los datos.
