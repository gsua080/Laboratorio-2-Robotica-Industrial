# Laboratorio-2-Robotica-Industrial


**Juliana Gongora Rasmussen**


_Ingeniería Mecatrónica_

Correo: jugongorar@unal.edu.co

---


**Gerhaldine Alejandra Suárez Bernal**
  
  _Ingeniería Mecatrónica_

Correo: gesuarezb@unal.edu.co

Este laboratorio tiene como objetivo la programación dek robot ABB IRB 140 con el fin de realizar la decoración de una torta virtual, en la que se escriban los nombres de cada uno de los integrantes del grupo, además de incluir un diseño personalizado en la parte inferior.

## Procedimiento
### Descripción de la Solución Planteada
Se implementó el movimiento del robot ABB IRB 140 mediante un programa en lenguaje RAPID previamente desarrollado en RobotStudio. Utilizando un conjunto de instrucciones definidas, así como la configuración de trayectorias y parámetros específicos, se buscó escribir los nombres de las integrantes del grupo, además de trazar una figura correspondiente al diseño del manipulador IRB 140.

### Diseño de herramienta
Se desarrolló el diseño de una herramienta para sostener un marcador delgado, compuesta por dos piezas ensamblables: una pieza de soporte y otra de encapsulamiento.
En su interior se integraron un resorte y el propio marcador, permitiendo un ajuste mecánico funcional.

La herramienta fue impresa en 3D utilizando filamento PLA, y se fabricaron varios prototipos para pruebas de ajuste, tolerancia y funcionalidad del mecanismo de sujeción.
![PHOTO-2025-06-15-21-43-35 6](https://github.com/user-attachments/assets/c3875a64-eeb7-476f-84e9-9f5601d0789a)
![PHOTO-2025-06-15-21-43-35 4](https://github.com/user-attachments/assets/d59ea6c6-7694-4f44-8a65-391367825876)

evidenciamos Problemas con el ajuste y la tolerancia asi que imprimimos otro
![PHOTO-2025-06-15-21-43-35 7](https://github.com/user-attachments/assets/d8ceafe2-a50b-4fa2-a7a8-380464b0f0cc)
![PHOTO-2025-06-15-21-43-35 3](https://github.com/user-attachments/assets/8896694a-f174-4fad-b2d1-dae528e35c07)

Luego notamos nuevamente problemas con las tolerancias dimensionales asi que realizamos otro montaje que lastimosamente se rompio debido a la equivocacio el la manipulacion de la pieza en la calibración 
![PHOTO-2025-06-13-08-06-54 2](https://github.com/user-attachments/assets/6aeeded3-d674-4129-91d2-809b1e15ad25)

El ensamble resultante es el siguiente :
![PHOTO-2025-06-15-21-43-36 6](https://github.com/user-attachments/assets/6b9d427d-4280-46fa-95fc-9bdd1b611193)

![PHOTO-2025-06-15-21-43-36](https://github.com/user-attachments/assets/11d1d845-628d-44bf-8d07-c0399e014b80)

### Calibración
Se realizo la calibración de la herramienta final obteniendo un error final de 6mm
**Herramienta:**

Para la herramienta, diseñamos un soporte que permitiera fijar un marcador al flange del robot IRB 140. Luego, hicimos el proceso de calibración directamente con el robot real, usando un objeto para marcar varios puntos con la punta del marcador. Esto nos permitió calcular el TCP (Tool Center Point) desde el controlador.

El objetivo era que el robot repitiera bien la posición del marcador, y que el cálculo del TCP fuera lo más preciso posible. Si al final del proceso el error era muy alto, era necesario repetir hasta que el resultado fuera aceptable.

Después, en RobotStudio importamos el modelo CAD de la herramienta y comparamos el tooldata generado allí con el del robot real, para verificar que fueran similares.

**Workobject:**

El WorkObject es el sistema de coordenadas de la superficie sobre la cual se escribe o dibuja. Para calibrarlo, se usaron medidas reales tomadas desde el robot hacia la torta virtual (o la base de trabajo), y las ingresamos manualmente en RobotStudio.

Luego se creaba un nuevo WorkObject con esos datos y se usaba durante toda la programación de trayectorias. Así se asegura de que los movimientos del robot coincidieran bien con la ubicación real del plano de trabajo.

### Diagrama de flujo de acciones del robot



---
```mermaid
flowchart TD
    A(["Inicio"]) --> C{"Esperar señal de inicio DI_01"}
    C -->|Sí| n1["Posicionarse en Home"]
    C -->|No| n2["Esperar señal de mantenimiento"]
    n1 --> n3["Encender luz indicadora DO_01"]
    n3 --> n4["Ejecutar trayectoria de dibujo"]
    n4 --> n5["Dibujo de nombres y figura"]
    n2 --> n6["Apagar luz DO_01"]
    n5 --> n7{"Esperar señal de mantenimiento DI_02"}
    n7 -->|Sí| n6
    n7 -->|No| n8(["Fin"])

    class n1,n2,n3,n4,n7 rounded
    class n7 diamond
```
### Plano de planta
### Descripción de las funciones utilizadas
##  Smart Components utilizados

En este proyecto se integraron los siguientes **Smart Components** en RobotStudio para simular el flujo del proceso automatizado:

---

###  `Linear_Mover`
Simula el movimiento lineal de una banda transportadora.

**Funciones principales:**
- Desplaza la pieza de trabajo en línea recta hasta la zona de manipulación del robot.

**Entradas digitales:**
- `di_01`: Activa el movimiento de la banda transportadora.

---

###  `Plane Sensor`
Detecta la presencia de una pieza cuando esta cruza un plano virtual.

**Funciones principales:**
- Emite una señal digital cuando la pieza llega al área de trabajo del robot.

**Salidas digitales:**
- `do_01`: Señal de detección activa (pieza lista para ser manipulada por el robot).

---
### Código en RAPID 
La práctica fue desarrollada utilizando un módulo programado en RAPID, el lenguaje propio de los robots ABB. Este codigo implementado se encarga de gestionar por completo el funcionamiento del robot, abarcando tanto sus desplazamientos como el manejo de la herramienta de dibujo.
### Vídeo


