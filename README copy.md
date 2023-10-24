
# Desafio Tecnico Hiring test Blue Express.

El siguiente proyecto busca resolver el desafio Tecnico para cargo de DevExp de la empresa Blue Express.

## ¿En que consiste?

A grandes rasgos, el desafio consiste en crear una aplicacion que exponga un endpoint con un metodo GET que al invocarlo obtenga un "!Hola Mundo!".
Luego se debe generar un pipeline CI/CD en GitHub actions, el cual genere prueba de la aplicacion, cree una imagen docker, la pushee a repositorio de imagenes de ECR y la despliegue en un cluster EKS.
Esta app debe estar expuesta a internet.


## Tecnologia Usada.

- La aplicacion fue construida con [NestJS](https://nestjs.com/)
- Como repositorio de codigo se uso [Github](https://github.com/)
- El pipeline fue creado mediante [Github Actions](https://github.com/features/actions)
- La imagen de la aplicacion es creada con [Docker](https://www.docker.com/)
- El repositorio de imagenes Docker se uso [Elastic Container Registry](https://aws.amazon.com/ecr/) (ECR) de AWS 
- El motor de Kubernetes que corre estas imagenes es [Elastic Kubernetes Service](https://aws.amazon.com/eks/) (EKS) de AWS 


## ¿Que hay dentro de este repositorio?

En este repositorio se encuentra la solucion completa del desafio y esta dividido en las siguientes carpetas:

**Carpeta raiz**: Dentro de la carpeta raiz se encuentran los archivos base de la aplicacion NestJS (*nest-cli.json, .eslintrc.js, .prettierrc, package.json, package-lock.json, tsconfig.build.json, tsconfig.json*).
Tambien esta el archivo para generar la imagen docker: *Dockerfile* y a su vez  el archivo *.dockerignore* no intrtoducir a la imagen docker elementos demas al interior de las imágenes de Docker.
Finalmente esta el archivo *.gitignore* para no subir al repositorio git archivos o carpetas no deseados. 

**.github\worflows**: Aca esta el archivo con el contenido de Github actions.

**test**: Esta carpeta contiene las pruebas unitarias de la aplicacion.

**src**: Es el codigo fuente de la aplicacion.




### Aplicacion NodeJS

Como se menciono anteriormente, esta app fue creada con [NestJS](https://nestjs.com/).
Contiene simplemente un metodo GET basico (en la raiz de la aplicacion), el cual responde **¡Hola Mundo!**

### Instalacion local
Dentro de la carpeta helloworldapp

```bash
# install
$ npm install
```

### Corriendo la app localmente
Dentro de la carpeta helloworldapp

```bash
# run
$ npm run start
```
La aplicacion por defecto corre en el puerto 3000
### Pruebas unitarias
Dentro de la carpeta helloworldapp

```bash
# unit tests
$ npm run test
```

### Invocacion
Una vez corriendo la aplicacion, simplemete hay que llamar a la raiz de donde esta corriendo y para ello, se puede invocar de diversas formas:
Ej:

- Curl
`curl http://localhost:3000`

- Browser
http://localhost:3000

- Postman (usando metodo get y url http://localhost:3000)


## 'Dockerizando' la aplicacion
Para crear una imagen docker de la aplicacion, se debe usar el archivo Dockerfile, el cual contiene las rutinas para crear la imagen. La forma de crear localmente una imagen es:

```bash
# Creando imagen docker version 0.0.1
$ docker build -t helloworldapp:0.0.1 .
```
Luego de creada, puedo ejecutarla localmente con el comando:
```bash
# Corriendo localmente imagen helloworldapp:0.0.1
$ docker run -p80:3000 helloworldapp:0.0.1
```
Nota: El cambio de puerto desde 3000 a 80 no es necesario, pero se hizo por simplicidad y para poder invocar la app desde el browser directamente como http://localhost .


## Creando el pipeline CI/CD
Se creo un pipeline de acuerdo a los requerimientos, el cual tiene 3 trabajos (jobs) principales:

1. **buildAndTest**: En esta etapa, se hace un checkout del codigo, se hace un npm ci (es como npm build pero mas orientado a automatizaciones puesto que hace un clean build) y luego ejecuta las pruebas unitarias.

2. **createDockerImageAndPush**: Aca se hace un login a la cuenta de AWS se crea la imagen Docker, se taguea y pushea al registro ECR

3. **deploy**: Este pipeline se conecta al cluster de EKS y despliega la imagen pusheada en el paso anterior.

### Creando el manifiesto de Kubernetes
**TODO**

### Probando la aplicacion desde Internet
**TODO**

