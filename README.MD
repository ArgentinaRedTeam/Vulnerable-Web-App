# Desplegando una Aplicación NodeJS en Vercel
### Desplegar una Aplicación Docker NodeJS en Vercel de forma Local
Pasos Iniciales:
1. Forkear el Repositorio
# Configuración en Vercel:
1. Crear una Cuenta y Iniciar Sesión
   - Visita Vercel
   - [Vercel](https://vercel.com/) para crear una cuenta y realizar el login.
2. Instalar Vercel CLI:
   ```bash
   npm install -g vercel
   ```
3. Iniciar Sesión en Vercel desde la Terminal:
   ```bash
   vercel login
   ```
# Desplegar la Aplicación:
1. Dirigirse al Directorio del Proyecto
   ```bash
   cd path/to/your/project
   ```
2. Configurar el Proyecto en Vercel
   ```bash
   vercel
   ```
   Sigue las instrucciones para configurar el proyecto, seleccionando las opciones adecuadas.
3. Crear un Archivo `Dockerfile` en la Raíz del Proyecto si Aún no Existe
   ```Dockerfile
   FROM node:14

   WORKDIR /usr/src/app

   COPY package*.json ./
   RUN npm install

   COPY . .

   EXPOSE 3000
   CMD ["node", "app.js"]
   ```
4. Desplegar el Proyecto en Vercel
   ```bash
   vercel --prod
   ```
# Habilitar Integración con GitHub Actions en Vercel:
1. Configurar la Integración con GitHub
   - Desde la plataforma de Vercel, ir a la configuración del proyecto y seleccionar "Git Integration".
   - Conectar el repositorio de GitHub y configurar los permisos necesarios.
# Configuración de GitHub Actions para Despliegue Continuo:
1. Crear un Archivo `.github/workflows/deploy.yml` en el Repositorio
   ```yaml
   name: Deploy to Vercel

   on:
     push:
       branches:
         - main

   jobs:
     deploy:
       runs-on: ubuntu-latest
       steps:
       - name: Checkout code
         uses: actions/checkout@v2

       - name: Install Vercel CLI
         run: npm install -g vercel

       - name: Deploy to Vercel
         env:
           VERCEL_TOKEN: ${{ secrets.VERCEL_TOKEN }}
           VERCEL_PROJECT_ID: ${{ secrets.VERCEL_PROJECT_ID }}
           VERCEL_ORG_ID: ${{ secrets.VERCEL_ORG_ID }}
         run: vercel --prod --token $VERCEL_TOKEN
   ```
   **Reemplazar los siguientes datos:**
   - `VERCEL_TOKEN`: El token de acceso de Vercel, configurado en los secretos del repositorio.
   - `VERCEL_PROJECT_ID`: El ID del proyecto de Vercel.
   - `VERCEL_ORG_ID`: El ID de la organización de Vercel.

# Integración de Herramientas de Seguridad en el CICD:
Para mejorar la seguridad del proyecto, se pueden integrar herramientas como Snyk, CodeQL, o ESLint en el flujo de trabajo de GitHub Actions.

# Manos a la Obra:
Integra estas herramientas y configuraciones para asegurar y desplegar tu aplicación NodeJS en Vercel con éxito.
