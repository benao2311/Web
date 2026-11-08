# Clip Propio — código para tu repositorio

Exportación de la interfaz publicada, versión 923e2538f8922cd2234fce437e9647f01d3ae00f.

## Subir al repositorio
1. Descomprime este ZIP.
2. Abre la carpeta ClipPropio_Web.
3. Sube el CONTENIDO de esa carpeta a la raíz del repositorio; package.json debe quedar en la raíz.
4. Incluye los archivos y carpetas que empiezan por punto (por ejemplo .gitignore y .openai).
5. No subas node_modules, archivos .env, claves ni carpetas de videos procesados.

Si usas Git en una terminal desde la carpeta descomprimida:

    git init
    git add .
    git commit -m "Interfaz y procesador de Clip Propio"
    git branch -M main
    git remote add origin URL_DE_TU_REPOSITORIO
    git push -u origin main

Sustituye URL_DE_TU_REPOSITORIO por la dirección real de un repositorio vacío.

## Contenido
- app/page.tsx y app/studio.css: nueva interfaz y editor de estilos de demostración.
- app/local/: editor local de videos.
- app/studio/: panel de tareas y resultados del procesador.
- app/api/cloud/ y lib/clip-processor.ts: conexión del servidor web al procesador.
- processor/: API Python, transcripción, selección de fragmentos y exportación FFmpeg; incluye Dockerfile e instrucciones DEPLOY.md.
- public/: recursos y paquete del procesador.
- package.json y pnpm-lock.yaml: dependencias y comandos del frontend.

## Ejecutar la interfaz en desarrollo
Requiere Node.js >=22.13.0 y pnpm (versión declarada en package.json).

    pnpm install
    pnpm dev

Para compilar:

    pnpm build

El proyecto usa React, TypeScript y Vinext, con integración de Cloudflare Workers. No es una web estática para abrir index.html ni desplegar directamente en GitHub Pages.

## Alojar fuera de la plataforma original
Este paquete conserva el código de la versión publicada; no constituye una migración ya configurada a otro proveedor.
- La configuración .openai/hosting.json pertenece al alojamiento original; no contiene claves privadas. Adapta la configuración de despliegue al nuevo proveedor.
- app/chatgpt-auth.ts confía en cabeceras de identidad proporcionadas por el alojamiento original. En otro servidor hay que reemplazarlo por autenticación validada, o configurar un proxy de confianza que elimine cabeceras externas y establezca la identidad tras autenticar. No expongas la API confiando en cabeceras que pueda enviar cualquier visitante.
- Configura CLIP_PROCESSOR_URL y CLIP_PROCESSOR_KEY como secretos del servidor web. Nunca los pongas en el frontend ni los subas al repositorio.
- El procesador requiere su propio servicio Linux con FFmpeg y almacenamiento persistente. Consulta processor/DEPLOY.md.

## Estado real
La interfaz y los ejemplos de diseño están disponibles. Los ejemplos no son clips generados. El procesador aún necesita alojamiento y conexión. El seguimiento de rostros, B-roll de IA y publicación en redes no están implementados.
La versión exportada pasó TypeScript y compilación. La comprobación visual del navegador quedó pendiente por fallo de conexión del entorno. Las importaciones reales, la transcripción y los directos requieren pruebas al desplegar el procesador.
