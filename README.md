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

## Clase `Analizador`

La clase Analizador se encarga de gestionar, almacenar y analizar datos climáticos a partir de registros individuales (RegistroClimatico). Su función principal es organizar la información recopilada en un conjunto de registros, calcular estadísticas relevantes y generar alertas relacionadas con la temperatura y la humedad.

### Atributos

- `self.registros`: Lista que almacena los objetos de tipo RegistroClimatico correspondientes a cada día o entrada de datos.

- `self.dias_unicos`: Conjunto que guarda las fechas registradas, garantizando que no se repitan días en el análisis.


### Métodos:

- `__init__(self)`: Constructor de la clase. Inicializa la lista registros y el conjunto dias_unicos.

- `cargar_datos(self, archivo_csv)`:
Carga los datos climáticos desde un archivo CSV.

Convierte el archivo en un DataFrame de pandas.

Itera sobre cada fila, creando un objeto RegistroClimatico con la fecha, temperatura y humedad.

Agrega cada registro a la lista registros y guarda la fecha en el conjunto dias_unicos.

- `estadisticas(self)`:
Calcula estadísticas básicas de temperatura y humedad a partir de los registros almacenados. Devuelve un diccionario con:

Temperatura promedio, máxima y mínima.

Humedad promedio, máxima y mínima.

- `generar_alertas_temperatura(self, umbral_calor=30)`:
Genera alertas de ola de calor para todos los días cuya temperatura supere el umbral indicado (por defecto 30 °C). Devuelve una lista de mensajes con la fecha y la temperatura.

- `clasificar_humedad(self, humedad)`:
Clasifica la humedad en tres categorías según su valor:

Humedad baja si es menor al 30 %.

Humedad moderada si se encuentra entre 30 % y 60 %.

Alta en cualquier otro caso.

- `generar_alertas_humedad(self)`:
Genera alertas en función de la humedad registrada cada día. Para ello utiliza el método clasificar_humedad y devuelve una lista con la fecha, el valor de humedad y su clasificación correspondiente.

- `generar_reportes_olas(self)`:
Esta funcion identifica y reporta períodos consecutivos de olas de calor, frío o temperatura ambiente con los registros de temperatura almacenados en self.registros y detecta secuencias de días consecutivos que cumplen ciertas condiciones y cuando una secuencia alcanza el número mínimo de días dias_minimos, se genera un reporte indicando las fechas de inicio y fin de la ola. 

- `dias_minimos` es el número mínimo de días consecutivos que deben cumplirse para considerar una secuencia como ola.
- `calor_umbral` es la temperatura mínima para considerar que un día pertenece a una ola de calor.
- `frio_umbral` es la temperatura máxima para considerar que un día pertenece a una ola de frío.
- `ambiente_rango` es el intervalo de temperaturas que se consideran como “temperatura ambiente agradable”.

1. Inicializa contadores para olas de calor, frío y ambiente.
2. Itera sobre cada registro de temperatura en `self.registros`.
3. Según el valor de la temperatura del día:
   - Aumenta el contador correspondiente (calor, frío o ambiente).
   - Reinicia los otros contadores en caso de que la condición cambie.
4. Cada vez que uno de los contadores alcanza `dias_minimos`, se añade un reporte con las fechas de inicio y fin de esa ola.
5. Devuelve la lista completa de reportes generados.

## Funcion `main(datos)`

La función `main(datos)` es el punto de entrada del programa. Su objetivo es cargar un archivo de datos climáticos, procesarlos mediante la clase `Analizador` y mostrar por pantalla un resumen con estadísticas, alertas y reportes de olas de temperatura.