# AzureLab05
Manual sobre como Implementar conectividad entre sitios a través de Azure y PowerShell 

Arquitectura del diagrama:

![](img/img1.png)

## **Paso 1: Aprovisionar el entorno de trabajo**

En esta tarea, implementará tres máquinas virtuales, cada una en una red virtual independiente, dos de ellas en la misma región de Azure y la tercera en otra región de Azure.

1. Inicie sesión en el [portal de Azure](https://portal.azure.com/) .

2. A continuación abrimos nuestro terminal (PowerShell) en Windows. En caso de que no lo tengas instalado, se puede hacer dentro de la plataforma de AZURE a través de CloudShell.

3. Iniciamos conexión con el comando connect-azaccount

4. Ahora copiamos la ruta de los archivos JSON ,  **Allfiles\Labs\05\az104-05-vnetvm-loop-template.json** y **\ Allfiles\Labs\05\az104-05-vnetvm-loop-parameters.json** y escribimos el comando quedando algo parecido a esto: *cd "C:\Users\Usuario\Desktop\trabajo cloud\Labs\05"*

5. Establecemos los valores para crear así el primer grupo de recursos:

   Las dos primeras redes virtuales y un par de máquinas virtuales se implementarán en [Azure_region_1]. La tercera red virtual y la tercera máquina virtual se implementarán en el mismo grupo de recursos pero en otro [Azure_region_2]

   ![](img/img2.png)

6. Y así con los demás:

   ![](img/img3.png)

Para identificar las regiones de Azure, desde una sesión de PowerShell en Cloud Shell, ejecute **(Get-AzLocation).Location**

6. Ejecutamos lo siguiente para crear las tres redes virtuales e implementar máquinas virtuales en ellas usando la plantilla y los archivos de parámetros que cargamos anteriormente:

   New-AzResourceGroupDeployment `

    `-ResourceGroupName $rgName `

    `-TemplateFile $HOME/az104-05-vnetvm-loop-template.json `

    `-TemplateParameterFile $HOME/az104-05-vnetvm-loop-parameters.json  `

   `-location1 $location1` 

   -location2 $location2

   

   ## Paso 2: Configurar el emparejamiento (peering) de las LAN y WAN

   1. En Azure Portal, busque y seleccione **Redes virtuales** .
   2. Revise las redes virtuales que creó en la tarea anterior y verifique que las dos primeras estén ubicadas en la misma región de Azure y la tercera en una región de Azure diferente.
   3. En la lista de redes virtuales, haga clic en **az104-05-vnet0** .

