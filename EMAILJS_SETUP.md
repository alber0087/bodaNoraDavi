# Configuración de EmailJS

Para que el formulario de confirmación envíe emails a `bodanoradavi@gmail.com`, necesitas configurar EmailJS.

## Pasos para configurar EmailJS:

1. **Crear una cuenta en EmailJS**
   - Ve a https://www.emailjs.com/
   - Crea una cuenta gratuita (permite hasta 200 emails/mes)

2. **Crear un Email Service**
   - En el dashboard, ve a "Email Services"
   - Haz clic en "Add New Service"
   - Selecciona "Gmail" como proveedor
   - Conecta tu cuenta de Gmail (bodanoradavi@gmail.com)
   - Copia el **Service ID** que se genera

3. **Crear un Email Template**
   - Ve a "Email Templates"
   - Haz clic en "Create New Template"
   - Usa este template como base:
   
   ```
   Subject: Confirmación de Asistencia - Boda Nora y David
   
   Nombre: {{name}}
   Asistencia: {{attendance}}
   Alergias o intolerancias: {{allergies}}
   ¿Quiere zapatillas?: {{wants_slippers}}
   Talla de zapatilla: {{shoe_size}}
   ¿Va al Alboroto?: {{goes_to_alboroto}}
   
   Mensaje completo:
   {{message}}
   ```
   
   - Guarda el template y copia el **Template ID**

4. **Obtener tu Public Key**
   - Ve a "Account" > "General"
   - Copia tu **Public Key** (User ID)

5. **Actualizar el código**
   - Abre `src/components/EncuestaSection.vue`
   - Reemplaza estos valores:
     - `YOUR_SERVICE_ID` → Tu Service ID
     - `YOUR_TEMPLATE_ID` → Tu Template ID
     - `YOUR_PUBLIC_KEY` → Tu Public Key

## Alternativa: Usar mailto (más simple pero menos elegante)

Si prefieres no usar EmailJS, puedes cambiar el formulario para usar un enlace `mailto:` que abrirá el cliente de correo del usuario. Sin embargo, esto requiere que el usuario tenga configurado un cliente de correo.
