# Sistema de Gestión de Hamburguesería 🍔

Este proyecto consiste en una aplicación de escritorio interactiva y robusta desarrollada para el módulo de **Programación**. El sistema permite centralizar los procesos de un restaurante de comida rápida, permitiendo la interacción directa de los consumidores con el catálogo de productos y ofreciendo un panel administrativo protegido para la gestión del negocio.

---

## 1. Descripción del Proyecto

La aplicación distribuye sus funciones mediante un control de accesos basado en roles de usuario (`Administrador` y `Cliente`), comunicándose dinámicamente con un servidor de bases de datos relacionales:

* **Módulo de Clientes:** Permite a los usuarios registrarse e iniciar sesión de forma segura tras validar sus credenciales. Una vez dentro, disponen de un catálogo dinámico dividido en **Hamburguesas, Bebidas y Extras**. Los clientes seleccionan sus productos favoritos, visualizan sus detalles, interactúan con un carrito virtual y confirman sus compras. Tras procesar el pago, el sistema almacena la transacción en la base de datos y genera automáticamente un ticket físico en formato de texto plano (`.txt`).
* **Módulo de Administración:** Actúa como panel de operaciones del establecimiento. Los administradores disponen de privilegios exclusivos para registrar nuevos administradores, purgar cuentas de usuario inoperantes del sistema, dar de baja productos de forma selectiva y agilizar la actualización del inventario mediante un proceso de importación masiva que lee e inserta datos desde un archivo estructurado `.csv`.

### Tecnologías y Herramientas Utilizadas
* **Lenguaje:** Java (JDK 17)
* **Interfaz Gráfica (GUI):** JavaFX apoyado en hojas de estilo personalizadas (`estilos.css`).
* **Persistencia de Datos:** Motor de base de datos MySQL mediante conectores JDBC.
* **Estructuras Físicas Externas:** Carga selectiva de stock (`.csv`) y exportación automatizada de tickets de caja (`.txt`).

---

## 2. Estructura del Código y Arquitectura

El diseño de la aplicación respeta los principios de modularidad y separación de responsabilidades distribuyendo el código en tres grandes paquetes (`packages`):

```text
RETO_FINAL/
│
├── app/                        # Capa de Negocio e Interfaz de Usuario
│   ├── MainApp.java            # Orquestador visual JavaFX y gestor de pantallas
│   ├── Usuario.java            # Superclase abstracta de usuarios del sistema
│   ├── Administrador.java      # Subclase con credenciales de gestión corporativa
│   ├── Cliente.java            # Subclase orientada al consumidor final
│   ├── Producto.java           # Superclase base del catálogo alimentario
│   ├── Hamburguesa.java        # Entidad hija que añade atributos como tipo de carne
│   ├── Bebida.java             # Entidad hija que añade marcas de control alcohólico
│   ├── Extra.java              # Entidad hija especializada en acompañamientos
│   ├── Pedidos.java            # Lógica del carrito de compras y generación de tickets
│   ├── GenerarInforme.java     # Interfaz abstracta para inyección de polimorfismo
│   └── estilos.css             # Reglas visuales para el diseño de la aplicación
│
├── mysql/                      # Capa de Datos y Persistencia Relacional
│   ├── DataBaseConnection.java # Gestor de canales de conexión mediante DriverManager
│   └── AccessDB.java           # Controladora de operaciones y consultas SQL (CRUD)
│
└── util/                       # Recursos auxiliares del sistema
    ├── LibreriaMetodos.java    # Validaciones algorítmicas (RegEx de seguridad)
    └── productos.csv           # Archivo estructurado de carga masiva de stock
