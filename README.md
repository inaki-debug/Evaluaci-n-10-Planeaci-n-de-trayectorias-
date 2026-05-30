# Evaluaci-n-10-Planeaci-n-de-trayectorias-

En esta evaluación se realizó la planeación de una trayectoria a partir de una imágen de un rostro. Se marcaron varios puntos que delimitaban los bordes del rostro, marcando la forma, ojos, nariz boca y cabello. Se utilizó un controlador para el seguimiento de los puntos en orden.

Se utilizó un control Pure Pursuit el cual se sintonizó con los siguientes parámetros:

```
sampleTime = 0.1;              
tVec = 0:sampleTime:100000;

initPose = [226.6;238.2;2.35619]; 

controller.LookaheadDistance = 0.30;
controller.DesiredLinearVelocity = 1;
controller.MaxAngularVelocity = 100;
```

Se estableció este `sampleTime` para tener un buen tiempo de muestreo para cuando se hace la integración para calcular la posición del robot a partir de su velocidad. Se inicializó en el punto (226.6, 238.2) que fue el primer punto que se estableció al marcar el rostro con la lista de waypoints. El `LookaheadDistance` fue el adecuado debido a que los puntos al estar muy unidos, no fue necesario colocar un valor muy grande ya que gracias a esta variable, puede detectar el siguiente punto a una distancia considerable. La `MaxAngularVelocity` fue muy alta para que el robot pueda realizar giros más fuertes al momento que se requiera, permitiendo tener un dibujo fluido sin curvas pronunciadas. La `LinearVelocity` fue la adecuada para evitar tener oscilaciones pero que realice la trayectoria con un buen tiempo.

Se  eligió este tipo de controlador debido a que gracias a usar la lógica con un `LookaheadDistance` puede anticipar los movimientos que debe realizar para llegar al punto, haciendo que al momento en que se detecta la posición de este, apunte hacia el para una trayectoria más limpia sin giros bruscos. Esto tiene ventaja ante otros tipos de controlador, por ejemplo uno proporcional es reactivo al error del momento, haciendo que el robot pueda tener oscilaciones si no se anticipa a los cambios bruscos. O por ejemplo, un control a lazo abierto, no tiene anticipación ni reacciona correctamente al error, causando que no llegue al punto. 
