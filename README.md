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

from abc import ABC, abstractmethod

class CuentaBancaria(ABC):
    def __init__(self, titular, saldo):
        self.titular = titular
        self.saldo = saldo

    @abstractmethod
    def cobrar_comision(self):
        pass

    @abstractmethod
    def mostrar_info(self):
        pass

class CuentaAhorros(CuentaBancaria):
    def cobrar_comision(self):
        rendimiento = self.saldo * 0.02
        self.saldo += rendimiento
        print(f"Señor {self.titular} su rendimiento es de: {rendimiento}")

    def mostrar_info(self):
        print(f"Señor {self.titular} su saldo actual: {self.saldo}")

class CuentaCorriente(CuentaBancaria):
    def cobrar_comision(self):
        comision = 8000
        self.saldo -= comision
        print(f"Señor {self.titular} se ha cobrado una comisión de: {comision}")

    def mostrar_info(self):
        print(f"Señor {self.titular} su saldo actual: {self.saldo}")


cuenta1 = CuentaAhorros("Pedro", 100000)
cuenta2 = CuentaCorriente("Thomas", 100000)

cuenta1.mostrar_info()
cuenta1.cobrar_comision()
cuenta1.mostrar_info()
cuenta2.mostrar_info()
cuenta2.cobrar_comision()
cuenta2.mostrar_info()




''' EJERCICIO 3
Crea una clase Contrato (tipo, fecha_inicio, duracion_meses). Crea una clase abstracta
Trabajador con atributos nombre y contrato (objeto Contrato), y métodos abstractos
y EmpleadoTemporal (tarifa_dia x dias_trabajados). Cada subclase hereda de Trabajador, recibe
un objeto Contrato e implementa ambos métodos. Instancia uno de cada tipo y genera sus
reportes completos.'''


from abc import ABC, abstractmethod

class Contrato:
    def __init__(self, tipo, fecha_inicio, duracion_meses):
        self.tipo = tipo
        self.fecha_inicio = fecha_inicio
        self.duracion_meses = duracion_meses

class Trabajador(ABC):
    def __init__(self, nombre, contrato_objeto):
        self.nombre = nombre
        self.contrato = contrato_objeto

    @abstractmethod
    def calcular_salario(self):
        pass

    @abstractmethod
    def generar_reporte(self):
        pass

class EmpleadoFijo(Trabajador):
    def __init__(self,nombre, contrato_objeto,salario_base):
        super().__init__(nombre,contrato_objeto)
        self.salaio_base = salario_base

    def calcular_salario(self):
        return f"Empleado {self.nombre} su salario es {self.salaio_base}"

    def generar_reporte(self):
        return f"Empleado: {self.nombre} \nTipo: {self.contrato.tipo}\nDuración:{self.contrato.duracion_meses} meses \nSalario: {self.salaio_base}"

class Empleadotemporal(Trabajador):
    def __init__(self,nombre,contrato_objeto,tarifa,dias_trabajados):
        super().__init__(nombre,contrato_objeto)

        self.tarifa = tarifa
        self.dias_trabajados = dias_trabajados

    def calcular_salario(self):
        return f"Empleado {self.nombre} su salario es {self.tarifa * self.dias_trabajados}"

    def generar_reporte(self):
        salario = self.calcular_salario()
        return f"Empleado;{self.nombre} \nTipo:{self.contrato.tipo}\nDuración:{self.contrato.duracion_meses} meses\nDias trabajados: {self.dias_trabajados} \nPago total:{salario}"

comtrato_F = Contrato("Fijo","29-03-2026",72)
jair = EmpleadoFijo("Jair Dario",comtrato_F,12000000)

contrato_T = Contrato("Temporal","04-04-2026",32)
juan = Empleadotemporal("Juan Miguel",contrato_T, 108340,12 )

print("*REPORTES EMPLEADO FIJO Y TEMPORAL*")
print(jair.generar_reporte())
print("------------------------")
print(juan.generar_reporte())


