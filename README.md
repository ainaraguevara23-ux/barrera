# barrera# mart Barrier — Sistema de Barrera Automática para Estacionamiento

##  Sobre el Proyecto
Sistema de control de acceso vehicular automatizado desarrollado sobre Arduino UNO. Su objetivo principal es simular el funcionamiento de una barrera de estacionamiento inteligente que detecta la presencia de vehículos mediante un sensor ultrasónico, acciona un motor para abrir el paso de manera automática y utiliza indicadores lumínicos LED para mostrar el estado actual del sistema.

---

## Integrantes del Equipo
* **Ainara Guevara** (Scrum Master)
* **Jazmín Banes** (Developer / Hardware)
* **Ignacio Demo** (Developer / Software)

---

##  Historia de Usuario
* **Como** conductor de un vehículo, 
* **quiero** que la barrera del estacionamiento se abra automáticamente al acercarme y se cierre al pasar, 
* **para** agilizar el ingreso al predio de forma segura y sin necesidad de manipulación manual.

---

## Requerimientos Funcionales
1. **RF01 - Detección de Vehículos:** El sensor ultrasónico mide continuamente la distancia y detecta un vehículo si se encuentra a una distancia menor o igual a 15 cm.
2. **RF02 - Apertura Automática:** Al detectar presencia, el servomotor gira a 90° levantando la pluma de la barrera.
3. **RF03 - Señalización Lumínica:** Durante la apertura, el LED verde se enciende y el LED rojo se apaga.
4. **RF04 - Cierre Automático con Retardo:** La barrera se mantiene abierta durante 3 segundos antes de volver a la posición de cierre (0°).
5. **RF05 - Estado de Reposo:** En ausencia de vehículos, la barrera permanece cerrada (0°) con el LED rojo encendido y el verde apagado.

---

##  Requerimientos No Funcionales
1. **RNF01 - Tiempo de Respuesta:** La reacción del sensor y la apertura del motor ocurren en menos de 500 ms tras la detección.
2. **RNF02 - Visibilidad:** Los indicadores LED deben ser claramente distinguibles a una distancia de al menos 3 metros.
3. **RNF03 - Mantenibilidad del Código:** El software está estructurado en C++ de manera modular y comentado para facilitar futuras modificaciones.
4. **RNF04 - Simulabilidad:** El circuito es 100% funcional y replicable tanto en software como en hardware físico.
5. **RNF05 - Eficiencia Energética:** Opera con un voltaje estándar de 5V adaptado a microcontroladores educativos.

---

##  Componentes y Precios

| Componente | Cantidad | Precio Estimado (ARS) |
| :--- | :---: | :---: |
| Placa Arduino UNO R3 + Cable USB | 1 | $19.950 |
| Sensor Ultrasónico HC-SR04 | 1 | $2.835 |
| Servomotor SG90 (9g) | 1 | $4.085 |
| Protoboard 400 puntos | 1 | $4.500 |
| LEDs (Rojo y Verde 5mm) | 2 | $500 |
| Resistencias 220 Ω (1/4W) | 2 | $300 |
| Jumper Wires (Cables) | 1 pack | $1.730 |
| **TOTAL ESTIMADO** | | **$33.900** |

---

##  Conexiones y Mapeo de Pines

El circuito utiliza entradas y salidas digitales y analógicas/PWM de la placa Arduino de la siguiente manera:

* **Sensor Ultrasónico HC-SR04 (Digital / Disparo y Eco):**
  * `VCC` ➔ Pin de 5V de Arduino
  * `Trig` ➔ Pin Digital 9 (Salida de disparo de pulso)
  * `Echo` ➔ Pin Digital 8 (Entrada de recepción de eco)
  * `GND` ➔ Pin GND de Arduino

* **Servomotor SG90 (Salida Digital PWM):**
  * `Señal (Naranja/Blanco)` ➔ Pin Digital 10 (Control PWM de posición)
  * `VCC (Rojo)` ➔ Pin de 5V
  * `GND (Café/Negro)` ➔ Pin GND

* **Indicadores LED (Salidas Digitales):**
  * `LED Rojo` ➔ Pin Digital 5 (con resistencia de protección de 220 Ω)
  * `LED Verde` ➔ Pin Digital 6 (con resistencia de protección de 220 Ω)

---

## Diagrama de Flujo del Sistema

```mermaid
graph TD
    A[Inicio: setup] --> B[Inicializar Servo a 0°]
    B --> C[LED Rojo ENCENDIDO / LED Verde APAGADO]
    C --> D[Emitir pulso ultrasónico Trig]
    D --> E[Medir tiempo de respuesta Echo]
    E --> F[Calcular distancia en cm]
    F --> G{¿Distancia <= 15 cm?}
    G -- Sí --> H[LED Rojo OFF / LED Verde ON]
    H --> I[Girar Servo a 90° - Abrir Barrera]
    I --> J[Esperar 3 segundos]
    J --> D
    G -- No --> K[Girar Servo a 0° - Cerrar Barrera]
    K --> C

