# Sistema de Gestión de Animales en un Refugio 🐾

Este proyecto implementa un sistema para gestionar animales en un refugio, permitiendo registrar diferentes tipos de animales, gestionar tratamientos médicos, registrar adopciones, calcular costos asociados al cuidado y proporcionar estadísticas relevantes. Además, incluye funcionalidades de persistencia para guardar y cargar datos.

## Funcionalidades Principales 🚀

1. **Registro de Animales**  
   - Registrar animales de distintos tipos (perros, gatos, aves).  
   - Validar datos como nombre y costo base al registrar.  

2. **Gestión de Tratamientos**  
   - Asignar tratamientos médicos a los animales.  
   - Calcular los costos de tratamientos adicionales.  

3. **Adopciones**  
   - Registrar adopciones para animales adoptables.  
   - Validar que un animal no adoptable no sea registrado como adoptado.  

4. **Cálculos y Estadísticas**  
   - Calcular costos asociados al cuidado de animales según su tipo y necesidades.  
   - Proporcionar estadísticas sobre:
     - Animales adoptados.  
     - Animales pendientes de adopción.  
     - Costo promedio de manutención por especie.  
   - Determinar el animal con mayor tiempo en el refugio.  

5. **Persistencia de Datos**  
   - Guardar y cargar datos en archivos binarios para mantener la información entre ejecuciones.  

---

## Arquitectura del Sistema 🏗️

### **Capa Modelo**
#### Clase Abstracta: `Animal`  
Define las características generales de los animales y sirve como base para las subclases específicas.  

**Atributos:**
- `int id`: Identificador único incremental.  
- `String nombre`: Nombre del animal.  
- `String especie`: Especie (perro, gato, ave, etc.).  
- `LocalDate fechaIngreso`: Fecha de ingreso al refugio.  
- `boolean adoptado`: Estado de adopción.  
- `double costoBase`: Costo base de manutención.  

**Métodos Abstractos:**
- `abstract double calcularCostoFinal()`: Calcula el costo total considerando características específicas.  

**Métodos Generales:**
- `Optional<LocalDate> calcularTiempoEnRefugio()`: Calcula el tiempo en el refugio si no ha sido adoptado.  
- `String obtenerEstado()`: Devuelve el estado ("Adoptado" o "Pendiente").  
- `boolean esAdoptable()`: Verifica si el animal puede ser adoptado.  

#### Subclases:  
1. **`Perro`**  
   - Atributo adicional: `boolean entrenado`.  
   - El costo aumenta si no está entrenado.  
2. **`Gato`**  
   - Atributo adicional: `boolean esterilizado`.  
   - El costo aumenta si no está esterilizado.  
3. **`Ave`**  
   - Atributo adicional: `String tipoAlimentacion`.  
   - El costo varía según el tipo de alimentación.  

---

#### Clase: `Tratamiento`  
**Atributos:**
- `int idAnimal`: ID del animal tratado.  
- `String descripcion`: Descripción del tratamiento.  
- `double costo`: Costo del tratamiento.  
- `LocalDate fecha`: Fecha del tratamiento.  

#### Clase: `Adopcion`  
**Atributos:**
- `String adoptante`: Nombre del adoptante.  
- `int idAnimal`: ID del animal adoptado.  
- `LocalDate fechaAdopcion`: Fecha de adopción.  

---

### **Capa de Gestión**
#### Clase: `RefugioGestor`  
Administra las listas de animales, tratamientos y adopciones.  

**Atributos:**
- `List<Animal> animales`: Lista de animales registrados.  
- `List<Tratamiento> tratamientos`: Lista de tratamientos realizados.  
- `List<Adopcion> adopciones`: Lista de adopciones realizadas.  

**Métodos Clave:**
- `boolean registrarAnimal(Animal animal)`: Registra un animal nuevo.  
- `Optional<Animal> buscarPorId(int id)`: Busca un animal por su ID.  
- `List<Animal> listarPorEspecie(String especie)`: Lista animales por especie.  
- `Optional<Tratamiento> agregarTratamiento(int idAnimal, Tratamiento tratamiento)`: Agrega tratamientos.  
- `Optional<Adopcion> registrarAdopcion(String adoptante, int idAnimal)`: Registra una adopción.  
- `List<Animal> consultarPendientesDeAdopcion()`: Lista animales pendientes de adopción.  
- `Map<String, Double> calcularCostoPromedioPorEspecie()`: Calcula costos promedio por especie.  
- `Optional<Animal> buscarAnimalConMayorTiempoEnRefugio()`: Encuentra el animal con mayor tiempo en el refugio.  

---

### **Capa de Persistencia**
#### Clase: `Persistencia`  
**Métodos:**
- `static <T> void guardarDatos(String archivo, List<T> datos)`: Guarda objetos genéricos en archivos binarios.  
- `static <T> List<T> cargarDatos(String archivo, Class<T> clase)`: Carga objetos genéricos desde archivos binarios.  
---
##Pruebas Unitarias 🧪
-Animales:

-Registrar animales válidos e inválidos.
-Verificar costos base negativos.
-Consultas:

-Listar animales pendientes de adopción.
-Identificar el animal con mayor tiempo en el refugio.
-Calcular costos promedio.
-Tratamientos y Adopciones:

-Agregar tratamientos y validar costos.
-Intentar adoptar animales no adoptables.
-Persistencia:
-Guardar y cargar datos.

## Ejemplos de Código
-
-
-
-
-
-
-
-
##Spoiler!!!!!!!!!!!
-
-
-
-
-
-
-
-

### Filtrar animales pendientes de adopción:
```java


List<Animal> pendientes = animales.stream()
    .filter(animal -> !animal.isAdoptado())
    .collect(Collectors.toList());

Calcular costo promedio por especie:
Map<String, Double> costoPromedio = animales.stream()
    .collect(Collectors.groupingBy(
        Animal::getEspecie, 
        Collectors.averagingDouble(Animal::calcularCostoFinal)
    ));

Guardar datos en archivos binarios:
public static <T> void guardarDatos(String archivo, List<T> datos) throws IOException {
    try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(archivo))) {
        oos.writeObject(datos);
    }
}


