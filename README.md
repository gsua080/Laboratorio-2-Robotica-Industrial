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

### Calibración

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
### Código en RAPID 
La práctica fue desarrollada utilizando un módulo programado en RAPID, el lenguaje propio de los robots ABB. Este codigo implementado se encarga de gestionar por completo el funcionamiento del robot, abarcando tanto sus desplazamientos como el manejo de la herramienta de dibujo.
### Vídeo


