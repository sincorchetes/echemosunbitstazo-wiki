# Tuplas, listas, diccionarios y sets

## Tuplas tuple
Conjunto de valores que no cambian dentro del flujo de la ejecución del programa. Pueden contener como valor todo tipo de dato incluyendo otra tupla.

_Más info en la <a href="https://docs.python.org/3/library/stdtypes.html?highlight=tuple#tuple" target="blank">doc oficial de Python_</a>
```python
>>> nacionalidad = ( 'Español', 'Turco', 'Italiano')
>>> paises = ( 'España', nacionalidad, 'Turquía', 'Italia' )
>>> print(paises)
('España', ('Español', 'Turco', 'Italiano'), 'Turquía', 'Italia')
```
Añadir elementos a la tupla:
```python
>>> nacionalidad = ( 'Español', 'Turco', 'Italiano')
>>> paises = ( 'España', nacionalidad, 'Turquía', 'Italia' )
>>> paises += ('Francia', 'Munich')
>>> print(paises)
('España', ('Español', 'Turco', 'Italiano'), 'Turquía', 'Italia', 'Francia', 'Munich')
```
Duplicar el `str` o caracter que obtengamos por un nº de veces:
```python
>>> nacionalidad = ( 'Español', 'Turco', 'Italiano')
>>> nacionalidad * 2
('Español', 'Turco', 'Italiano', 'Español', 'Turco', 'Italiano')
```
Muestra el `str` que esté ubicada en una posición:
```python
>>> nacionalidad = ( 'Español', 'Turco', 'Italiano')
>>> print(nacionalidad[2])
'Italiano'
```
Mostrar un conjunto de valores específicos de la tupla haciendo uso de su posición:
```python
>>> paises = ( 'España', nacionalidad, 'Turquía', 'Italia','Francia', 'Munich')
>>> print(paises[3:5])
('Italia', 'Francia')
```

## Listas
Grupo de valores representados dentro de unos [], se pueden cambiar de forma simple y sencilla.
_Más info en la <a href="https://docs.python.org/3/library/stdtypes.html?highlight=list#list" target="blank">doc oficial de Python_</a>

Declarando una lista:
```python
>>> animales = [ 'gato', 'perro', 'búho' ]
```
Añadir valores en la última posición de la lista, (_similar a la tupla_):
```python
>>> animales = [ 'gato', 'perro', 'búho' ]
>>> animales += [ 'lagartija', 'pez' ]
>>> print(animales)
['gato', 'perro', 'búho', 'lagartija', 'pez']
```
También podemos utilizar `.extend()`:
```python
>>> animales = [ 'gato', 'perro', 'búho' ]
>>> animales.extend([ 'lagartija', 'pez' ])
>>> print(animales)
['gato', 'perro', 'búho', 'lagartija', 'pez']
```
Por otro lado podemos añadir un valor a partir de una posición específica dentro de la lista `.insert()`
```python
>>> animales = [ 'gato', 'perro', 'búho' ]
>>> animales.insert(0, 'lagartija')
>>> print(animales)
['lagartija', 'gato', 'perro', 'búho']
```
Eliminar un valor de la lista:
```python
>>> animales = [ 'gato', 'perro', 'búho' ]
>>> animales.remove('gato')
>>> print(animales)
[ 'perro', 'búho' ]
```
Multiplicar el nº veces los valores de la lista:
```python
>>> animales = [ 'gato', 'perro', 'búho' ]
>>> animales * 2
['gato', 'perro', 'búho', 'gato', 'perro', 'búho']
```
Mostrar valores específicos utilizando la posición de dichos valores en la lista:
```python
>>> animales = [ 'gato', 'perro', 'búho' ]
>>> print(animales[0:2])
['gato', 'perro']
```

## Diccionarios
Son un conjunto de valores que se almacenan en modo *clave:valor*, separados los valores por comas, y todas las claves y sus valores van encerrados en `{}` como JSON. Las claves no pueden contener tuplas, diccionarios, sets... solo `str` o `int`.
_Más info en la <a href="https://docs.python.org/3/library/stdtypes.html?highlight=dictionary#dict" target="blank">doc oficial de Python_</a>
```python
>>> ciudades = { 'Andalucía': 'Sevilla', 'País Vasco': 'Bilbao', 'Baleares':'Palma' }
```

