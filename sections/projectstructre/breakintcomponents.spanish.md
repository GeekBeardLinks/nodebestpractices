# Estructura tu solución en componentes

<br/><br/>

### Explicación de un párrafo

Para aplicaciones de tamaño medio o superior, los monolitos *no modulares* son bastante malos. Tener un gran software con un "spaghetti" de dependencias es simplemente dificil de razonar sobre él. La solución definitiva es desarrollar software más pequeño: dividir toda la pila en componentes autónomos que no compartan archivos con otros, cada uno es una aplicación lógica independiente (por ejemplo, tienen su propia API, servicios, acceso a datos, tests, etc.) de modo que incorporarse a él y cambiar el código sea mucho más fácil que lidiar con todo el sistema. Algunos pueden llamar a esto arquitectura de 'microservicios'; es importante comprender que los microservicios no son una especificación que se deba seguir, sino más bien un conjunto de principios. Puede adoptar muchos principios en una arquitectura de microservicios completa o adoptar solo unos pocos. Lo mínimo que debe hacer es crear límites básicos entre los componentes, asignar una carpeta o repositorio en la raíz de su sistema para cada componente de negocio y hacerlo autónomo. Otros componentes pueden consumir su funcionalidad solo a través de su interfaz pública o API. Esta es la base para mantener sus componentes simples, evitar el infierno de dependencias y allanar el camino  hacia los microservicios completos en un futuro una vez que su aplicación crezca.
<br/><br/>

### Blog Quote: "Scaling requires scaling of the entire application"

 From the blog [MartinFowler.com](https://martinfowler.com/articles/microservices.html)

> Monolithic applications can be successful, but increasingly people are feeling frustrations with them - especially as more applications are being deployed to the cloud. Change cycles are tied together - a change made to a small part of the application requires the entire monolith to be rebuilt and deployed. Over time it's often hard to keep a good modular structure, making it harder to keep changes that ought to only affect one module within that module. Scaling requires scaling of the entire application rather than parts of it that require greater resource.

> *Las aplicaciones monolíticas pueden tener éxito, pero cada vez más personas se sienten frustradas con ellas - especialmente mientras más aplicaciones son desplegadas en la nube. Ciclos de cambios están unidos - un cambio hecho a una pequeña parte de la aplicación requiere que el monolito sea reconstruido y desplegado. A través del tiempo es común que sea difícil mantener una buena estructura modular, haciendo difícil mantener los cambios que solo afectan un módulo dentro de ese otro módulo. Escalar requiere escalar la aplicación completa en vez de sólo partes que requieren mayores recursos*

<br/><br/>

### Blog Quote: "So what does the architecture of your application scream?"

 From the blog [uncle-bob](https://8thlight.com/blog/uncle-bob/2011/09/30/Screaming-Architecture.html) 

> ...if you were looking at the architecture of a library, you’d likely see a grand entrance, an area for check-in-out clerks, reading areas, small conference rooms, and gallery after gallery capable of holding bookshelves for all the books in the library. That architecture would scream: Library.<br/>

> *...si observas la arquitectura de una biblioteca, es probable que veas una gran entrada, un área para entrada-salida de empleados, áreas de lectura, pequeñas salas de conferencias, y galería tras galería capaces de sostener estanterías para todos los libros en la biblioteca. Esa arquitectura gritaría: Biblioteca*

Así que, ¿qué es lo que grita la arquitectura de tu aplicación? Cuando ves la estructura de directorios en el nivel superior y los archivos fuente en el paquete de más alto nivel; gritan: ¿Sistema de Cuidado de Salud,  Sistema de Contabilidad o Sistema de Manejo de Inventario? o a caso gritan ¿Rails, Spring/Hibernate o ASP?

<br/><br/>

### Bien: Estructurar tu solución en componentes auto-contenidos

```bash
my-system
├─ apps (componentes)
│  ├─ orders
│  │ ├─ package.json
│  │ ├─ api
│  │ ├─ domain
│  │ ├─ data-access
│  ├─ users
│  ├─ payments
├─ libraries (funcionalidad genérica transversal a componentes)
│  ├─ logger
│  ├─ authenticator
```

<br/><br/>

### Mal: Agrupar tus archivos según rol técnico

```bash
my-system
├─ controllers
│  ├─ user-controller.js
│  ├─ order-controller.js
│  ├─ payment-controller.js
├─ services
│  ├─ user-service.js
│  ├─ order-service.js
│  ├─ payment-service.js
├─ models
│  ├─ user-model.js
│  ├─ order-model.js
│  ├─ payment-model.js
```