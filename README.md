# Sistema Tunomático

**Nombre:** Cristobal Martinez  
**Carrera:** Ingeniería Informática  
**Fecha:** 16 de mayo de 2025  

## 1 Descripción General del Sistema

El Sistema Tunomático es una solución digital para la gestión automatizada de turnos en entornos de atención al cliente  
Su objetivo es optimizar el flujo de atención permitiendo a los usuarios solicitar consultar o cancelar turnos desde una interfaz web mientras el personal de atención gestiona los turnos y la administración supervisa el sistema y genera reportes  
El sistema está diseñado con buenas prácticas de diseño orientado a objetos y aplica patrones de diseño para garantizar escalabilidad mantenimiento y modularidad  

---

## 2 Diagrama de Casos de Uso

![image](https://github.com/user-attachments/assets/11857783-5cc3-4297-9100-4a7d4c5725dd)


### Explicación y Justificación

- **Actores**  
  - Cliente solicita cancela consulta y visualiza turnos  
  - Punto de Atención atiende turnos llama al siguiente y puede reasignar turnos  
  - Administrador gestiona servicios configura el sistema y genera reportes  

- **Casos de uso principales**  
  - Solicitar Turno que incluye obligatoriamente la selección de un servicio usando relación <<include>>  
  - Atender Turno que puede extenderse a Reasignar Turno cuando es necesario atender en otro punto usando <<extend>>  
  - Visualizar Turnos usado tanto por clientes como por puntos de atención para monitorear el estado  
  - Notificaciones automáticas se disparan tras eventos clave como solicitar atender y llamar siguiente  

Este diagrama refleja la interacción clara y detallada entre usuarios y el sistema utilizando relaciones formales para mostrar dependencia y extensión de funcionalidades  

---

## 3 Diagrama de Clases

![image](https://github.com/user-attachments/assets/4af47496-ad0a-476e-9123-97025fadac40)


### Explicación Técnica y Patrones Aplicados

- **GestorTurnos** es un <<Singleton>> que controla toda la gestión de turnos y asegura una única instancia global  
- **Turno** representa cada turno con atributos como número estado y hora de asignación con relaciones con cliente y servicio  
- **Cliente** y **Servicio** modelan a los usuarios y los servicios disponibles con métodos para solicitar cancelar y consultar turnos  
- **PuntoAtencion** maneja la atención directa de turnos con funciones para llamar siguiente atender y reasignar turnos  
- **Notificador** es una interfaz implementada por **EmailAdapter** y **SMSAdapter** siguiendo el patrón <<Adapter>> para integrar distintos canales de notificación  
- **PlantillaTurno** es un <<Prototype>> que permite clonar turnos base para crear configuraciones predefinidas  
- **Administrador** gestiona servicios configura el sistema y genera reportes  

Las cardinalidades reflejan que un gestor tiene muchos turnos clientes y servicios  
Cada turno tiene un cliente y un servicio un cliente puede tener muchos turnos y un punto de atención atiende muchos turnos  
Se aplican principios SOLID como responsabilidad única apertura para extensión y sustitución de Liskov para herencia correcta  

---

## 4 Diagrama de Implementación

![image](https://github.com/user-attachments/assets/8417d8bc-ccd9-4011-a0d6-ce2937e83209)


### Explicación Técnica

El diagrama muestra la arquitectura física y los nodos que componen el sistema  

- **Nodo Cliente Web** contiene la interfaz que usan los clientes para interactuar con el sistema  
- **Nodo Punto de Atención** donde el personal de atención gestiona la atención de turnos mediante su interfaz  
- **Nodo Servidor Central** aloja el componente principal GestorTurnos implementado como <<Singleton>> junto con módulos especializados para turnos servicios y administración  
  El Controlador de Notificaciones implementa el patrón <<Adapter>> para integrar servicios externos de mensajería  
- **Nodo Base de Datos** almacena persistentemente turnos servicios clientes y configuraciones  
- **Nodo Servicio de Notificaciones** servicio externo que maneja el envío real de mensajes conectado a través del adaptador  

Las conexiones muestran flujos de interacción entre componentes y respetan la separación de responsabilidades facilitando la escalabilidad y mantenimiento del sistema  

---

## 5 Reflexiones Finales

El modelado del Sistema Tunomático ayudó a crear una solución clara ordenada y adaptable que cumple con lo que se pedía
Los patrones de diseño que usamos ayudaron a mantener el código bien organizado y a conectar servicios externos sin problemas
Los patrones Singleton Prototype y Adapter dieron ventajas como tener control centralizado crear objetos fácilmente y enviar notificaciones de forma flexible
Recomiendo seguir mejorando el sistema con pruebas y agregar más patrones en futuras versiones
