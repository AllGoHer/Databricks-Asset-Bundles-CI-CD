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
