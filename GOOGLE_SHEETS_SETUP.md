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
3. Pega este código:

```javascript
function doPost(e) {
  try {
    const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Confirmaciones');
    
    // Parse the data
    const data = JSON.parse(e.postData.contents);
    
    // Get current date and time
    const timestamp = new Date();
    
    // Add row to sheet
    sheet.appendRow([
      timestamp,
      data.name || '',
      data.attendance || '',
      data.allergies || 'Ninguna',
      data.wants_slippers || '',
      data.shoe_size || 'N/A',
      data.goes_to_alboroto || ''
    ]);
    
    // Return success response with CORS headers
    return ContentService
      .createTextOutput(JSON.stringify({ success: true }))
      .setMimeType(ContentService.MimeType.JSON);
      
  } catch (error) {
    // Return error response with CORS headers
    return ContentService
      .createTextOutput(JSON.stringify({ success: false, error: error.toString() }))
      .setMimeType(ContentService.MimeType.JSON);
  }
}

// Handle CORS preflight requests
function doOptions() {
  return ContentService
    .createTextOutput('')
    .setMimeType(ContentService.MimeType.JSON);
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

### 4. Actualizar el código

1. Abre `src/components/EncuestaSection.vue`
2. Busca: `const GOOGLE_SCRIPT_URL = 'YOUR_GOOGLE_SCRIPT_URL'`
3. Reemplaza `YOUR_GOOGLE_SCRIPT_URL` con la URL que copiaste en el paso 3

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
