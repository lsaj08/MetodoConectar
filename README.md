# Método CONECTAR · Brújula Interna

Landing page de Método CONECTAR, un acompañamiento de tres meses que integra psicología y nutrición para construir una relación más flexible y consciente con la comida y el cuerpo, sin dietas ni metas de peso.

Esta versión inicial conserva el HTML creado en la conversación «Ajustar HTML del correo». Presenta el programa, sus cinco etapas (Comprender, Reconectar, Nutrir, Regular y Sostener), el video de presentación y un calendario para coordinar una llamada. No incluye contador de tiempo.

**Sitio:** [lsaj08.github.io/MetodoConectar](https://lsaj08.github.io/MetodoConectar/)

## Estructura del proyecto

```text
MetodoConectar/
├── .github/workflows/ # Despliegue automático en Azure Static Web Apps
├── index.html   # Landing completa, con los estilos CSS integrados
├── .nojekyll    # Publicación directa como sitio estático en GitHub Pages
└── README.md    # Documentación del proyecto
```

## Tecnologías

- HTML5 y CSS3: diseño adaptable mediante Grid, Flexbox y consultas de medios.
- Google Fonts para las tipografías.
- Iframes para el video de YouTube y el calendario de reservas.
- GitHub Pages y Azure Static Web Apps para alojamiento estático por HTTPS.

No requiere instalación de paquetes, compilación, framework ni backend. Un script JavaScript pequeño controla el carrusel de testimonios, sin dependencias ni reproducción automática. Sin JavaScript, los siete testimonios se muestran completos en una lista. Los servicios incrustados pueden ejecutar sus propios scripts. El sitio no almacena datos ni contiene un formulario propio: las reservas se gestionan en el calendario externo.

## Identidad visual

La landing utiliza la identidad de **Brújula Interna**:

| Elemento | Uso |
| --- | --- |
| Verde profundo `#10605a` | Color principal, titulares y secciones destacadas |
| Beige cálido `#f4f1ec` | Fondo general |
| Dorado `#b8965a` | Botones, acentos y detalles |
| Cormorant Garamond | Titulares y textos destacados |
| Montserrat | Texto general y botones |

El diseño mantiene espacios amplios, contenedores redondeados y detalles inspirados en una brújula. El [logo de la marca](https://assets.cdn.filesafe.space/iIOBApGso2UQVofpQ6C5/media/6a3c25c7bc1f62f4dd009c7e.ico) se carga desde la URL facilitada para el proyecto.

Para mejorar la lectura, el texto de los botones dorados utiliza `#202a28` (contraste aproximado de 5,30:1). Los textos dorados sobre beige usan el tono más oscuro `#82632f`, y sobre verde se usa `#e8d6b6`. El dorado original se conserva en fondos y detalles.

## Accesibilidad y carga

- Enlace «Saltar al contenido», foco visible y encabezados de sección para facilitar la navegación con teclado y lectores de pantalla.
- Respeto de la preferencia de movimiento reducido y áreas táctiles más amplias en los enlaces sociales.
- Video y calendario con carga diferida; enlace alternativo a la agenda antes del iframe.
- Solo se solicitan los pesos tipográficos utilizados, con `display=swap` y fuentes de respaldo.
- Dimensiones explícitas de los logos, icono de pestaña y metadatos básicos para compartir el sitio.

La revisión visual cubrió anchos de 320, 390, 768 y 1280 píxeles, sin desbordamiento horizontal del documento. Se comprobaron el salto por teclado y los destinos de los enlaces internos. Esto no sustituye una auditoría completa de accesibilidad ni una medición de rendimiento en dispositivos reales; el contenido interno de los iframes depende de sus proveedores.

## Visualizar localmente

1. Cloná el repositorio y entrá a su carpeta:

   ```sh
   git clone https://github.com/lsaj08/MetodoConectar.git
   cd MetodoConectar
   ```

2. Abrí `index.html` con un navegador, haciendo doble clic sobre el archivo.

Para probarlo mediante un servidor local, si tenés Python instalado:

```sh
python -m http.server 8000 --bind 127.0.0.1
```

Abrí [http://127.0.0.1:8000](http://127.0.0.1:8000). Detené el servidor con `Ctrl+C`.

La estructura y los estilos funcionan localmente; las fuentes, el logo, el video y el calendario requieren conexión a Internet. Si Google Fonts no está disponible, se utilizan las fuentes de respaldo del navegador.

## Enlaces integrados

- **Video:** [presentación de Método CONECTAR en YouTube](https://youtu.be/77v3BOO4n18). El iframe utiliza `https://www.youtube.com/embed/77v3BOO4n18` y `referrerpolicy="strict-origin-when-cross-origin"`.
- **Calendario:** [agendar una llamada](https://api.psicoceo.com/widget/booking/93S1bBetM0nQT8rnrUni).
- **Instagram:** [@brujulainternacr](https://www.instagram.com/brujulainternacr/).
- **Facebook:** [Psicología de la Nutrición](https://www.facebook.com/people/Psicolog%C3%ADa-de-la-Nutrici%C3%B3n/100057042829626/).
- **TikTok:** [@psiconutricioncr](https://www.tiktok.com/@psiconutricioncr).
- **WhatsApp:** [+506 6027 0270](https://api.whatsapp.com/send/?phone=50660270270), con un mensaje de interés en Método CONECTAR precargado en la landing.

El video y la agenda incluyen enlaces alternativos para abrirlos en otra pestaña. La reproducción pública depende de la visibilidad del video y del permiso de inserción en YouTube; la disponibilidad de horarios depende del calendario. Publicar el HTML no cambia esas configuraciones ni crea reservas.

El video debe estar público o no listado y permitir la inserción en otros sitios. Si YouTube muestra el error 153, comprobar que el navegador envía la referencia del sitio de origen; no usar `no-referrer` en el iframe. Probar desde la URL HTTPS del sitio y conservar el enlace alternativo para navegadores que bloqueen el reproductor.

## Despliegue

### Azure Static Web Apps

El flujo `.github/workflows/azure-static-web-apps-black-desert-0878dd410.yml` publica los cambios de `main` en Azure y gestiona los entornos de vista previa de pull requests. Utiliza el secreto de GitHub Actions `AZURE_STATIC_WEB_APPS_API_TOKEN_BLACK_DESERT_0878DD410`, configurado por la integración de Azure; su valor no debe guardarse en los archivos del repositorio.

La landing ya está lista para publicar, por lo que el flujo usa `app_location: "/"`, `output_location: ""`, `api_location: ""` y `skip_app_build: true`. No ejecuta `npm install` ni necesita un `package.json` o un comando `build`.

El flujo inicial fallaba porque instalaba un cliente OIDC en la raíz y Oryx detectaba una aplicación Node sin comando de compilación. Ahora obtiene la identidad de GitHub mediante `core.getIDToken()` integrado en `actions/github-script`, sin instalar paquetes en el sitio, y mantiene `github_id_token` junto con el secreto de despliegue para conservar la autenticación configurada originalmente por Azure. El mismo secreto de despliegue se utiliza al cerrar los entornos de vista previa.

### GitHub Pages

El sitio se publica con **GitHub Pages desde la rama `main`, carpeta raíz `/`**. No necesita un flujo personalizado ni credenciales en los archivos del proyecto. `.nojekyll` evita el procesamiento con Jekyll.

La configuración se encuentra en **Settings → Pages → Build and deployment → Deploy from a branch → main → /(root)**. Cada push a `main` actualiza la publicación; puede tardar unos minutos. El estado se puede consultar en Pages y en la ejecución automática de despliegue de GitHub Actions.

URL pública: [https://lsaj08.github.io/MetodoConectar/](https://lsaj08.github.io/MetodoConectar/).

Para futuras actualizaciones, editá `index.html`, comprobá el resultado localmente y subí los cambios a `main`. Conservá las rutas relativas si agregás recursos locales para que funcionen bajo `/MetodoConectar/`. Esta versión no configura un dominio propio.

## Comprobaciones antes de publicar cambios

- Abrir la landing y revisar su presentación en escritorio y en una ventana angosta.
- Comprobar que los botones llevan a las secciones de video y agenda.
- Revisar que el logo y las fuentes cargan, y que el video y el calendario se muestran o permiten abrir sus enlaces alternativos.
- Revisar `git diff --check` y verificar el sitio público después del despliegue.

Las integraciones externas pueden verse afectadas por permisos, bloqueadores del navegador o interrupciones de sus proveedores. La landing no necesita claves; el despliegue en Azure utiliza el secreto de GitHub Actions descrito arriba.

## Testimonios

La sección anterior a la agenda contiene los siete comentarios facilitados por Brújula Interna, conservados íntegramente y sin nombres de pacientes. Se identifican como experiencias de talleres. Cada tarjeta incluye cinco estrellas decorativas siguiendo la referencia visual; no se publica una puntuación agregada ni datos estructurados de valoraciones.

El carrusel se maneja con botones anterior/siguiente o flechas del teclado cuando el foco está en los controles. No avanza automáticamente y el texto largo no se recorta. Para editar testimonios, modificar los elementos `figure.testimonial` en `index.html`; el contador se ajusta al número de tarjetas.
