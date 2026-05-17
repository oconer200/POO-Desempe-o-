''' EJERCICIO 1
 Crea una clase abstracta Animal con los atributos nombre y especie, y dos métodos abstractos:
 emitir_sonido() y moverse().
 Crea una subclase Perro que herede de Animal e implemente ambos métodos (ej: emite "Guau" y se mueve "corriendo en cuatro patas").
 Instancia dos perros con nombres distintos e invoca sus métodos en cada objeto.'''

from abc import ABC, abstractmethod

class Animal(ABC):

    def __init__(self, nombre, especie):
        self.nombre = nombre
        self.especie = especie

    @abstractmethod
    def emitir_sonido(self):
        pass

    @abstractmethod
    def moverse(self):
        pass

class Perro(Animal):
    def emitir_sonido(self):
        return f"{self.nombre} emite Guau!"

    def moverse(self):
        return f"{self.nombre} esta corriendo en 4 patas"

perro1 = Perro("Elias","Canis")
perro2 = Perro("Fido","Canis")

print(perro1.emitir_sonido())
print(perro1.moverse())
print(perro2.emitir_sonido())
print(perro2.moverse())


''' EJERCICIO 2 
Crea una clase abstracta CuentaBancaria con los atributos titular y saldo, y dos métodos
abstractos: cobrar_comision() y mostrar_info(). Crea dos subclases: CuentaAhorros (sin
comisión, genera rendimiento del 2% sobre el saldo) y CuentaCorriente (cobra comisión fija de
$8.000). Cada subclase hereda e implementa ambos métodos. Instancia una cuenta de cada tipo
y pruébalas.'''



