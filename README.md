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


![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()

![image]()
