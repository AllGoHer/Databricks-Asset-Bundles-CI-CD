# Databricks-Asset-Bundles-CI-CD
_________________________________________________________________________________________________________________________________________________________________________________________________________________

**PREREQUISITOS:**

Primero, en la terminal instalamos UV de python

Segundo, instalamos Databricks CLI

Código:

        winget install Databricks.DatabricksCLI

Ahora iniciamos abriendo el Visual Studio Code y vinculamos con una carpeta (AssetBundles).

Luego, abrimos la terminal (ctrl + shift + tab ó crtl ñ) y, probamos que Databricks está bien instalado.

Código:

        Databricks -v

![image](https://github.com/user-attachments/assets/2b9713d8-02bf-4376-badc-20e5a42aa927)

Ahora, vamos a conectar VSCode con Databricks.

Vamos a Databricks y, seleccionamos SQL Warehouses

![image](https://github.com/user-attachments/assets/22197f28-3ae1-49e0-989b-4695e0dcd8ab)

Luego hacemos click en severless Starter Warehouse y, en la ventana emergente seleccionamos connection details.

![image](https://github.com/user-attachments/assets/3181732d-1ccb-44fb-a207-83c36c3c0275)

Copiamos el server hostname

![image](https://github.com/user-attachments/assets/3d1af169-15c0-468f-be8f-9b3f1709bc4e)

y en la terminal de VSCode escribimos el siguiente código.

código:

        Databricks auth login 

Y al final de ese código pegamos el código del server hostname que copiamos.


![image](https://github.com/user-attachments/assets/0e764d31-b673-4908-b77e-a1b8eae9357e)

Luego, escribimos DEV en Databricks profile name [DEFAULT]: 

![image](https://github.com/user-attachments/assets/8d265099-bdaa-41f5-93e9-4870c585cf59)

El cual, pedirá una autorización a través de una ventana emergente de databricks, en el cual, daremos click en autorizar.

![image](https://github.com/user-attachments/assets/e1960c32-d816-4676-bff6-66d81a8b8248)

![image](https://github.com/user-attachments/assets/63203a30-9425-4c50-b8b9-5e00f37c3694)

![image](https://github.com/user-attachments/assets/a2553f59-80c7-4ca0-8991-7ccc98a81e88)

<nark>NOTA:</mark> para conocer todos los comandos profile para databricks solo escribe en la termina de VSCode so siguiente.

Bash:
     
          Databricks profiles -h

Ahora, veremos Autenticación de perfiles-

Codigo:

        databricks auth profiles


![image](https://github.com/user-attachments/assets/cea067ca-b1d3-459b-889b-96aa54862498)

Si quiere ver los catalogos que tienes en databricks deberas ejecutar el siguiente codigo.

Codigo:

        Databricks catalogs list

![image](https://github.com/user-attachments/assets/84e6f1d4-c35c-4c2c-9aec-a42fbf13ab6c)

![image](https://github.com/user-attachments/assets/9f7fd024-3ccb-444e-bf89-95e6cc2f52d4)

Luego iremos a nuestro disco C /usurio/usurio y encontraremos un archivo que se generó automáticamente mediante la autenticación llamado .databrickscfg, el cual, abriremos con VSC y lo editamos eliminando la parte que dice default, solo quedando desde la parte que dice DEV hacia abajo.

![image](https://github.com/user-attachments/assets/e786e102-7a5e-44ff-bcc8-ce15b718f8bf)

![image](https://github.com/user-attachments/assets/97e47787-e162-4e3b-a505-7ab0b26478a9)

Debe quedar así.

![image](https://github.com/user-attachments/assets/cfa5a8b4-9a06-4974-851d-a5cce56fdad0)

Nos vamos a Databricks para crear un catálogo.

![image](https://github.com/user-attachments/assets/d068f2e9-c172-41fb-9473-2628231f790a)

Todos los espacios de trabajo tienen acceso

![image](https://github.com/user-attachments/assets/976d26c5-03ae-4ef0-b765-650eb79a7c98)

Luego, damos click en create -> next -> save.

![image](https://github.com/user-attachments/assets/1a58d9e5-c82c-4233-a7ce-32f47570a88d)

Buscaremos ahora acceso los catalogos de asset_bundles.

Código:

        databricks catalogs get asset_bundle --profile DEV


![image](https://github.com/user-attachments/assets/db7896f1-f3e4-4e58-b3b1-69f0aa9233d9)

Ahora, crearemos un esquema

Código:

        Databricks schemas create bronze asset_bundle


![image](https://github.com/user-attachments/assets/d78e2d78-7145-4345-81bb-2e6d8247df85)

Comprobamos en Databricks.

![image](https://github.com/user-attachments/assets/519c53a7-6b2c-4dfd-abb8-e084e0dc0f88)

![image](https://github.com/user-attachments/assets/f4159773-3969-4f85-9fdb-19f9df61b80d)

Iniciamos los paquetes de Databricks.

Código:

        Databricks bundle init

Luego, presionamos enter.


![image](https://github.com/user-attachments/assets/dfe30297-d9ba-4451-8278-2d94260d9956)

Le asignamos un nombre, en este caso, la abreviación de Databricks asset bundles (dab)

![image](https://github.com/user-attachments/assets/9ab75856-7626-4f6f-85eb-c4194b54e789)

Ya no estará dentro de Asset_Bundles.


<mark>NOTA:</mark> si gustas, para tener archivos mas limpios, puedes eliminar el contenido de las carpetas de resources, src y test.

Ahora, nos vamos a Databricks en workspace y creamos una carpeta PROD.


![image](https://github.com/user-attachments/assets/6fdbac48-3e12-4d0a-a285-e05362af1822)

Regresamos a VSC y creamos un archivo llamado notebooks en la carpeta SRC y dentro del notebook1.ipynb

![image](https://github.com/user-attachments/assets/6e4b4d8a-7ce3-4c2a-81cd-029b2c951217)

Código:

       print("Hello World")

Nos vamos a la terminal para desplegar.

Código:

        databricks bundle deploy  --target dev



NOTA: en caso que al ejecutar da error, aplica el siguiente código en power shell.

1. Ejecutar codigo

Código:

       # Crear la estructura de carpetas

        mkdir src\dab -Force

       # Crear un archivo __init__.py vacío
        New-Item src\dab\__init__.py -ItemType File

       # Crear un archivo main.py básico
        @"
        def main():
            print("Hello from dab!")

        if __name__ == "__main__":
            main()
        "@ | Out-File src\dab\main.py -Encoding UTF8


2. Ahora, en tu proyecto en el archivo pyproject.toml agrega esta sección al final del código.


[tool.hatch.build.targets.wheel]

packages = ["src/dab"]



![image](https://github.com/user-attachments/assets/35365fb8-eac6-42bf-b2f6-529ac8f36217)

3. Verifica que src/dab/__init__.py existe
   
El archivo __init__.py es obligatorio para que Python reconozca la carpeta como un paquete. Si no existe, créalo:

Powershell:

            # Si no existe, créalo
            if (!(Test-Path src\dab\__init__.py)) {
                New-Item src\dab\__init__.py -ItemType File
            }

4. Ejecuta la construcción localmente para probar

Powershell:

            # Primero, sincroniza las dependencias
            uv sync --dev

            # Luego, prueba construir el wheel localmente
            uv build –wheel


Si la construcción funciona, deberías ver un archivo .whl en la carpeta dist/.


5. Despliega nuevamente

Powershell:

            databricks bundle deploy --target dev


Ya ejecutado el comando, podremos ver el archivo .bundle en Databricks.


![image](https://github.com/user-attachments/assets/c8400704-7507-4f96-a72d-e4ad259fafd0)

Ingresamos .bundle, luego a dab, ahí encontraremos los siguientes archivos.

![image](https://github.com/user-attachments/assets/ccf6615f-f882-40e2-8474-7029c14f4c34)

Ahora, en Databricks creamos un trabajo.

![image](https://github.com/user-attachments/assets/26b016ee-cfb1-4af9-9b0b-e98e0c827ac5)

![image](https://github.com/user-attachments/assets/5e3911f5-6adb-4a6c-8add-c02fcc614f6e)

![image](https://github.com/user-attachments/assets/9c9bfd3e-016a-44c9-8c7c-8082f70a02cc)

Ahora, colocamos el nombre de la tarea 

Task name: ingestión

Y luego escogemos el path de la siguiente manera.


![image](https://github.com/user-attachments/assets/36904293-f7d3-4d54-a8bd-4ff1e53eaaa4)

![image](https://github.com/user-attachments/assets/18755257-6d1b-4a5a-b420-60438dc534f7)

![image](https://github.com/user-attachments/assets/63a0cf73-8b74-4477-bfd4-c105692023af)

![image](https://github.com/user-attachments/assets/60332cf9-5a90-4752-bf40-9bf50f3bd08a)

![image](https://github.com/user-attachments/assets/10328b45-550d-4b34-90e3-3b0612033097)

![image](https://github.com/user-attachments/assets/490f8274-d8fb-4263-b557-fdd082be5882)

Y finalmente le damos click en crear tarea.

![image](https://github.com/user-attachments/assets/a64ff25a-1405-483e-bd4a-d76c065a3092)

Ahora nos vamos a los tres puntitos de la parte superior derecha y selecionamos “edit as YAML”.

![image](https://github.com/user-attachments/assets/b1079613-ab80-4c21-b9ca-4181a86e1941)

![image](https://github.com/user-attachments/assets/95823953-2d6b-49e4-921c-42b0967b9e9f)

Ahora, copiamos todo el código y nos dirigimos a VSC

![image](https://github.com/user-attachments/assets/83be5660-ad7c-4851-a270-6edce5707223)

Ahora, nos dirigimos a recursos y creamos una carpeta llamado Jobs y dentro de ella, un archivo llamado job_dab.yml

![image](https://github.com/user-attachments/assets/8a08b8a6-ba0e-4ac2-b19f-d7cb902fd717)

Y guardamos el archivo.

Ahora, en notebook_path borramos parte del valor y lo sustituimos de la siguiente manera.


![image](https://github.com/user-attachments/assets/68a2ee48-446e-48e0-8565-f261ec065d47)

![image](https://github.com/user-attachments/assets/5f5b2164-63b6-4261-8a79-e6b9fb9fdbcd)

Bien, ahora nos dirigimos a la terminal y ejecutamos el siguiente código.

Código:

        databricks bundle deploy --target dev


ahora, podremos ver en Databricks el archivo de Jobs.


![image](https://github.com/user-attachments/assets/fadb9271-7d06-44a6-9aac-af2e7b9216a0)

Editamos esta parte

![image](https://github.com/user-attachments/assets/30efb656-da40-4ad4-87d8-6a50b3fd2bba)

Luego, ejecutamos en la terminal el siguiente código.

Código: 

        databricks bundle deploy --target dev


![image](https://github.com/user-attachments/assets/52b7ab31-e233-431b-bedc-d4949e15cd03)

Ahora, crearemos un cuderno más en src\notebooks.

Notebook2

Codigo:

        print('Hello World')
        print('This is a sample Python script.')


![image](https://github.com/user-attachments/assets/26f7e955-0791-4c28-a68d-6bf20015edfd)

Luego, en la terminal ejecutamos el deployment.

Código:

        databricks bundle deploy --target dev


![image](https://github.com/user-attachments/assets/5236a6a2-6218-406c-959b-c2835fa6be4d)

Ahora, vamos a Jobs & Pipelines y eliminamos el job_dab.

Luego, regresamos a la terminal 

Código:

        databricks bundle summary --target prod


código:

       databricks bundle validate --target prod


![image](https://github.com/user-attachments/assets/1ea0c9fb-34c4-4125-bc7a-814827bac837)

Código:

       databricks bundle prod --target prod


![image](https://github.com/user-attachments/assets/47111d36-854d-4e5a-8a07-8dc1be405c22)

**Ojo:** antes de ejecutar deploy verifica que en tu archivo Databricks.yml  en la parte de incluide estén estos dos recursos.

![image](https://github.com/user-attachments/assets/2ffabf84-11ce-4263-9289-cc3909ffb782)

Luego ejecuta el siguiente código.

Código:

        databricks bundle deploy --target prod


![image](https://github.com/user-attachments/assets/cabf6c18-5e65-4f9c-9eae-d3eb1d7c1638)

Luego, verificamos en Databricks que nuevamente aparezca el job_dab que eliminamos al inicio.

![image](https://github.com/user-attachments/assets/51e2a89f-33d9-47e3-b763-79b91d78ccb0)

![image](https://github.com/user-attachments/assets/77af199d-9f57-448b-8c93-509af75f3c29)

Ahora, en Databricks, nos vamos a la esquina superior derecha en tu logo y hacemis click y, en la ventana emergente seleccionamos setting.

![image](https://github.com/user-attachments/assets/68b314df-8499-4b74-a0b8-59365645f1c1)

Luego, hacemos click en Linked accounts.

![image](https://github.com/user-attachments/assets/845a40a3-7ecf-4db0-a745-baa975261a1e)

Hacemos click en Add Git credencial

![image](https://github.com/user-attachments/assets/52a9bc13-f7dc-40ee-bb36-a5d29bd5ef6e)

Eliminamos la fecha y hora, luego hacemos click en link

![image](https://github.com/user-attachments/assets/dac073ac-bdf4-43cb-86e2-8e35533cfa07)

Luego autorizamos.

![image](https://github.com/user-attachments/assets/a02fba72-4a9b-4cae-972c-e80ef169da32)

![image](https://github.com/user-attachments/assets/1d202bf8-2559-4969-86b4-8d39a167967a)

Ahora, nos vamos a workspace y creamos una carpeta Git.

![image](https://github.com/user-attachments/assets/3067b732-1978-48c7-8e7e-473311376da1)

Luego, vas a tu GitHub y creas un nuevo repositorio con el nombre de tu conveniencia, en mi caso Databricks Asset Bundles CI/CD.

Ahora, en code copia el http generado.


![image](https://github.com/user-attachments/assets/1d7dba08-399b-4930-a4ed-8d639ec5e850)

Luego, lo pegas en el recuadro de la creación del archivo Git de Databricks, y damos click en crear archivo Git.

![image](https://github.com/user-attachments/assets/c07573ed-a9a1-4d63-b995-0e56a6c4c0af)

Ahora, veras generado el archivo en Databricks.

![image](https://github.com/user-attachments/assets/aa15caf7-f923-467b-9ac2-633aa123a034)

Ahora, hacemos click en git.

![image](https://github.com/user-attachments/assets/b5bb8c84-7acd-46ac-802f-11647b0016d5)

Luego creamos una rama característica.

![image](https://github.com/user-attachments/assets/035f8882-84ed-4320-b2fc-3da0b6ba7520)

![image](https://github.com/user-attachments/assets/ebb5ca14-1726-427e-b263-2dc4cb9ece6d)

Si es la primera vez que ejecutas esto, es muy probable que salga este error.

Y solo debes dar click en la url y dar el permiso.


![image](https://github.com/user-attachments/assets/3c68cebf-3b88-4933-93b9-8e1eae5a9ddf)

![image](https://github.com/user-attachments/assets/f62afe50-00c0-4606-ba8e-e8f786dfda8f)

![image](https://github.com/user-attachments/assets/1c6f1235-4876-4f21-82e5-f87505c172f9)

![image](https://github.com/user-attachments/assets/fbe7ef21-d90f-4002-8b13-172e51a300fc)

Ahora, regresamos a Databricks y creamos un notebook.

![image](https://github.com/user-attachments/assets/d473aec3-d812-4395-a2d3-415e1896bea7)

Luego de crear el notebook, entramos al servidor y activamos web terminal de la siguiente manera.

![image](https://github.com/user-attachments/assets/495b000f-5702-4290-9a54-bdc863a7f2cd)

![image](https://github.com/user-attachments/assets/00144da8-ae17-485a-8a58-2af243074074)

Ahora, en la terminal tendremos que iniciar el Databricks bundle

Código:

        Databricks bundle init

Luego en la primera consulta damos enter y luego agregamos el nombre del proyecto en este caso dabproject.


![image](https://github.com/user-attachments/assets/5bc2559f-57b2-4ba1-8191-b5be84e31d2b)

Para las otras consultas, le damos si o yes a todo solo con presionar enter.

![image](https://github.com/user-attachments/assets/a8fd14b1-8a71-4d13-955e-6fed7719f7d6)

Luego, ingresamos al proyecto creado.

Código:

        cd dabproject

ahora, en los archivos que se creo con el proyecto, vaciamos los archivos de resources porque solo son de ejemplo y no lo necesitamos. Así como también, del archivo src que queden limpios.

Luego, en el archivo Databricks.yml eliminamos los artefactos.


![image](https://github.com/user-attachments/assets/77bf8d5f-a7cd-4c7b-bd43-93aff6b76d4f)

En este archivo, fíjate que en include haya los 2 resources o sino tendrás problemas mas adelante. En caso de que no lo tuvieras agrégalo manualmente.

![image](https://github.com/user-attachments/assets/b50b8d3b-55d2-45b2-93bb-35880db75a82)

Ahora, cambiamos el host del deployment. Para ello abrimos un duplicado de la pestaña de Databricks y nos dirigimos a SQL Warehouse y luego a serverless.

![image](https://github.com/user-attachments/assets/d902fd73-5b7a-4e16-9502-2f6c7542ac03)

![image](https://github.com/user-attachments/assets/4a5d916a-98de-438f-bfce-14a65d3a9800)

Aquí copiamos el server hostname y lo pegamos en el host de deployment y production del archivo Databricks.yml 

![image](https://github.com/user-attachments/assets/1d478b61-2aa7-457a-9a0a-d185032373b5)

Luego, hacemos click aquí.

![image](https://github.com/user-attachments/assets/81bb3e6b-26a6-4aa0-86c8-813137a9b26b)

Ahora, nos vamos a la carpeta src y creamos una carpeta llamado notebooks

![image](https://github.com/user-attachments/assets/b292f2a9-756c-4e90-810a-f6e8b0cc76c2)

Y dentro de ella creamos un cuaderno o notebook llamado ingestión.

![image](https://github.com/user-attachments/assets/7d280784-fc14-40ff-a0c6-b7fa9c1eb9c5)

Probamos si todo marcha bien y ejecutamos la siguiente consulta.

Sql:

     SELECT * FROM asset_bundles.information_schema.columns


![image](https://github.com/user-attachments/assets/a2bdfa07-5bed-43a8-87c3-6f90e87a9403)

Haremos ahora una estructura dinámica y la creación de una arquitectura medallón.

Código:

        dbutils.widgets.text(‘catalog_name’, ‘ ’)

ahí veras como genera un recuadro llamado catalog_name en la parte superior.


![image](https://github.com/user-attachments/assets/37aaefeb-7182-4f2b-9f09-1281a82b5f94)

Luego, creamos otra línea de código abajo con el siguiente código y ejecutamos.

Código:

        catalog_name = dbutils.widgets.get('catalog_name')


![image](https://github.com/user-attachments/assets/c303c757-73c3-4cb5-9ac3-92fa6e8cc84f)

Luego, con el siguiente código haremos un llamado de forma dinámica al catálogo asste_bundles.

Código:

        spark.sql(f'SELECT * FROM {catalog_name}.information_schema.columns')


![image](https://github.com/user-attachments/assets/7d1962d4-bbbf-4e42-8ec1-301879a93ffe)

Luego ejecutamos.

![image](https://github.com/user-attachments/assets/93e5c041-e4cd-475d-8643-17a7bfd6ad4c)

Y ahora los almacenamos en un dataframe.

Código:

        df = spark.sql(f'SELECT * FROM {catalog_name}.information_schema.columns')
        display(df)


![image](https://github.com/user-attachments/assets/6e7210ef-c4d8-4ba1-be78-bae485780d35)

Ahora, crearemos un trabajo (Job).

![image](https://github.com/user-attachments/assets/496bd9d1-6b7f-4e9c-a409-476f41618515)

![image](https://github.com/user-attachments/assets/baed9c8a-0598-4669-a309-7e10e5529fce)

Al notebook lo llamamos ingestión y luego ubicamos su ruta(path)

![image](https://github.com/user-attachments/assets/c6670008-085e-44e4-ac4b-941b0a11e546)

![image](https://github.com/user-attachments/assets/49fc5f76-ca2e-479e-b9d8-ebd5ffaba01a)

![image](https://github.com/user-attachments/assets/0a06006f-70f0-4ee8-a247-74b64ea3d81e)

Y confirmamos.

Luego, configuramos los parámetros.


![image](https://github.com/user-attachments/assets/c2148f13-c600-4f2a-972f-3086f0e061b2)



![image](https://github.com/user-attachments/assets/b061c586-2fc2-4fbb-b446-92fd54e94601)

Y creamos el trabajo (create task) y, cambiamos el nombre el nombre del trabajo general para su mejor identificación.

![image](https://github.com/user-attachments/assets/48b400c7-918d-4e22-82b4-be761953554e)

![image](https://github.com/user-attachments/assets/5552d7dd-307d-46d0-befd-8420a8a54169)

Ahora, nos vamos a la carpeta resources de Databricks y dentro de ella creamos una carpeta llamada Jobs.

![image](https://github.com/user-attachments/assets/76004627-7ce0-488f-8c00-633294a67107)

![image](https://github.com/user-attachments/assets/cc7eb48f-9e5d-4367-818a-34fc37879bc6)

Y dentro de la carpeta Jobs crearemos un file llamado job.yml

![image](https://github.com/user-attachments/assets/0e9ce8e7-2b3c-4d09-a218-cd212b4a46c4)

Luego nos vamos a Jobs & Pipeline al archivo ingestion_ab y luego a task y, copiamos todo el código YML y lo pondremos en el archivo job.yml de Databricks.

![image](https://github.com/user-attachments/assets/d9c24a4c-ffdc-491b-80e8-9f94175ddf52)

![image](https://github.com/user-attachments/assets/885875a6-d1f0-485c-9b4c-1808c6015943)

![image](https://github.com/user-attachments/assets/043c5137-ce78-4118-963f-c73655a74f36)

Código:

        resources:
         jobs:
            ingestion_ab:
              name: ingestion_ab
              tasks:
                - task_key: ingestion
                  notebook_task:
                    notebook_path: /Workspace/Users/allgoher007@gmail.com/Databricks-Asset-Bundles-CI-CD/dabproject/src/notebooks/ingestion
                    base_parameters:
                      catalog_name: asset_bundles
                    source: WORKSPACE
              queue:
                enabled: true
              performance_target: PERFORMANCE_OPTIMIZED


Y luego lo pegamos en job.yml de Databricks 


Ahora, editamos el notebook_path, en el cual eliminamos parte de ruta hasta el src y, luego lo cambiaremos a un rumbo relativo.


![image](https://github.com/user-attachments/assets/a64d5992-9091-4503-8ecd-072f73611bd2)

Y pondremos ../.. y al final del path o ruta le pondremos  .ipynb

![image](https://github.com/user-attachments/assets/bf738224-8cdd-46ed-b03c-d27262c41754)

Ahora, crearemos una variables ambientales en el archivo Databricks.yml. entonces crearemos una carpeta de variables en resources

![image](https://github.com/user-attachments/assets/069725d9-3750-4b49-a8a5-b082dd2e5154)

![image](https://github.com/user-attachments/assets/1a907b46-3801-454c-b15b-d80de026f0bb)

Ahora, dentro de ella creamos un file llamado variables.yml

![image](https://github.com/user-attachments/assets/8ffedbbe-8749-4fd2-93d2-ff045c79bff1)

![image](https://github.com/user-attachments/assets/35772d44-d638-41ec-8db4-7fd62d469e2b)

Y pasamos el siguiente código.

Código:

        variables:
          catalog_name:
            default: asset_bundles

luego, modificamos el archivo job.yml para que acepte las variables.

Cambiamos esto:


![image](https://github.com/user-attachments/assets/8c975217-7976-4921-9fa4-be8170d30627)

Por esto:

![image](https://github.com/user-attachments/assets/89a4698b-2eb1-4769-98ff-2c62be8ec4f4)

De esta manera, cambiamos las variables ambientales.

Ahora veremos las tablas delta, si requieres mas información, en tu navegador buscar tablas deltas o declarative pipelines que es lo más moderno.

Para comenzar, nos vamos a Jobs & Pipelines y creamos un ETL pipeline.


![image](https://github.com/user-attachments/assets/dfed8d85-8507-4cd5-849f-71a5423dcc8d)

Luego configuramos el catalogo y el esquema de la siguiente manera.

![image](https://github.com/user-attachments/assets/b306eec0-5698-4ca0-af4c-4ed975a4bcaf)

Cambiamos el nombre del ETL principal por demopipeline y, luego pasamos el siguiente código.

Código:

        import dlt

        @dlt.table
        def transformed():
            return spark.range(10)

y luego ejecutamos en seco (Run Dry)


![image](https://github.com/user-attachments/assets/0357fb67-39d7-4c2d-b6d3-bcc1744d573e)

![image](https://github.com/user-attachments/assets/58a91004-b3a1-4563-9c16-cb9a9a5a5141)

![image](https://github.com/user-attachments/assets/aa24b93e-0df3-458b-8155-80efd76c3bf2)

Ahora, moveremos la carpeta raíz a los usuarios

![image](https://github.com/user-attachments/assets/a2999f3f-855d-47e8-9f5a-ee6df0c7618d)

![image](https://github.com/user-attachments/assets/762ce207-c90a-464f-ad16-ccaca239afcb)

![image](https://github.com/user-attachments/assets/04c8ea0f-2056-4e8d-8202-4fa75ebb92fd)

![image](https://github.com/user-attachments/assets/609529e7-6d7a-4c42-9748-69f17f709d42)

![image](https://github.com/user-attachments/assets/b2f7d7f4-b5e7-4150-966d-8405d022086a)

![image](https://github.com/user-attachments/assets/f0c3c498-9921-4b4d-8b24-32aceabb1ad3)

Luego, hacemos click en mas + y , creamos el file pipeline.

![image](https://github.com/user-attachments/assets/915db958-73fb-491d-bc5f-eced8aeaab71)

Y por ultimo hacemos click en Move.

![image]()

![image]()

![image]()

![image]()

![image]()
