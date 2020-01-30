# Ionic 4 - `Angular`
## Login Con Google y Facebook 
Implementar un login con google o con facebook en ionic puede ser un dolor de cabeza para muchos desarrolladores de app móviles híbridas, pero con esta guia dejara de ser una molestia, espero que les sea de mucha utilidad y recuerden que esta guia esta enfocado en proyectos Ioni con Angular.
Funcionando desde el `30/01/2020`

## Configuración previa
Para desarrollar el login con google y facebook, debemos primero conectar nuestro proyecto ionic a firebase, para esto debemos:
 1. Crear un proyecto en firebase
 2. Instalar angularfire2 en nuestro proyecto Ionic
 3. Configurar nuestro proyecto Ionic

### 1. Crear un proyecto en firebase
Antes de empezar a desarrollar el login debemos crear una cuenta en firebase, no tiene ningun costo para lo que necesitamos ahora, luego de que tengamos una cuenta en firebase debemos crear un proyecto desde la consola de firebase en la opción añadir proyecto como se puede ver en la siguiente imagen.

![](https://i.imgur.com/Wqiouur.png)

luego nos pedirá un nombre para el proyecto, ingresamos el nombre que desee, en este caso sera LoginGaF.

![](https://i.imgur.com/A08W4QM.png)

Ahora google nos preguntará si queremos utilizar Google Analytics, en este caso no lo utilizaremos pero le igual le damos en continuar.

![](https://i.imgur.com/RlxU8js.png)

Luego seleccionamos una ubicación, aceptamos los terminos y condiciones, y le damos en crear proyecto, y finalmente tendremos nuestro proyecto creado en firebase.

### 2. Instalar angularfire2 en nuestro proyecto Ionic
Tenga en cuenta que esta guía consiste en explicar como implementar un login con google y facebook utilizando un proyecto ionic ya existente, en esta guia utilizaremos el proyecto que se encuentra en el [commit 3 Diseño del ejemplo](https://github.com/Bianfa20/LoginGoogleAndFacebook/tree/1a79f88f1f8596cd5091a5cc7326dbd20aeb370d) del repositorio: [LoginGoogleAndFacebook](https://github.com/Bianfa20/LoginGoogleAndFacebook).

##### Vista del diseño:
![](https://i.imgur.com/BrygreP.png)

Para instalar angularfire2 solo necesitamos ejecutar el siguiente comando por terminal, desde el proyecto:

```sh
\ProyectoIonic> npm install @angular/fire firebase --save
```

### 3. Configurar nuestro proyecto Ionic
Para configurar nuestro proyecto ionic primero debemos obtener los datos de configuración de nuestro proyecto firebase desde la consola de firebase, para esto le damos click al icono `(marcado en rojo)` para luego ingresar a la configuración del proyecto `(marcado en azul)`, como podemos ver en la siguiente imagen.

![](https://i.imgur.com/jo6eubZ.png)

Ahora le damos en el boton `marcado en rojo` en la siguiente imagen.

![](https://i.imgur.com/IkRwkK2.png)

Ahora google nos pedirá un apodo para la aplicación, puedes poner el que desee, en este caso pondre de nuevo LoginGaF y le damos en registrar aplicación.

![](https://i.imgur.com/V8Lr2k4.png)

Y obtendremos los datos necesarios para configurar nuestro proyecto ionic, copiamos toda la variable firebaseConfig `marcado en un cuadro negro`, como podemos ver en la siguiente imagen.

![](https://i.imgur.com/VDk8izv.png)

Ahora que tenemos los datos de firebaseConfig, abrimos el archivo `/src/enviroments/enviroments.ts` de nuestro proyecto ionic y exportamos una nueva constante `firebaseConfig`

```javascript
export const environment = {
    production: false
};

export const firebaseConfig: {
    apiKey: "<tu apikey>",
    authDomain: "<tu authDomain>",
    databaseURL: "<tu databaseURL>",
    projectId: "<tu projectId>",
    storageBucket: "<tu storageBucket>",
    messagingSenderId: "<tu messagingSenderId>",
    appId: "<tu appId>",
    measurementId: "<tu measurementId>"
}
```

Y para terminar la configuración de nuestro proyecto debemos que importar la variable `enviroment` que es la que editamos anteriormente y debemos que añadir también el modulo `AngularFireModule` para conectar nuestro proyecto a firebase y `AngularFireAuthModule` para utilizar el servicio de autenticación de firebase en el archivo `/src/app/app.module.ts`

```javascript
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
...

// Firebase
import { firebaseConfig } from '../environments/environment';
import { AngularFireModule } from '@angular/fire';
import { AngularFireAuthModule } from '@angular/fire/auth';

@NgModule({
  declarations: [AppComponent],
  imports: [
    BrowserModule,
    IonicModule.forRoot(),
    AppRoutingModule,
    AngularFireModule.initializeApp(firebaseConfig), //Modulo 1 a importa
    AngularFireAuthModule // Modulo 2 a importar
  ],
  bootstrap: [AppComponent]
})
export class AppModule {}
```