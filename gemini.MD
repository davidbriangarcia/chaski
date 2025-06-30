# gemini.md: Blueprint del Esqueleto de Software "Chaski"

## 1. Visión del Proyecto

**Nombre del Proyecto:** Chaski Framework (o "Esqueleto Chaski")

**Visión:** Crear un esqueleto de software (boilerplate) modular, escalable y optimizado para el mercado peruano. "Chaski" representa la rapidez y eficiencia con la que entregaremos soluciones web profesionales a nuestros clientes. El objetivo es reducir el tiempo de desarrollo en un 60-70% para proyectos recurrentes, permitiéndonos ofrecer precios competitivos y entregar valor rápidamente.

**Clientes Objetivo Iniciales:**
1.  **Restaurantes, Cafeterías y Bares.**
2.  **Tiendas de Ropa, Moda y Accesorios (Retail).**

---

## 2. Filosofía y Principios de Diseño

* **Modularidad (Plug-and-Play):** El núcleo debe ser agnóstico al tipo de negocio. Las funcionalidades específicas (menús, catálogos) se cargarán como módulos independientes.
* **Personalización Sencilla (Theming):** Debe ser fácil cambiar colores, tipografías y logos para adaptar el sitio a la marca de cada cliente sin reescribir código.
* **Rendimiento y SEO Primero:** Las webs deben ser rápidas y estar optimizadas para los motores de búsqueda desde su base (uso de SSR/SSG).
* **Gestión por el Cliente:** El cliente final debe poder gestionar su contenido (platos del menú, productos, fotos) a través de un panel de administración amigable (CMS Headless).

---

## 3. Pila Tecnológica (Tech Stack)

* **Frontend:** **Next.js (React)** - Excelente para SEO (SSR/SSG), gran ecosistema y rendimiento.
* **Estilos:** **Tailwind CSS** - Para un desarrollo rápido, personalizable y mantenible.
* **Backend (API):** **Node.js con Express.js o NestJS** - NestJS es recomendado por su arquitectura modular y el uso de TypeScript, lo que se alinea con la visión del proyecto.
* **Base de Datos:** **PostgreSQL** - Robusta, escalable y excelente para manejar datos relacionales como usuarios, órdenes e inventario.
* **CMS Headless:** **Strapi.io** - Es de código abierto, se puede auto-hospedar (ahorro de costos) y es muy fácil de usar para el cliente final para gestionar productos, menús, etc.
* **Pasarelas de Pago (Perú):** La arquitectura debe permitir una fácil integración. Las prioridades son:
    1.  **Mercado Pago** (muy popular)
    2.  **Izipay / Niubiz** (requieren afiliación comercial)
    3.  **Stripe** (para clientes internacionales o más tecnológicos)
* **Gestión de Estado (Frontend):** **Zustand** o **Redux Toolkit** - Para manejar estados globales como el carrito de compras.

---

## 4. Estructura de Carpetas del Esqueleto
/chaski
├── 📂 client/              # Frontend (Next.js)
│   ├── 📂 components/      # Componentes UI reutilizables (Botones, Inputs, Cards)
│   │   ├── 📂 common/
│   │   └── 📂 modules/     # Componentes específicos de cada módulo
│   ├── 📂 contexts/       # Contextos de React (Ej: AuthContext, CartContext)
│   ├── 📂 layouts/         # Estructuras de página (Ej: MainLayout con Navbar/Footer)
│   ├── 📂 pages/           # Rutas y páginas del sitio
│   ├── 📂 public/          # Archivos estáticos (imágenes, fuentes)
│   ├── 📂 styles/          # CSS Global y configuración de Tailwind
│   └── 📂 lib/             # Funciones de ayuda, cliente de API
│
├── 📂 server/              # Backend (NestJS / Express)
│   ├── 📂 src/
│   │   ├── 📂 auth/         # Lógica de autenticación (JWT)
│   │   ├── 📂 config/       # Configuración de DB, variables de entorno
│   │   ├── 📂 modules/     # Módulos de negocio (core y específicos)
│   │   │   ├── 📂 core/     # Funcionalidades base (usuarios, roles)
│   │   │   ├── 📂 restaurant/ # Lógica para restaurantes (menús, reservas)
│   │   │   └── 📂 ecommerce/  # Lógica para tiendas (productos, órdenes, pagos)
│   │   ├── main.ts         # Punto de entrada de la app
│   └── Dockerfile        # Para contenedorizar el backend
│
├── 📂 cms/                 # Configuración y backups del CMS (Strapi)
│
├── 📜 .env.example         # Variables de entorno de ejemplo
├── 📜 .gitignore
├── 📜 docker-compose.yml   # Para levantar todo el entorno (DB, Server, CMS)
└── 📜 gemini.md            # Este archivo

