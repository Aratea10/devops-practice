# Práctica DevOps - Despliegue en Servidor

<div align="center">

  [![Node.js](https://img.shields.io/badge/nodejs-5FA04E?style=for-the-badge&logo=nodedotjs&logoColor=white)](https://nodejs.org/en)
  [![Express](https://img.shields.io/badge/express-000000?style=for-the-badge&logo=express&logoColor=white)](https://expressjs.com/)
  [![MongoDB](https://img.shields.io/badge/mongodb-47A248?style=for-the-badge&logo=mongodb&logoColor=white)](https://www.mongodb.com/)
  [![Next.js](https://img.shields.io/badge/next%20js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)](https://nextjs.org/)
  [![PostgreSQL](https://img.shields.io/badge/postgresql-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
  [![Nginx](https://img.shields.io/badge/nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)](https://nginx.org/)
  [![AWS](https://img.shields.io/badge/AWS-FF9900?style=for-the-badge&logo=amazonec2&logoColor=white)](https://aws.amazon.com/)
  [![Ubuntu](https://img.shields.io/badge/ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)](https://ubuntu.com/)
  [![Docker](https://img.shields.io/badge/docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)


</div>

Práctica del módulo de **Configuración de servidores y despliegue de aplicaciones** del Bootcamp Desarrollo Web FullStack en [KeepCoding](https://keepcoding.io/).

Consiste en desplegar aplicaciones web en un servidor AWS EC2 con la arquitectura requerida.

---

## 🌐 URL de la aplicación desplegada

| Ejercicio | App | URL |
| --- | --- | --- |
| **Ejercicio 1** | Nodepop (Backend Node) | **http://aratea.duckdns.org** |
| **Ejercicio 2** | Marketplace (React Avanzado / Next.js) | **http://35.170.15.75** |

---

### Archivo estático servido por Nginx con cabecera X-Owner

**http://aratea.duckdns.org/public/stylesheets/login.css**

> Verificar cabecera `X-Owner: Aratea10`:
> ```bash
> curl -I http://aratea.duckdns.org/public/stylesheets/login.css
> ```

---

## 🏗️ Arquitectura

| Componente | Tecnología | Descripción |
| --- | --- | --- |
| **Servidor** | AWS EC2 (t3.micro) | Ubuntu 24.04 LTS en us-east-1 |
| **IP** | Elastic IP | 35.170.15.75 (IP estática) |
| **Dominio** | DuckDNS | aratea.duckdns.org |
| **Nodepop** | Node.js v20 + Express | App de anuncios SSR con EJS (puerto 3000) |
| **Marketplace** | Next.js 16 + React 19 | App de anuncios fullstack (puerto 4000) |
| **BBDD Nodepop** | MongoDB 7.0 | Base de datos para usuarios y productos |
| **BBDD Marketplace** | PostgreSQL 17 (Docker) | Base de datos para anuncios y usuarios |
| **Proxy inverso** | Nginx | Enruta dominio → Nodepop, IP → Marketplace |
| **Estáticos** | Nginx | Sirve archivos estáticos con cabecera `X-Owner` |
| **Gestor de procesos** | Supervisor | Mantiene ambas apps en ejecución y reinicia en startup |

---

## 📋 Requisitos cumplidos

### Ejercicio 1 — Nodepop (por dominio)

- ✅ Node como servidor de aplicación con **Supervisor** como gestor de procesos
- ✅ La aplicación se reinicia automáticamente al arrancar el servidor (autostart)
- ✅ **Nginx** como proxy inverso que recibe las peticiones HTTP y las deriva a Node
- ✅ Archivos estáticos servidos por **Nginx** (no por Node)
- ✅ Cabecera personalizada `X-Owner: Aratea10` en los archivos estáticos

### Ejercicio 2 — Marketplace (por IP)

- ✅ Al acceder por IP se sirve la práctica de **React Avanzado** (Next.js)
- ✅ Al acceder por dominio se sirve **Nodepop** (Backend con Node)
- ✅ Next.js gestionado con Supervisor (reinicio automático)
- ✅ PostgreSQL en contenedor Docker

---

## 📁 Estructura del repositorio

```text
devops-practice/
├── [README.md](http://README.md)
├── exercise-1/
│   ├── nginx/
│   │   └── nodepop.conf              # Configuración de Nginx (ambos ejercicios)
│   └── supervisor/
│       └── nodepop.conf              # Configuración de Supervisor para Nodepop
└── exercise-2/
    ├── docker/
    │   └── docker-compose.yml        # PostgreSQL en Docker
    └── supervisor/
        └── marketplace.conf          # Configuración de Supervisor para Marketplace
```

---

## 🛠️ Configuración del servidor

### Prerrequisitos instalados

- Node.js v20.20.2 y v22.22.2 (via NVM)
- MongoDB 7.0
- PostgreSQL 17 (Docker)
- Nginx 1.24
- Supervisor 4.x
- Docker 28.2.2 + Docker Compose 2.37.1

### Rutas en el servidor

| Ruta | Descripción |
| --- | --- |
| `/home/ubuntu/nodepop` | Código de Nodepop |
| `/home/ubuntu/react-app` | Código del Marketplace (Next.js) |
| `/home/ubuntu/postgres` | Docker Compose de PostgreSQL |
| `/etc/nginx/sites-available/nodepop` | Configuración de Nginx |
| `/etc/supervisor/conf.d/nodepop.conf` | Supervisor — Nodepop |
| `/etc/supervisor/conf.d/marketplace.conf` | Supervisor — Marketplace |
| `/var/log/nodepop.out.log` | Logs Nodepop (stdout) |
| `/var/log/nodepop.err.log` | Logs Nodepop (errores) |
| `/var/log/marketplace.out.log` | Logs Marketplace (stdout) |
| `/var/log/marketplace.err.log` | Logs Marketplace (errores) |

---

## 🤝 Contribución

Si quieres mejorar el proyecto:

1. Haz fork del repositorio.
2. Crea una rama: `git checkout -b feature/mi-mejora`.
3. Haz commits claros siguiendo Conventional Commits.
4. Haz push y abre un Pull Request describiendo los cambios.

---

## 📄 Licencia

Este proyecto se entrega con [**Licencia MIT**](https://github.com/Aratea10/devops-practice/blob/main/LICENSE).

---

## 👩‍💻 Autora

**Sara Gallego Méndez** — Estudiante Bootcamp Desarrollo Web FullStack en [KeepCoding](https://keepcoding.io/).
