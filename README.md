# Práctica DevOps - Despliegue en Servidor

<div align="center">

  [![Node.js](https://img.shields.io/badge/nodejs-5FA04E?style=for-the-badge&logo=nodedotjs&logoColor=white)](https://nodejs.org/en)
  [![Express](https://img.shields.io/badge/express-000000?style=for-the-badge&logo=express&logoColor=white)](https://expressjs.com/)
  [![MongoDB](https://img.shields.io/badge/mongodb-47A248?style=for-the-badge&logo=mongodb&logoColor=white)](https://www.mongodb.com/)
  [![Nginx](https://img.shields.io/badge/nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)](https://nginx.org/)
  [![Ubuntu](https://img.shields.io/badge/ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)](https://ubuntu.com/)

</div>

Práctica del módulo de **Configuración de servidores y despliegue de aplicaciones** del Bootcamp Desarrollo Web FullStack en KeepCoding.

Consiste en desplegar la aplicación [Nodepop](https://github.com/Aratea10/nodepop-ssr-ejs) en un servidor AWS EC2 con la arquitectura requerida.

---

## 🌐 URL de la aplicación desplegada

[http://35.170.15.75](http://35.170.15.75)

> La cabecera personalizada `X-Owner: Aratea10` se puede verificar con:
> ```bash
> curl -I http://35.170.15.75/public/stylesheets/login.css
>```

---

## 🏗️ Arquitectura

| Componente | Tecnología | Descripción |
| --- | --- | --- |
| **Servidor** | AWS EC2 (t3.micro) | Ubuntu 24.04 LTS en us-east-1 |
| **IP** | Elastic IP | 35.170.15.75 (IP estática) |
| **App** | Node.js v20 + Express | Aplicación Nodepop (SSR con EJS) |
| **BBDD** | MongoDB 7.0 | Base de datos para usuarios y productos |
| **Proxy inverso** | Nginx | Recibe peticiones HTTP y las deriva a Node |
| **Estáticos** | Nginx | Sirve archivos estáticos con cabecera `X-Owner` |
| **Gestor de procesos** | Supervisor | Mantiene Node en ejecución y reinicia en el startup |

---

## 📋 Requisitos cumplidos (Ejercicio 1)

- ✅ Node como servidor de aplicación con **Supervisor** como gestor de procesos
- ✅ La aplicación se reinicia automáticamente al arrancar el servidor (autostart)
- ✅ **Nginx** como proxy inverso que recibe las peticiones HTTP y las deriva a Node
- ✅ Archivos estáticos servidos por **Nginx** (no por Node)
- ✅ Cabecera personalizada `X-Owner: Aratea10` en los archivos estáticos

---

## 📁 Estructura del repositorio

````text
devops-practice/
├── [README.md](http://README.md)

└── exercise-1/
    ├── nginx/
    │   └── nodepop.conf          # Configuración de Nginx
    └── supervisor/
        └── nodepop.conf          # Configuración de Supervisor
````

## 🛠️ Configuración del servidor

### Prerrequisitos instalados

- Node.js v20.20.2 (via NVM)
- MongoDB 7.0
- Nginx 1.24
- Supervisor 4.x

### Rutas en el servidor

| Ruta | Descripción |
| --- | --- |
| `/home/ubuntu/nodepop` | Código de la aplicación Nodepop |
| `/etc/nginx/sites-available/nodepop` | Configuración de Nginx |
| `/etc/supervisor/conf.d/nodepop.conf` | Configuración de Supervisor |
| `/var/log/nodepop.out.log` | Logs de stdout |
| `/var/log/nodepop.err.log` | Logs de errores |

---

## 🤝 Contribución

Si quieres mejorar el proyecto:

1. Haz fork del repositorio.
2. Crea una rama: `git checkout -b feature/mi-mejora`.
3. Haz commits claros siguiendo Conventional Commits.
4. Haz push y abre un Pull Request describiendo los cambios.

---

## 📄 Licencia

Este proyecto se entrega con **Licencia MIT**.

---

## 👩‍💻 Autora

**Sara Gallego Méndez** — Estudiante Bootcamp Desarrollo Web FullStack en [KeepCoding](https://keepcoding.io/).