## 5. Módulos y Funcionalidades Clave

### 5.1. Módulo Core (Base para todos los proyectos)

-   [ ] Sistema de Autenticación (JWT para usuarios y administradores).
-   [ ] Panel de Administración básico (integrado o vía el CMS).
-   [ ] Sistema de Theming (archivo de configuración `theme.config.js` para colores, fuentes, logo).
-   [ ] Componentes Comunes (Navbar, Footer, Botón de WhatsApp flotante, Formulario de Contacto).
-   [ ] Página "Nosotros", "Contacto" (con mapa).

### 5.2. Módulo Restaurante (`@modules/restaurant`)

-   [ ] **Gestión de Menú:** Entidad en el CMS para Platos con nombre, descripción, precio, foto y categoría (Entradas, Segundos, Bebidas, etc.).
-   [ ] **Componente de Menú Digital:** Componente de React que renderiza el menú de forma atractiva y filtrable.
-   [ ] **Sistema de Reservas:** Formulario de reserva que envía un correo de notificación o guarda la reserva en la base de datos.
-   [ ] **Galería de Fotos:** Integrada con el CMS para que el cliente suba fotos del local y los platos.

### 5.3. Módulo E-commerce (`@modules/ecommerce`)

-   [ ] **Gestión de Productos:** Entidad en el CMS para Productos con nombre, SKU, descripción, fotos, precio, stock.
-   [ ] **Variantes de Producto:** Soporte para tallas, colores, etc.
-   [ ] **Catálogo de Productos:** Página con filtros (por categoría, precio) y búsqueda.
-   [ ] **Carrito de Compras:** Lógica de estado global para añadir, eliminar y actualizar productos en el carrito.
-   [ ] **Proceso de Checkout:** Formulario para datos de envío y facturación.
-   [ ] **Integración de Pasarela de Pagos:** Interfaz estandarizada en el backend para conectar `Mercado Pago` u otras.
-   [ ] **Gestión de Órdenes:** Guardado de órdenes en la base de datos con su estado (Pendiente, Pagado, Enviado).

---

## 6. Hoja de Ruta (Roadmap)

* **Fase 1 (Mes 1): El Núcleo.**
    * [ ] Montar la estructura de carpetas y repositorios (Git).
    * [ ] Configurar el entorno de desarrollo con Docker.
    * [ ] Desarrollar el Módulo Core: Autenticación, Theming y componentes básicos.
    * [ ] Integrar Strapi y definir los modelos de datos básicos.

* **Fase 2 (Mes 2): Módulo Restaurante.**
    * [ ] Desarrollar las entidades y la lógica del backend para menús y reservas.
    * [ ] Crear los componentes de React para el frontend.
    * [ ] Construir un sitio de demostración completo para un restaurante ficticio.

* **Fase 3 (Mes 3-4): Módulo E-commerce.**
    * [ ] Desarrollar la lógica de productos, inventario y órdenes.
    * [ ] Implementar el carrito de compras y el flujo de checkout.
    * [ ] **Prioridad Alta:** Integrar y probar exitosamente la pasarela de Mercado Pago.
    * [ ] Construir un sitio de demostración completo para una tienda de ropa ficticia.

* **Fase 4 (Continuo): Documentación y Mejora.**
    * [ ] Documentar cómo usar el esqueleto, cómo configurar un nuevo cliente y cómo activar módulos.
    * [ ] Refinar y optimizar el código base a partir de los primeros proyectos reales.