Accediendo a un valor del diccionario:
```python
>>> ciudades = { 'Andalucía': 'Sevilla', 'País Vasco': 'Bilbao', 'Baleares':'Palma' }
>>> print(ciudades['Andalucía'])
Sevilla
```
Obtener el nº de posiciones de una lista:
```python
>>> ciudades = { 'Andalucía': 'Sevilla', 'País Vasco': 'Bilbao', 'Baleares':'Palma' }
>>> len(ciudades)
3
```
Obtener las claves de un diccionario:
```python
>>> ciudades = { 'Andalucía': 'Sevilla', 'País Vasco': 'Bilbao', 'Baleares':'Palma' }
>>> ciudades.keys()
dict_keys(['Andalucía', 'País Vasco', 'Baleares'])
```
Obtener los valores de un diccionario:
```python
>>> ciudades = { 'Andalucía': 'Sevilla', 'País Vasco': 'Bilbao', 'Baleares':'Palma' }
>>> ciudades.values()
dict_values(['Sevilla', 'Bilbao', 'Palma'])
```
Obtener un valor de una clave del diccionario:
```python
>>> print(ciudades.get('Baleares'))
```
Eliminar un valor de una clave del diccionario:
```python
del ciudades['Baleares']

# Esto de volverá None.
print(ciudades.get('Baleares'))
```
Cambiar el valor de una clave del diccionario:
```python
ciudades['Baleares'] = 'Menorca'

# Esto de volverá Menorca.
print(ciudades.get('Baleares'))
```
## Sets
Son un conjunto sin orden de valores encerrados en `{}` que se ordenan cuando se imprimen:
_Más info en la <a href="https://docs.python.org/3.8/library/stdtypes.html#set-types-set-frozenset" target="blank">doc oficial de Python_</a>
```python
>>> marcas_coche = { 'Opel', 'Citröen', 'Tesla' }
>>> print(marcas_coche)
{'Citröen', 'Opel', 'Tesla'}
```
Comparar 2 sets y mostrar los valores no duplicados de ambas listas
```python
>>> marcas_coche = { 'Opel', 'Citröen', 'Tesla' }
>>> marcas_moto = { 'Suzuki', 'Citröen', 'Tesla', 'Yamaha' }
>>> marcas_coche | marcas_moto
{'Citröen', 'Opel', 'Suzuki', 'Tesla', 'Yamaha'}
```
Comparar 2 sets y mostrar los valores duplicados de ambas listas como sin repetirlos.
```python
>>> marcas_coche = { 'Opel', 'Citröen', 'Tesla' }
>>> marcas_moto = { 'Suzuki', 'Citröen', 'Tesla', 'Yamaha' }
>>> marcas_coche & marcas_moto
{'Citröen', 'Tesla'}
```
Comparar 2 sets y mostrar diferencias:
```python
>>> marcas_coche = { 'Opel', 'Citröen', 'Tesla' }
>>> marcas_moto = { 'Suzuki', 'Citröen', 'Tesla', 'Yamaha' }
>>> marcas_coche - marcas_moto
{'Opel'}
>>> marcas_moto - marcas_coche
{'Suzuki', 'Yamaha'}
```
Añadir un conjunto de valores a un set y que queden en primer lugar.
```python
marcas_coche.update([["2","3","4"])
print(marcas_coche)
{2, 3, 4, 'Opel', 'Citröen', 'Tesla'}
```
Añadir un valor al set
```python
marcas_coche.add("Valor")
print(marcas_coche)
{2, 3, 4, 'Opel', 'Citröen', 'Tesla', 'Valor'}
```
Eliminar un valor del set
```python
marcas_coche.remove("Opel")
print(marcas_coche)
{2, 3, 4, 'Citröen', 'Tesla', 'Valor'}
```
Imprimir dos sets en uno:
```python
setA = {1,2,3,4,5}
setB = {6,7,8,9,10}
print(setA|setB)
{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
```
