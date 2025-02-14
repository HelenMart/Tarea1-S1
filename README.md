# Funciones
- Crear clase para representacion de un usuario con parametros basicos.
- Generar 100,000 usuarios con el mismo formato.
- Realizar búsqueda líneal y binaria.
- Medir tiempo de ejecucion de ambas búsqueda.
# Librerias
```python
import random
import string
import timeit
```

## Estructura de la clase 'Usuarios'

```python
class Usuarios:
    def __init__(self, id, nombre, edad):
        self.id = id
        self.nombre = nombre
        self.edad = edad

    def __repr__(self):  
        return f"Usuario: ID={self.id}, Nombre='{self.nombre}', Edad={self.edad}"
```
## Funciones Princiaple
##### Función para generar usuarios aleatorios
```python
def generarUsuarios(n):
    usuarios = []
    for i in range(1, n + 1):
        nombre = ''.join(random.choices(string.ascii_letters, k=5))  # Nombre de 5 letras aleatorias
        edad = random.randint(10, 50)
        usuarios.append(Usuarios(i, nombre, edad))  # Agregar usuario a la lista
    return usuarios
```

##### Funciones de búsqueda
```python
#Busqueda Lineal
def busqueda_lineal(usuarios, id_buscar):
    for usuario in usuarios:
        if usuario.id == id_buscar:
            return usuario  
    return None  # No se encontró

#Busqueda binaria
def busqueda_binaria(usuarios, id_buscar):
    izquierda, derecha = 0, len(usuarios) - 1

    while izquierda <= derecha:
        medio = (izquierda + derecha) // 2
        if usuarios[medio].id == id_buscar:
            return usuarios[medio]  
        elif usuarios[medio].id < id_buscar:
            izquierda = medio + 1  # Buscar en la mitad derecha
        else:
            derecha = medio - 1  # Buscar en la mitad izquierda

    return None  # No se encontró
```

##### Comparar tiempo de ejecución
```python
print(f"Tiempo de busqueda:")
print(f" ")
id = 50000
# Medir tiempo de búsqueda lineal
tiempo_lineal = timeit.timeit(lambda: busqueda_lineal(usuarios, id), number=1)
print(f"Busqueda Lineal: {tiempo_lineal:.6f} segundos")
# Medir tiempo de búsqueda binaria
tiempo_binaria = timeit.timeit(lambda: busqueda_binaria(usuarios, id), number=1)
print(f"Busqueda Binaria: {tiempo_binaria:.6f} segundos")
print(f" ")
```
