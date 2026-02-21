# Telco Predict - Frontend 🚀

**Sistema de Monitoreo de Retención de Clientes mediante Machine Learning**

Este proyecto es el frontend desarrollado en **Vue.js 3** para telco. Se integra con un backend en **Django REST Framework** que procesa un modelo predictivo de Churn (abandono) basado en el dataset de Telco de IBM.

## 🛠️ Stack Tecnológico

- **Framework:** Vue 3 (Composition API)
- **Estado Global:** Pinia
- **Enrutamiento:** Vue Router
- **Estilos:** Bootstrap 5 + CSS Corporativo (Telmex Style)
- **Cliente API:** Axios (con interceptores para JWT)
- **Herramienta de Construcción:** Vite

## 📂 Estructura del Proyecto

```text
src/
├── api/          # Configuración de Axios e Interceptores
├── assets/       # Estilos corporativos y logos
├── components/   # Componentes de UI (Tablas de riesgo, Cards)
├── layouts/      # Plantillas (Auth vs Dashboard)
├── stores/       # Manejo de tokens JWT con Pinia
├── views/        # Páginas (Login y Monitor de Riesgo)
└── router/       # Guardias de navegación (Seguridad)
```

🚀 Instalación y Configuración

1. Clonar y Preparar
   Bash
   git clone https://github.com/rbarrientos182/telco-frontend.git
   cd telco-frontend
   npm install
2. Variables de Entorno
   Crea un archivo .env en la raíz con la dirección de tu backend en Django:

Fragmento de código
VITE_API_URL=http://localhost:8000/api

3. Ejecución en Desarrollo
   Bash
   npm run dev
   🔒 Seguridad e Integración
   El sistema utiliza JSON Web Tokens (JWT) para la comunicación segura.

El usuario se autentica contra el backend de Django.

El token se almacena de forma segura en localStorage y se gestiona mediante el Auth Store de Pinia.

Se utiliza un Navigation Guard en Vue Router para prevenir el acceso no autorizado al Monitor de Riesgo.

📊 Dashboard de Riesgo
El monitor clasifica a los clientes en tres niveles mediante colores corporativos:

🔴 Crítico (>70%): Requiere llamada de retención inmediata.

🟡 Observación (40%-70%): Cliente con señales de abandono.

🟢 Estable (<40%): Cliente con baja probabilidad de fuga.

Autor: Ing. Barrientos
