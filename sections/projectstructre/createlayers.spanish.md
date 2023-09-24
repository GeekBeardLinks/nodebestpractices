# Separe su aplicación en capas, mantenga la capa web dentro de sus límites

<br/><br/>

### Separe en 3 capas el código de los componentes 



El directorio raíz de cada componente debería contener 3 carpetas que representan intereses y etapas comunes a cada transacción:

```bash
my-system
├─ apps (componentes)
│  ├─ component-a
   │  ├─ entry-points (puntos de entrada)
   │  │  ├─ api # el controlador va aquí
   │  │  ├─ message-queue # el consumidor de mensaje va aqui
   │  ├─ domain (dominio) # funcionalidades y flujos: DTO, servicios, lógica
   │  ├─ data-access (acceso a datos) # Llamadas a BDD sin ORM
```

**- Puntos de entrada (entry-points) -** Aquí es donde comienzan las solicitudes y los flujos, ya sea API REST, GraphQL, cola de mensajes, trabajos programados o cualquier otra _puerta_ a la aplicación. La responsabilidad de esta capa es mínima: adaptar la carga útil (por ejemplo, JSON) al formato de la aplicación, incluida la primera validación, llamar a la capa lógica/dominio y devolver una respuesta. Normalmente, esto se logra con unas pocas líneas de código. Muchos usan el término "controlador" para este tipo de código también técnicamente es solo un adaptador.

**- Dominio (domain) -** Aquí es donde fluye la aplicación, donde vive la lógica y los datos. Esta capa acepta entrada independiente del protocolo, un objeto JavaScript simple y también devuelve uno[^1]. Técnicamente contiene objetos de código comunes como servicios, dto/entidades y clientes que llaman a servicios externos. También suele llamar a la capa de acceso a datos para recuperar o conservar información.

**- Acceso a datos (data-access) -** Aquí es donde la aplicación contiene código que interactúa con la BDD. Idealmente, debería externalizar una interfaz que devuelva/obtenga un objeto JavaScript simple que sea agnóstica de la BDD (también conocido como patrón de repositorio). Esta capa incluye utilidades auxiliares de BDD, como constructores de consultas[^2], ORM, controladores de base de datos y otras bibliotecas de implementación.

**¿Cuál es el mérito? -** Al tener una infraestructura flexible que permite agregar más llamadas API y consultas de BDD rápidamente, un desarrollador puede codificar una función más rápido centrándose en la carpeta del dominio. Es decir, se dedica menos tiempo a actividades técnicas y más a actividades que agregan valor. Este es un rasgo omnipresente que está en el corazón de la mayoría de las arquitecturas de software como DDD, hexagonal, arquitectura limpia y otras. Además de esto, cuando la capa de dominio no conoce ningún protocolo perimetral, puede atender a cualquier cliente y no solo a las llamadas HTTP.

**¿Por qué no MVC o una arquitectura limpia? -** El patrón de 3 niveles logra un gran equilibrio entre lograr el objetivo de separación y al mismo tiempo mantener la estructura simple. También carece de abstracciones: cada nivel representa el nivel físico del mundo real que visitará cada solicitud. Por otro lado, MVC es un patrón simplista donde las letras VC representan sólo unas pocas líneas de un código y la letra M significa cualquier otra cosa. La arquitectura limpia es una arquitectura con un alto nivel de abstracciones que puede lograr una separación aún mayor, pero el precio es desproporcionadamente mayor debido a la mayor complejidad.

[^1]: N. del T. se asume que se trata de objetos que no poseen dependencias a los frameworks utilizados.

[^2]: N. del T. en inglés query builders.
