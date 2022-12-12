# Delilah Restó 

Este proyecto planteó la creación de un sistema de pedidos online para un restaurante poniendo en funcionamiento las partes necesarias para montar una REST API que permita realizar operaciones CRUD sobre una estructura de datos.

## Construido con 

- Node JS
- Express js
- Sequelize
- MySQL
- JWT
- Postman
- Swagger

## Documentación 

Archivo `spec.yaml` Para verlo mejor, puede copiarlo y abrirlo con [Swagger](https://editor.swagger.io/)

## Instalación ⚙

Clonar el repositorio de [GitHub](https://github.com/camilobr1/delilahRestoCamiloBravi.git)

```
git clone https://github.com/camilobr1/delilahRestoCamiloBravi.git
```

## Dependencias 

Instalar las dependencias requeridas para el correcto funcionamiento de la aplicación

```
npm install express
npm install sequelize
npm install mysql2
npm install body-parcer
npm install jsonwebtoken
npm install cors
npm install nodemon
```

## Base de datos SQL 

Documento `delilahrestocamilo.sql`

1. Instalar [Xamp](https://www.apachefriends.org/es/index.html) y abrir el panel de control, iniciando MySQL y Apache.
 1b. Es muy importante verificar que MySQL este corriendo el el puerto 3307, y no en el que viene por defecto (3306)
2. Abrir el navegador con localhost, phpmyadmin y en sql crear el schema "delilahrestocamilo".
3. Replicar las tablas del documento.

## Inicio del servidor 

En la terminal:

```
node index.js
```

Recibirá el mensaje:

```
El servidor está funcionando correctamente en puerto 3000
```

Probar la API con [Postman](https://www.postman.com/)

1.  ### **Usuarios** 

    ```
    http://localhost:3000/usuarios
    ```

    #### a. Método POST

    Crear un nuevo usuario con el siguiente formato de body en raw, json:

    ```
    {
    "username": "CamiloBravi",
    "fullname": "Camilo Bravi",
    "email": "camilobravi@gmail.com",
    "phone": "35167896644",
    "address": "Mauricio Yadarola 600",
    "password": "MiclavePersonal",
    "is_admin": false
    }
    ```

    El campo "is_admin" está seteado para que al poner "false" o "true"; "0" o "1"; siempre se cargue false. Es decir usuario no administrador.
    El administrador está ya cargado previamente, con el sign 5

    ```
    "username": "Emilio",
    "password": "28Agosto"
    ```

    #### b. Login:

    "http://localhost:3000/login"
    Método POST
    BODY: raw, jason

    ```
    {
    "username": "Emilio",
    "password": "28Agosto"
    }
    ```

    para el caso de querer loguear el administrador; en caso de querer loguear otro usuario existente o el creado recientemente, reemplazar los datos del username y del password, por los correspondientes.
    Se recibe el Token que utilizará para las operaciones CRUD de las 3 tablas.

    #### c. Método GET:

    ( Se debe loguear previamente) "http://localhost:3000/usuarios"
    Autorización BEARER TOKEN y copiar el Token recibido en el login

    a) Si el usuario logueado es un usuario común, podrá ver sus datos.

    b) Si quien está logueado es el Administrador, verá los datos de todos los usuarios.

2.  ### **Productos** 🍛

    ```
    http://localhost:3000/productos
    ```

    #### a. Método GET

    Todos los usuarios pueden ver los productos existentes ( Colocando su token de Login en Autorización, Bearer Token)

    #### b. Método POST

    (Solo admnistrador puede cargar nuevos productos)
    formato:

    ```
    {
    "product_name": "Alitas de Pollo Rebozadas",
    "price": 1350,
    "stock": 1,
    "img_url": "dirección de la imagen del producto",
    "category": "Pollo"
    }
    ```

    #### c. Método PUT

    (Solo admnistrador puede modificar productos)
    formato:

    ```
    {
    "product_name": "Alitas de Pollo Rebozadas con salsa picante",
    "price": 1350,
    "stock": 1,
    "img_url": "dirección de la imagen del producto",
    "category": "Pollo"
    }
    ```

    #### d. Eliminar producto

    ```
    http://localhost:3000/productos/:id
    ```

    Se debe colocar como parámetro el ID del producto a eliminar
    Método DELETE (Solo administrador puede eliminar productos)

3.  ### **Pedidos**

    #### a. Crear pedido

    Método POST
    formato:

    ```
    {
    "products": [
    {
    "product_id": 2,
    "quantity": 3
    }, {
    "product_id": 7,
    "quantity": 2
    }
    ],
    "payment_method": "Efectivo"
    }
    ```

    #### b. Ver pedido

    Método GET
    *El usuario común verá la información de su pedido
    *El usuario con rol de administrador, verá todos los pedidos, y podrá cruzar la información con los datos de la tabla "info_pedidos"

    #### c. Modificar el estdo del pedido

    ( Solo el administrador)

    ```
    http://localhost:3000/pedidos/:id
    ```

    ( reemplazar :id por el id del pedido a modificar)
    Método PUT
    formato del body, raw, jason:

    ```
    {
    "status": "Enviado"
    }
    ```

    #### d. Eliminar pedido

    ( solo el administrador)

    ```
    http://localhost:3000/pedidos/:id
    ```

    (reemplazar :id por el id del pedido a eliminar)
    Método DELETE

## Autores

- **Camilo Bravi** - _Desarrolo web_ - [camilobr1](https://github.com/camilobr1)
- **Acámica** 

## Repositorio 📚

- [GitHub](https://github.com/camilobr1/delilahRestoCamiloBravi.git)
