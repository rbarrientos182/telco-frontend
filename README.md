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
