
```markdown
# Conversor de Monedas

## Descripción

Esta aplicación en Java permite a los usuarios convertir entre diferentes monedas utilizando tasas de cambio actualizadas desde una API externa. El usuario puede elegir entre varias monedas predefinidas o ingresar códigos de monedas personalizados.

## Características

- Conversión entre varias monedas:
  - Dólar a Peso Argentino
  - Peso Argentino a Dólar
  - Dólar a Real Brasileño
  - Real Brasileño a Dólar
  - Dólar a Peso Colombiano
  - Peso Colombiano a Dólar
- Opción para ingresar códigos de monedas personalizadas.
- Tasas de conversión actualizadas en tiempo real.

## Requisitos

- Java 11 o superior
- Dependencia de Gson para la deserialización de JSON

## Instalación

1. **Clonar el repositorio:**

   ```bash
   git clone <URL_DEL_REPOSITORIO>
   cd <NOMBRE_DEL_REPOSITORIO>
   ```

2. **Agregar la dependencia de Gson**: Si estás utilizando un gestor de dependencias como Maven o Gradle, asegúrate de incluir la dependencia de Gson en tu archivo de configuración.

   **Para Maven**, agrega esto a tu archivo `pom.xml`:

   ```xml
   <dependency>
       <groupId>com.google.code.gson</groupId>
       <artifactId>gson</artifactId>
       <version>2.8.9</version>
   </dependency>
   ```

3. **Compilar la aplicación**:

   Asegúrate de estar en el directorio raíz del proyecto y ejecuta:

   ```bash
   javac Principal.java ConsultarMoneda.java ConvertirMoneda.java Monedas.java
   ```

## Uso

1. **Ejecutar la aplicación**:

   Desde el directorio donde están los archivos `.class`, ejecuta:

   ```bash
   java Principal
   ```

2. **Interfaz de usuario**:

   - El programa mostrará un menú con las opciones de conversión.
   - Selecciona el número correspondiente a la conversión que deseas realizar.
   - Ingresa la cantidad que deseas convertir cuando se te solicite.
   - El programa mostrará la cantidad convertida y la tasa de conversión actual.

3. **Salir de la aplicación**:

   Selecciona la opción 8 en el menú para salir.

## Contribuciones

Si deseas contribuir a este proyecto, por favor abre un issue o envía un pull request.

---

## Desglose del Código

### 1. Clase `Principal`

Esta es la clase principal que ejecuta el programa. Su función es ofrecer un menú al usuario para realizar conversiones de monedas.

- **Importaciones**: Se importa `Scanner` para leer la entrada del usuario.
- **Método `main`**:
  - Crea un objeto `Scanner` para capturar la entrada del usuario.
  - Crea un objeto `ConsultarMoneda` para consultar tasas de conversión.
  - Usa un bucle `while` que permite al usuario seleccionar varias opciones hasta que decida salir (opción 8).
  - Muestra un menú con las opciones de conversión de monedas.
  - Según la opción seleccionada, llama al método `convertir` o `convertirOtraMoneda` de la clase `ConvertirMoneda`.

### 2. Clase `Monedas`

Este es un **record** que define una estructura de datos para almacenar información sobre la conversión de monedas.

- **Atributos**:
  - `base_code`: código de la moneda base (por ejemplo, USD).
  - `target_code`: código de la moneda objetivo (por ejemplo, ARS).
  - `conversion_rate`: tasa de conversión entre las dos monedas.

Un record en Java es una forma sencilla de crear clases que son principalmente portadoras de datos, con menos código boilerplate.

### 3. Clase `ConsultarMoneda`

Esta clase se encarga de obtener la tasa de conversión de una API externa.

- **Método `buscarMoneda`**:
  - Toma como parámetros los códigos de la moneda base y la moneda objetivo.
  - Construye una URL para realizar una solicitud a la API de tasas de cambio.
  - Utiliza `HttpClient` para enviar una solicitud y obtener la respuesta.
  - La respuesta se deserializa (convierte de JSON a un objeto Java) usando la biblioteca Gson.
  - Crea un objeto `Monedas` con los datos obtenidos de la API.
  - Si ocurre un error (por ejemplo, si la moneda no se encuentra), lanza una excepción.

### 4. Clase `ConvertirMoneda`

Esta clase tiene métodos que realizan las conversiones efectivamente.

- **Método `convertir`**:
  - Toma como parámetros los códigos de la moneda base y la moneda objetivo, el objeto `ConsultarMoneda` y el `Scanner`.
  - Llama al método `buscarMoneda` para obtener la tasa de conversión.
  - Muestra al usuario la tasa de conversión actual.
  - Solicita al usuario que ingrese la cantidad que desea convertir.
  - Calcula la cantidad convertida usando la tasa de conversión.
  - Muestra el resultado.
  - Maneja excepciones en caso de que la entrada del usuario no sea un número válido.

- **Método `convertirOtraMoneda`**:
  - Permite al usuario ingresar códigos de monedas personalizados.
  - Llama al método `convertir` con los códigos ingresados.

### Flujo general del programa

1. El usuario inicia el programa y se le presenta un menú.
2. Elige una opción de conversión de monedas.
3. El programa consulta la tasa de conversión usando la API externa.
4. El usuario ingresa la cantidad que desea convertir.
5. Se muestra el resultado de la conversión.
6. El ciclo continúa hasta que el usuario decide salir.
