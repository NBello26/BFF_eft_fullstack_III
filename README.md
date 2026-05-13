# 🌉 BFF (Backend For Frontend) - Sistema de Gestión de Mascotas

Este repositorio contiene el microservicio **BFF (Backend For Frontend)**, desarrollado en Spring Boot. Actúa como el puente principal entre la interfaz de usuario (Frontend) y el ecosistema de microservicios internos. Su función principal es recibir las peticiones del Frontend, descubrir las IPs dinámicas de los microservicios de negocio a través de Eureka y enrutar las solicitudes de forma segura utilizando OpenFeign.

## 🚀 Arquitectura y Prácticas DevOps

Este servicio es una pieza clave en la seguridad y eficiencia de la red de la aplicación. Al operar detrás de un Reverse Proxy, el BFF asegura que la comunicación con los microservicios internos nunca sea expuesta a internet.

El despliegue está completamente automatizado mediante un pipeline de **CI/CD** con GitHub Actions:
1. Compila el código fuente de Java/Spring Boot.
2. Construye la imagen Docker del BFF.
3. Sube la imagen a **Amazon Elastic Container Registry (ECR)**.
4. Ejecuta comandos de forma remota y segura vía **AWS Systems Manager (SSM)** para desplegar el contenedor en la instancia EC2 designada, inyectando las variables de entorno necesarias (como la URL de Eureka).

### 🌐 Ecosistema de Infraestructura en AWS
Este microservicio reside en la capa intermedia de la arquitectura alojada en AWS:

* **Nodo Web:** ApiGateway y Frontend
* **Nodo Back 1:** Eureka Server y **BFF** (Este repositorio) 📍
* **Nodo Back 2:** Microservicios de Mascotas y Usuarios
* **Nodo Back 3:** Microservicios de Geolocalización y Notificaciones
* **Nodo Back 4:** Motor de Coincidencias
* **Base de Datos:** SanosDB (PostgreSQL)

## 🛠️ Tecnologías Principales

* **Framework:** Java 17 / Spring Boot 3
* **Cloud Native:** Spring Cloud (Netflix Eureka Client, OpenFeign)
* **Contenedores:** Docker
* **CI/CD:** GitHub Actions
* **Infraestructura AWS:** EC2, ECR, SSM, IAM

## ⚙️ Descubrimiento de Servicios Dinámico

Para mantener una infraestructura resiliente, el BFF **no utiliza IPs estáticas** para comunicarse con los demás microservicios. 

En su lugar, está configurado como un cliente de **Eureka**. Cuando el Frontend solicita información (por ejemplo, el detalle de una mascota), el BFF utiliza **OpenFeign** para consultar el registro de Eureka por el nombre del servicio (`MS-GESTION-MASCOTAS`). Eureka le devuelve la IP privada actual de la instancia EC2 correspondiente, permitiendo que la petición HTTP se resuelva internamente dentro de la red de AWS.

## 📦 Repositorios del Proyecto

Explora el resto de la infraestructura y microservicios de este ecosistema:

**Frontend y Puertas de Enlace**
* 🌐 [Frontend_eft_fullstack_III](https://github.com/NBello26/Frontend_eft_fullstack_III)
* 🚪 [ApiGateway_eft_fullstack_III](https://github.com/NBello26/ApiGateway_eft_fullstack_III)
* 🌉 [BFF_eft_fullstack_III](https://github.com/NBello26/BFF_eft_fullstack_III) *(Estás aquí)*

**Descubrimiento y Base de Datos**
* 🧭 [Eureka_eft_fullstack_III](https://github.com/NBello26/Eureka_eft_fullstack_III)
* 🗄️ [BD_eft_fullstack_III](https://github.com/NBello26/BD_eft_fullstack_III)

**Microservicios de Negocio**
* 🐾 [Reporte_Mascota_eft_fullstack_III](https://github.com/NBello26/Reporte_Mascota_eft_fullstack_III)
* 👤 [Usuarios_eft_fullstack_III](https://github.com/NBello26/Usuarios_eft_fullstack_III)
* 📍 [Geolocalizacion_eft_fullstack_III](https://github.com/NBello26/Geolocalizacion_eft_fullstack_III)
* 🔔 [Notificaciones_eft_fullstack_III](https://github.com/NBello26/Notificaciones_eft_fullstack_III)
* 🧩 [Coincidencias_eft_fullstack_III](https://github.com/NBello26/Coincidencias_eft_fullstack_III)

---
*Desarrollado como parte del proyecto final de integración de arquitectura DevOps.*
