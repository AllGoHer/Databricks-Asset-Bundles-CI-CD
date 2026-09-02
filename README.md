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
