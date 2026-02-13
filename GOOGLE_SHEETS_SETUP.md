# Configuración con Google Sheets

Esta solución guarda todas las confirmaciones en una hoja de cálculo de Google Sheets en lugar de enviar un email por cada respuesta. Así puedes ver todas las respuestas organizadas en una tabla.

## Pasos para configurar:

### 1. Crear una Google Sheet

1. Ve a https://sheets.google.com/
2. Crea una nueva hoja de cálculo
3. Nombra la primera hoja (pestaña) como "Confirmaciones"
4. En la primera fila, añade estos encabezados:
   ```
   A1: Fecha y Hora
   B1: Nombre y Apellidos
   C1: Asistencia
   D1: Alergias o Intolerancias
   E1: ¿Quiere Zapatillas?
   F1: Talla de Zapatilla
   G1: ¿Va al Alboroto?
   ```

### 2. Crear un Script de Apps Script

1. En tu Google Sheet, ve a **Extensiones** > **Apps Script**
2. Elimina el código que aparece por defecto
3. Pega este código (acepta el envío del formulario de la web; si ya tenías una versión anterior, sustitúyela por esta):

```javascript
function doPost(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Confirmaciones');
    var p = {};
    var raw = (e.postData && e.postData.contents) ? (e.postData.contents + '') : '';
    if (raw.trim().indexOf('{') === 0) {
      try { p = JSON.parse(raw); } catch (err) {}
    } else if (raw.indexOf('=') !== -1) {
      raw.split('&').forEach(function(pair) {
        var i = pair.indexOf('=');
        if (i !== -1) p[decodeURIComponent(pair.substring(0, i))] = decodeURIComponent((pair.substring(i + 1) || '').replace(/\+/g, ' '));
      });
    }
    if (Object.keys(p).length === 0 && e.parameter) p = e.parameter;
    var name = p.name || '';
    var attendance = p.attendance || '';
    var allergies = p.allergies || 'Ninguna';
    var wants_slippers = p.wants_slippers || '';
    var shoe_size = p.shoe_size || 'N/A';
    var goes_to_alboroto = p.goes_to_alboroto || '';
    var timestamp = new Date();
    sheet.appendRow([timestamp, name, attendance, allergies, wants_slippers, shoe_size, goes_to_alboroto]);
    return ContentService.createTextOutput(JSON.stringify({ success: true })).setMimeType(ContentService.MimeType.JSON);
  } catch (error) {
    return ContentService.createTextOutput(JSON.stringify({ success: false, error: error.toString() })).setMimeType(ContentService.MimeType.JSON);
  }
}
```

4. Guarda el proyecto (Ctrl+S o Cmd+S)
5. Nombra el proyecto (ej: "Boda Confirmaciones")

### 3. Desplegar como Web App

1. Haz clic en **Desplegar** > **Nueva implementación**
2. Selecciona tipo: **Aplicación web**
3. Configura:
   - **Descripción**: "API para confirmaciones de boda"
   - **Ejecutar como**: "Yo"
   - **Quién tiene acceso**: "Cualquiera" (importante para que funcione desde la web)
4. Haz clic en **Desplegar**
5. **Copia la URL de la aplicación web** (algo como: `https://script.google.com/macros/s/AKfycby.../exec`)
   - **IMPORTANTE**: Asegúrate de copiar la URL que termina en `/exec` (no `/dev`)
6. Haz clic en **Autorizar acceso** y acepta los permisos
7. Si es la primera vez, Google te pedirá autorizar el acceso. Acepta todos los permisos.

### 4. Poner la URL en la web

1. Abre `src/components/EncuestaSection.vue`
2. Busca la línea: `const GOOGLE_SCRIPT_URL = 'https://script...'`
3. Sustituye esa URL por la que copiaste en el paso 3 (la que termina en `/exec`).

No hace falta backend ni variables de entorno: el formulario envía los datos directamente a Google (el navegador hace un POST normal, sin CORS).

### 5. (Opcional) Configurar notificaciones por email

Si quieres recibir un email cuando alguien confirme (pero no uno por cada confirmación), puedes añadir esto al final de la función `doPost`:

```javascript
// Send summary email (optional - only if you want notifications)
const totalRows = sheet.getLastRow() - 1; // Subtract header row
if (totalRows % 10 === 0) { // Send email every 10 confirmations
  MailApp.sendEmail({
    to: 'bodanoradavi@gmail.com',
    subject: `Confirmaciones Boda - ${totalRows} confirmaciones recibidas`,
    body: `Ya tienes ${totalRows} confirmaciones en la hoja de cálculo.`
  });
}
```

## Ventajas de esta solución:

- ✅ Todas las respuestas en una tabla organizada
- ✅ No recibes 150 emails, solo ves todo en la hoja
- ✅ Puedes exportar a Excel, hacer análisis, etc.
- ✅ Completamente gratuito
- ✅ Fácil de compartir con otros organizadores
- ✅ Puedes ver las respuestas en tiempo real

## Ver las respuestas:

Simplemente abre tu Google Sheet y verás todas las confirmaciones organizadas en filas, con una nueva fila cada vez que alguien envía el formulario.
