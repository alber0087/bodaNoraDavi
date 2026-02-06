# Configuración de Formspree

Formspree es una alternativa más simple a EmailJS que no requiere configuración de Gmail ni permisos complejos.

## Pasos para configurar Formspree:

1. **Crear una cuenta en Formspree**
   - Ve a https://formspree.io/
   - Haz clic en "Sign Up" y crea una cuenta gratuita
   - El plan gratuito permite hasta 50 envíos/mes

2. **Crear un nuevo formulario**
   - Una vez dentro del dashboard, haz clic en "New Form"
   - Nombre el formulario (ej: "Confirmación Boda Nora y David")
   - En "Email Notifications", añade: `bodanoradavi@gmail.com`
   - Haz clic en "Create Form"

3. **Obtener el endpoint URL**
   - Después de crear el formulario, verás el "Form Endpoint"
   - Será algo como: `https://formspree.io/f/YOUR_FORM_ID`
   - Copia esta URL completa

4. **Actualizar el código**
   - Abre `src/components/EncuestaSection.vue`
   - Busca la línea: `const FORMSPREE_ENDPOINT = 'YOUR_FORMSPREE_ENDPOINT'`
   - Reemplaza `YOUR_FORMSPREE_ENDPOINT` con tu URL de Formspree
   - Ejemplo: `const FORMSPREE_ENDPOINT = 'https://formspree.io/f/xpzgkqyz'`

5. **Configurar el email de destino (opcional)**
   - En la configuración del formulario en Formspree
   - Ve a "Settings" > "Email Notifications"
   - Asegúrate de que `bodanoradavi@gmail.com` esté configurado como destinatario

## Ventajas de Formspree:

- ✅ No requiere configuración de OAuth o permisos de Gmail
- ✅ Muy fácil de configurar (solo necesitas la URL del endpoint)
- ✅ Los emails llegan directamente a tu bandeja de entrada
- ✅ Plan gratuito con 50 envíos/mes
- ✅ No requiere instalación de dependencias

## Nota:

Si necesitas más de 50 envíos/mes, Formspree tiene planes de pago, o puedes considerar otras alternativas como:
- Web3Forms (gratis, ilimitado)
- FormSubmit (gratis, ilimitado)
- Getform (gratis hasta 50 envíos/mes)
