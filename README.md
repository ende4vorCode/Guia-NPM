# NPM

- Una lista de apuntes sobre NPM, incluye funcionalidades y una explicación de los comandos, como seguridad y publicación de paquetes.

## Que es NPM?

- Node Package Manager es un gestor de dependencias de javascript, con el cual podemos administrar las dependencias e incluso crear las nuestras propias.

## Primeros pasos

- Primero necesitamos tener un espacio de trabajo, para evitar problemas. -> take "workspace".
- `git init` Con este paso inicializamos con git el proyecto.
- `npm init` Con este comando creamos un proyecto con npm. Seguimos los pasos.

## Instalando dependencias

- `npm install "nombre del paquete"`
- Hay que tener cuidado, asi que existen distintas flags
- `npm install "nombre del paquete" --save-dev` o `npm install "nombre del paquete" -D` Dependencias utilizadas para cuando el el proyecto esta en etapa de desarrollo.
- `npm install "nombre del paquete" -S` o `npm install 'nombre del paquete' --save` Si vemos en el package.json podemos ver que se crean dos etapas distintas, una con el apartado de desarrollo y otra con el apartado de save.
- `npm install -g "nombre del paquete"` Instalar paquetes globales.
- `npm install "nombre del paquete" -o` Instalamos paquetes de forma opcional.
- `npm list` Muestra los paquetes que tenemos instalados en el proyecto.
- `npm list -g` Muestra los paquetes instalados globalmente.
- `npm install "nombre del paquete" --dry-run` Nos permite ver si es que dos paquetes tienen conflictos entre si.
- `npm install "nombre del paquete"@"version"` Nos permite instalar una version especifica del proyecto. Si en version ponemos latest, instalaremos la version mas reciente de dicho paquete.
- `npm install` Instalaremos los paquetes que estén dentro del archivo package.json.

## Scripts

- Los scripts nos permiten automatizar ciertas funcionalidades.
- Creamos una carpeta src `mkdir src` y dentro de este archivo crearemos un archivo `index.js`
- Dentro de este archivo pondremos un console.log('Hola soy un script'), esto para probar el script.
- Dentro del `package.json` en la sección de scripts, pondremos lo siguiente `"start" : "node src/index.js"` Aquí lo que estamos haciendo es crear un parámetro para npm en el cual ejecutaremos dentro de nodejs el archivo index.js
- `npm run start` Con este comando veremos si es que el comando esta disponible y luego lo ejecutara.
- En la creación de los scripts, también podemos utilizar ciertas opciones, como el &&. Esto nos permite crear varias ejecuciones dentro del mismo comando. Ejemplo: package.json -> `"comando" : "Acción-1 && Acción2"` entonces al ejecutar `npm run comando` Ejecutara ambos comandos que hayamos creado.

## NPX

- Node package execute -> Nos permite ejecutar acciones, sin tener que instalar previamente alguna dependencia.
- Por ejemplo, con `npx create-react-app "nombre de la app" -y` Podremos crear una aplicación de React, sin tener que instalar y crear script paso a paso. Esto nos creara un proyecto pre configurado.

## Actualizar o Eliminar dependencias

- Teniendo en cuenta que ya tenemos un proyecto base o que copiamos alguno desde un repositorio remoto, este puede tener problemas de actualización o dependencias directamente obsoletas. Entonces podemos seguir este proceso. -> Estos procesos son de los mas importantes.
- `npm install` Instalamos todo, aquí nos mostrara las vulnerabilidades de las dependencias instaladas.
  - Aquí podemos encontrar mucha información, entre ellas las mas importantes son las vulnerabilidades. Donde aquellas que sean "high" hay que prestarles mucha atención y ojala arreglarlas y por otro lado "critical" las cuales si o si deben ser reparadas.
- `npm list` Lista las dependencias instaladas.
- `npm outdate` Lista las dependencias que están des actualizadas. (No es necesario actualizar todas, porque puede romper el proyecto completo.)
- `npm install "nombre del paquete@latest" --dry-run` En este punto veremos si es que se necesitan actualizar otras dependencias antes, de la que queremos instalar. De mas esta decir que si no hay conflicto, solo instalamos.
- `npm install "nombre del paquete"@latest` Aquí instalamos las versiones de todos los paquetes que lo requieran.

### Seguridad de la aplicación

- Teniendo en cuenta las situaciones anteriores, necesitamos ver que dependencias entran en conflictos.
- `npm audit` Revisa que dependencias tienen problemas.
- Aquí encontraremos la información que necesitamos e incluso links para ver discusiones sobre dichas vulnerabilidades.
- `npm audit --json` Nos mostrara esta información mucho mas detallada de estas vulnerabilidades.
- `npm audit fix` Instalara los recursos necesarios para solucionar los problemas mas críticos al menos.
- `npm audit fix --force` Forzar a "reparar" los paquetes a bajo nivel. Es posible que esto no repare todos los paquetes que necesitamos, entonces aquí hay que hacerlo a mano.
- Aprovechamos que el comando anterior nos muestra los paquetes que no ha actualizado. ejecutaremos la actualización de estos de forma manual `npm install "nombre del paquete"@latest` latest no es estrictamente necesaria, porque recuerden que se puede romper el proyecto, entonces podemos sustituirla por una version que corrija el error, esto puede dar paso a mas errores (No necesariamente relacionados con los paquetes, sino que con el código de nuestra app).
- `npm ci` Mostrara las dependencias que están deprecadas o fuera de actualización, con esto podemos preparar el proyecto para actualizarlo cuando sea necesario.

## Eliminación de dependencias y Package Lock

- `npm uninstall "nombre del paquete"` Eliminara todo lo que conlleve esta dependencia.
- También podemos eliminarlo desde el package.json
- Ahora hay que instalar nuevamente el proyecto.
- `rm -rf node_modules` Eliminamos la carpeta.
- El package-lock.json contiene la información detallada de los componentes del proyecto, este se crea al instalar las dependencias con npm.
- `"phoenix": "rm -f package-lock.json && rm -rf ./node_modules && npm install --no-fund --no-audit"` Este comando eliminara el package-lock.json y el node_modules, posteriormente instalara todo correctamente.
- Existe una flag importante, sobre todo para el tema de pasar el proyecto a producción, tomemos el ejemplo anterior en el cual estamos utilizando React, utilizamos el comando `npm run build -dd` -dd es la flag que nos muestra la información completamente detallada del proceso.

## Crear un paquete y publicarlo.
- Primero debemos crear una cuenta en [npm](https://www.npmjs.com/)
- Ahora debemos crear un proyecto en [GitHub](https://github.com/) El cual debe tener el mismo nombre que el paquete que subiremos.
- Verificamos en la pagina de npm si es que el proyecto ya existe. Si no existe creamos el repositorio que creamos.