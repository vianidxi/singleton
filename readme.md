# Ejercicio: Singleton en Java

Este ejercicio practica la implementación del patrón de diseño Singleton en Java y te ayuda a comprender por qué es importante controlar la creación de instancias en aplicaciones con configuración global.

## Objetivo y forma de trabajo

Al terminar, deberás demostrar que puedes:

- identificar cuándo un objeto debe mantenerse único,
- refactorizar una clase para convertirla en Singleton,
- actualizar el código cliente para usar la instancia compartida,
- compilar y ejecutar el programa para comprobar el comportamiento final.

En cada etapa:

1. Lee la explicación del problema.
2. Realiza la modificación solicitada en los archivos Java.
3. Compila y ejecuta el programa.
4. Comprueba el resultado antes de marcar cada casilla.

No marques una casilla si el código no compila o si no puedes explicar qué cambió.

## 1. Comprender el problema

La clase `AppConfig` representa la configuración global de la aplicación: tema, idioma, y otros ajustes que deben ser consistentes en toda la ejecución.

El código inicial crea varias instancias distintas de `AppConfig`, lo que permite que diferentes partes del sistema trabajen con configuraciones diferentes y generen inconsistencias.

Abre `AppConfig.java` y `Main.java` y observa el comportamiento actual.

```java
public class Main {
    public static void main(String[] args) {
        AppConfig config1 = new AppConfig();
        AppConfig config2 = new AppConfig();

        config1.setTheme("Dark");
        config1.printConfig();
        config2.printConfig();

        System.out.println("Are these the same instance? " + (config1 == config2));
    }
}
```

**Actividad:** identifica qué problema aparece al crear dos objetos distintos para la misma configuración.

- [x] Revisé el problema inicial y entiendo por qué `AppConfig` debería tener una sola instancia.

## 2. Convertir `AppConfig` en Singleton

Aplica el patrón Singleton con inicialización ansiosa.

### Instrucciones

1. Haz el constructor privado.
2. Crea un campo `static final` llamado `instance`.
3. Inicializa ese campo con `new AppConfig()`.
4. Añade el método público y estático `getInstance()`.

Ejemplo:

```java
public class AppConfig {
    private static final AppConfig instance = new AppConfig();

    private AppConfig() {
        this.theme = "Light";
        this.language = "EN";
    }

    public static AppConfig getInstance() {
        return instance;
    }
}
```

**Actividad:** modifica la clase `AppConfig` para que nadie pueda crear nuevas instancias con `new` y para que todas las partes de la aplicación usen la misma referencia.

- [x] El constructor de `AppConfig` es privado.
- [x] Existe un campo `instance` `static` y `final`.
- [x] El método `getInstance()` devuelve la única instancia disponible.

## 3. Actualizar el cliente

En `Main.java`, reemplaza las llamadas a `new AppConfig()` por `AppConfig.getInstance()`.

```java
public class Main {
    public static void main(String[] args) {
        AppConfig config1 = AppConfig.getInstance();
        AppConfig config2 = AppConfig.getInstance();

        config1.setTheme("Dark");
        config1.printConfig();
        config2.printConfig();

        System.out.println("Are these the same instance? " + (config1 == config2));
    }
}
```

**Actividad:** ejecuta el programa después del cambio y comprueba que `config1` y `config2` apuntan a la misma instancia.

- [ ] Actualicé `Main` para utilizar `AppConfig.getInstance()`.
- [ ] Ejecuté el programa y comprobé el resultado de `(config1 == config2)`.

## 4. Compilar y ejecutar el ejercicio

Desde la raíz del proyecto, compila y ejecuta:

```bash
javac AppConfig.java Main.java
java Main
```

El programa debe imprimir la configuración y mostrar que ambas referencias son la misma instancia.

**Actividad:** guarda la salida que te permita demostrar que el patrón Singleton funciona correctamente.

- [ ] El programa compiló sin errores.
- [ ] Ejecuté `Main` y verifiqué la salida final.

## 5. Reflexión final

Responde estas preguntas en tu cuaderno o en tu entrega:

- ¿Cuál es el resultado de `(config1 == config2)` después de aplicar Singleton?
- ¿Por qué el campo `instance` debe ser `static`?
- ¿Qué ventaja tiene garantizar que exista una única instancia de configuración?
- ¿Cuál es la principal desventaja de la inicialización ansiosa?
- ¿Qué problema puede aparecer si el Singleton guarda estado global y la aplicación crece mucho?

**Actividad:** anota tus respuestas y prepárate para discutirlas en clase.

- [ ] Respondí las preguntas de análisis y entendí el impacto del patrón Singleton.

## 6. Criterio de finalización

Este ejercicio está terminado cuando:

- la clase `AppConfig` usa constructor privado,
- existe una única instancia compartida,
- `Main` usa `getInstance()`,
- el programa compila y ejecuta correctamente,
- comprendes las ventajas y limitaciones del patrón.

- [ ] He completado el ejercicio de Singleton en Java y puedo explicar el resultado final.