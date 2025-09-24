# Proyecto: Análisis Climático

Este proyecto tiene como objetivo analizar datos climáticos almacenados en archivos CSV. La estructura principal del código se organiza en dos clases: `RegistroClimatico` y `Analizador`.

## Clase `RegistroClimatico`

Esta clase representa un registro individual de datos climáticos. Su función principal es almacenar información de manera organizada para facilitar el análisis posterior.  

### Atributos:
- `fecha`: Fecha del registro climático.
- `temperatura`: Temperatura registrada (en °C).
- `humedad`: Humedad relativa registrada (en %).

### Métodos:
- `__init__(self, fecha, temperatura, humedad)`: Constructor que inicializa un objeto `RegistroClimatico` con los datos proporcionados.
- `__repr__(self)`: Representación en forma de string del objeto, útil para imprimir el registro de manera legible en consola.