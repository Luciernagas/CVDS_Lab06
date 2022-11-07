## Laboratorio CI/CD Azure DevOps
## ♡ Luisa Valentina De la hoz Rocha ♡
- - -
#### Tarea 1: Configuración de los recursos de Azure
Primero se creo el proyecto siguiendo los pasos dados en los requisitos previos del laboratorio de Azure DevOps
![image](https://user-images.githubusercontent.com/104604359/200205016-32402e52-3c0b-4d0c-a2c5-e4e3ff1a8618.png)

![image](https://user-images.githubusercontent.com/104604359/200205027-8a6f807f-af44-420e-a1f7-353d8ad5f2ff.png)

Después hacemos click en Crear un recurso y busque "Base de datos SQL" . Seleccionamos Base de datos SQL 
![image](https://user-images.githubusercontent.com/104604359/200205036-ea646eac-568c-44ce-b15e-16de32b57eed.png)

![image](https://user-images.githubusercontent.com/104604359/200205045-b82e9890-914e-4529-b0a1-2f1a76fbccb7.png)

![image](https://user-images.githubusercontent.com/104604359/200205062-b1a0212f-d4d7-4ed2-a862-174d907856c4.png)

Después en la página de inicio de Azure Portal, buscamos "Servicios de aplicaciones" y seleccione Servicios de aplicaciones .
Haga clic en Crear en la página Servicios de aplicaciones.
En Detalles del proyecto , seleccione la misma suscripción y grupo de recursos utilizados para la base de datos.
![image](https://user-images.githubusercontent.com/104604359/200205071-00394990-fbc7-43d5-83b6-2352e0fb8210.png)

![image](https://user-images.githubusercontent.com/104604359/200205080-4a4cc538-b960-4174-8d96-fab655c5f0e7.png)

![image](https://user-images.githubusercontent.com/104604359/200205093-ead6c4b1-b793-4881-82f7-187b4ee0add4.png)

Repetimos el proceso anterior para crear un segundo servicio de aplicaciones para la etapa de producción. Esta vez, agregamos el Nombre con "-prod" en su lugar. 
![image](https://user-images.githubusercontent.com/104604359/200205101-02545bac-2c4c-4927-a1b9-f3ff1c8ebaa3.png)

![image](https://user-images.githubusercontent.com/104604359/200205149-10db3c5e-47da-413b-b68c-c0b1b1b91a59.png)

#### Tarea 2: Crear una versión continua para la etapa de control de calidad
Navegamos en Piperlines | Releases  y eliminamos el piperline de lanzamiento de PartsUnlimitedE2E existente . Empezaremos de nuevo aquí.
![image](https://user-images.githubusercontent.com/104604359/200205182-a89d6b4f-da22-4c9b-ba8f-ce3bd22b7666.png)

![image](https://user-images.githubusercontent.com/104604359/200205208-48d60bed-6b68-4b4e-8bfd-d0cfdba2dd8a.png)

Hay muchos tipos de artefactos, pero este será bastante simple: un proyecto creado a partir de la canalización de compilación PartsUnlimitedE2E que ya existe en este proyecto de equipo. Haga clic en Agregar .

![image](https://user-images.githubusercontent.com/104604359/200205304-74e75dce-221c-43ca-b974-62f6c2586726.png)

Seleccione la suscripción de Azure que usó anteriormente para crear los recursos y haga clic en Autorizar . Si necesita crear una conexión a una cuenta de Azure asociada con una cuenta de Microsoft diferente, haga clic en Nuevo y siga ese flujo de trabajo antes de continuar y Ingrese el nombre del servicio de la aplicación que se usó anteriormente al crear el servicio de la aplicación QA.
![image](https://user-images.githubusercontent.com/104604359/200205314-9dd1dfbf-5f30-4eca-8339-04083d7c00d2.png)

Habilite el activador de implementación continua . Agregue un filtro de rama de compilación que apunte a la rama predeterminada de la canalización de compilación . Esto iniciará la implementación cuando se complete la compilación.
![image](https://user-images.githubusercontent.com/104604359/200205389-4c98c800-8266-4ff8-86b6-faa03bd81458.png)

#### Tarea 3: Configuración de los servicios de aplicaciones de Azure
Vuelva a la pestaña del navegador abierta en Azure Portal.
Haga clic en la pestaña Grupos de recursos en el menú de la izquierda. Localice y haga clic en el grupo partsunlimited creado anteriormente.
En la hoja nueva, haga clic en Mostrar cadenas de conexión de base de datos .
Esto le proporcionará una lista de cadenas de conexión según la plataforma. Copie la cadena ADO.NET en su portapapeles para que pueda configurar su nuevo sitio web para usarlo.
![image](https://user-images.githubusercontent.com/104604359/200205439-66ee0f73-fe82-4536-b5b5-1b9daf3489ff.png)

Localice la sección Cadenas de conexión y agregue una nueva entrada con la clave "DefaultConnectionString" y el valor pegado desde el portapapeles. Deberá ubicar las secciones "{su_nombre de usuario}" y "{su_contraseña}" y reemplazarlas (incluidas las llaves) con las credenciales SQL reales ingresadas anteriormente. Asegúrese de que Tipo esté establecido en SQLAzure y haga clic en Aceptar .
![image](https://user-images.githubusercontent.com/104604359/200205447-7192e203-9b67-456c-9c06-bb66a01fbba2.png)

Repita el proceso anterior para agregar la misma cadena de conexión al servicio de aplicaciones de producción.
![image](https://user-images.githubusercontent.com/104604359/200205453-7f445611-f943-4f52-ad9e-59b0d54a95fb.png)


#### Tarea 4: invocar una liberación de entrega continua para el control de calidad
Vaya a PartsUnlimited-aspnet45/src/PartsUnlimitedWebsite/Views/Shared/_Layout.cshtml . Este es un archivo que define el diseño general del sitio y es un buen lugar para hacer un cambio que será fácilmente visible después de la implementación.
Localice el logotipo de Parts Unlimited y agregue el texto "v2.0" después. Esto será fácil de comprobar después de la implementación.
![image](https://user-images.githubusercontent.com/104604359/200205468-6fda39ab-2185-4c80-aa72-f2017f2ef63b.png)

Abra la versión más reciente de PartsUnlimitedE2E . Puede estar en cola, en progreso o ya completado.
![image](https://user-images.githubusercontent.com/104604359/200205480-1e47d695-e0a2-4fd0-85d2-8e26d92bbd63.png)

![image](https://user-images.githubusercontent.com/104604359/200205487-9ac264b4-5f33-442f-bbb1-59f1c19b0075.png)

#### Tarea 5: Crear una versión cerrada para la etapa de producción
A medida que los canales de lanzamiento se vuelven más sofisticados, se vuelve importante definir puertas para garantizar la calidad en todo el canal de lanzamiento. Dado que la próxima etapa en la que estamos implementando es la producción, debemos asegurarnos de incluir tanto las puertas de calidad automatizadas como una puerta de aprobación manual. Vuelva a la pestaña del navegador de canalización de versión y haga clic en Clonar en la etapa de control de calidad . Dado que la etapa de producción es prácticamente la misma, podemos reutilizar casi toda la configuración existente.
![image](https://user-images.githubusercontent.com/104604359/200205631-2f52b4b7-e8db-431a-9f8b-cc24d16f7aad.png)

![image](https://user-images.githubusercontent.com/104604359/200205646-ddae1484-b92d-4a53-b985-bfe347aaef52.png)

![image](https://user-images.githubusercontent.com/104604359/200205660-4a587616-28ef-4eb8-9af8-0664288ec8a9.png)

![image](https://user-images.githubusercontent.com/104604359/200205680-32dc70e7-21de-4021-abaa-89afee1b2ac3.png)


Para que Query Gate funcione, Project Build Service requeriría permiso de lectura para las consultas. Vaya a Azure Boards > Consultas > Todas > Consultas compartidas > “…” > Seguridad .
![image](https://user-images.githubusercontent.com/104604359/200205688-a12abe34-3fd3-4517-a1fe-ee05601e5ca1.png)

Busque el proyecto , si no está incluido de forma predeterminada (¡no el servicio de compilación de la colección de proyectos!) y déle permiso de lectura > Permitir 
![image](https://user-images.githubusercontent.com/104604359/200205699-fe451ffd-7534-45c3-8c72-9e362b866643.png)

![image](https://user-images.githubusercontent.com/104604359/200205714-d2520b37-edba-4a2c-a9e6-b50562b21532.png)

Habilite las aprobaciones previas a la implementación y agréguese como aprobador . La idea aquí es que no se le pedirá que apruebe la implementación de producción hasta que la implementación de control de calidad se haya realizado correctamente. En ese momento, alguien de esta lista deberá aprobar la implementación en producción. También borre la casilla para que el usuario que solicita una versión de implementación no debe aprobar si está marcada. A los efectos de esta práctica de laboratorio, puede aprobar las liberaciones que haya solicitado.
![image](https://user-images.githubusercontent.com/104604359/200205725-41ef5d84-3176-45c5-91af-8e878860f14a.png)

![image](https://user-images.githubusercontent.com/104604359/200205736-f03e15ad-2e65-4e70-b406-12cb525841ec.png)

Repita el proceso para cambiar la base de código en "PartsUnlimited-aspnet45/src/PartsUnlimitedWebsite/Views/Shared/_Layout.cshtml" seguido anteriormente en una nueva pestaña. Esta vez, actualice el número de versión de "2.0" a "3.0" . Esto invocará la canalización de versión.
![image](https://user-images.githubusercontent.com/104604359/200205751-38da54ad-6865-42d2-80ce-f092c8ea860a.png)

![image](https://user-images.githubusercontent.com/104604359/200205760-8da2a6af-1630-48db-bfbb-b2168343548e.png)

![image](https://user-images.githubusercontent.com/104604359/200205782-9e0742a7-017c-40a4-8296-9f3b9be89ab9.png)

![image](https://user-images.githubusercontent.com/104604359/200205793-0c3ebe3d-ca5b-4a72-b55d-dff81fe63dd7.png)

![image](https://user-images.githubusercontent.com/104604359/200205805-0a2957b6-d105-4dfe-acc3-9d157ff0890a.png)

Por lo general, consultaría el sitio para confirmar que se solucionó el error, pero nos saltaremos aquí y lo marcaremos como Listo . Haga clic en Guardar y cierre la pestaña.
![image](https://user-images.githubusercontent.com/104604359/200205814-d3a82cdf-e18b-4ecc-a5f4-13a48c53127a.png)
