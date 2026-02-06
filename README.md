# Boda Nora y Davi

Página web sencilla para la boda de Nora y Davi, desarrollada con Vue 3 y Tailwind CSS.

## Características

- ✨ Diseño moderno con colores dorado y azul
- ⏰ Cuenta atrás hasta la fecha de la boda
- 📅 Horario detallado de los eventos
- 📍 Localización con Google Maps
- 🏨 Recomendaciones de hoteles y peluquerías
- 📝 Formulario de confirmación de asistencia

## Instalación

1. Instala las dependencias:
```bash
npm install
```

2. Inicia el servidor de desarrollo:
```bash
npm run dev
```

3. Abre tu navegador en `http://localhost:5173`

## Personalización

### Cambiar la fecha de la boda

Edita el archivo `src/components/CountdownSection.vue` y modifica la línea:
```javascript
const weddingDate = new Date('2025-06-15 18:00:00').getTime()
```

### Actualizar la localización

Edita el archivo `src/components/LocalizacionSection.vue` y actualiza:
- `location.address`: La dirección completa
- `location.mapsUrl`: El enlace de Google Maps
- `location.embedUrl`: El código de embed de Google Maps

### Añadir el logo

1. Coloca tu logo en la carpeta `public/` (por ejemplo: `public/logo.png`)
2. Edita `src/App.vue` y actualiza la línea:
```javascript
const logo = ref('/logo.png') // Cambia la ruta según el nombre de tu archivo
```

### Añadir fotos al horario

1. Coloca las fotos en la carpeta `public/` (por ejemplo: `public/fijo-discontinuo.jpg`)
2. En `src/components/HorarioSection.vue`, añade la ruta de la imagen en el campo `image` de cada evento del array `schedule`:
```javascript
{
  time: '20:00',
  title: 'Concierto de Fijo Discontinuo',
  description: 'Concierto en directo de Fijo Discontinuo. ¡No os lo perdáis!',
  image: '/fijo-discontinuo.jpg' // Añade la ruta aquí
}
```

### Actualizar recomendaciones

Edita `src/components/RecomendacionesSection.vue` y modifica los arrays `hotels` y `hairdressers` con tus recomendaciones.

## Construcción para producción

```bash
npm run build
```

Los archivos se generarán en la carpeta `dist/`.

## Tecnologías

- Vue 3
- Tailwind CSS
- Vite
