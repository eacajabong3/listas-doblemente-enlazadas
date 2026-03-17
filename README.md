class Nodo:
    def __init__(self, dato):
        self.dato = dato
        self.siguiente = None
        self.anterior = None


class ListaEnLazadaDoble:
    def __init__(self):
        self.inicio = None
        self.final = None

    def insertar_inicio(self, dato):
        nuevo_nodo = Nodo(dato)
        if self.inicio is None:
            self.inicio = self.final = nuevo_nodo
        else:
             nuevo_nodo.siguiente = self.inicio
             self.inicio.anterior = nuevo_nodo
             self.inicio = nuevo_nodo


    def insertar_final(self, dato):
        nuevo_nodo = Nodo(dato)
        if self.final is None:
            self.inicio = self.final = nuevo_nodo
        else:
            nuevo_nodo.anterior = self.final
            self.final.siguiente = nuevo_nodo
            self.final = nuevo_nodo


    def eliminar(self, dato):
        actual = self.inicio
        while actual:
            if actual.dato == dato:
                if actual.anterior:
                   actual.anterior.siguiente = actual.siguiente
                else:
                   self.inicio = actual.siguiente
                if actual.siguiente:
                   actual.siguiente.anterior = actual.anterior
                else:
                   self.final = actual.anterior
                return True
            actual = actual.siguiente
        return False


    def mostrar(self):
        actual = self.inicio
        while actual:
            print(actual.dato, end=' -> ')
            actual = actual.siguiente


    def mostrar_inverso(self):
        actual = self.final
        while actual:
            print(actual.dato, end=' <- ')
            actual = actual.anterior


    def insertar_en_posicion(self, dato, posicion):
        nuevo_nodo = Nodo(dato)
        actual = self.inicio
        for _ in range(posicion - 1):
            if actual is None:
                return False
            actual = actual.siguiente
        nuevo_nodo.siguiente = actual.siguiente
        nuevo_nodo.anterior = actual
        if actual.siguiente:
            actual.siguiente.anterior = nuevo_nodo
        actual.siguiente = nuevo_nodo
        return True


    def modificar_posicion(self, nuevo_dato, posicion):
        actual = self.inicio
        for _ in range(posicion - 1):
            if actual is None:
                return False
            actual = actual.siguiente
        actual.dato = nuevo_dato
        return True

    def vaciar(self):
        self.inicio= None
        self.final = None

    def ordenar_descendente(self):
        datos = []
        actual = self.inicio
        while actual:
            datos.append(actual.dato)
            actual = actual.siguiente
        datos.sort(reverse=True)
        self.vaciar()
        for d in datos:
            self.insertar_final(d)


    def ordenar_ascendente(self):
        datos = []
        actual = self.inicio
        while actual:
            datos.append(actual.dato)
            actual = actual.siguiente
        datos.sort()
        self.vaciar()
        for d in datos:
            self.insertar_final(d)


    def sumar_datos(self):
        total = 0
        actual = self.inicio
        while actual:
            total += actual.dato
            actual = actual.siguiente
        return total


    def insertar_despues(self, dato_buscando, nuevo_dato):
        actual = self.inicio
        while actual:
            if actual.dato == dato_buscando:
                nuevo= Nodo(nuevo_dato)
                nuevo.siguiente = actual.siguiente
                nuevo.anterior = actual
                if actual.siguiente:
                    actual.siguiente.anterior = nuevo
                else:
                    self.final = nuevo
                actual.siguiente = nuevo
                return True
            actual = actual.siguiente
        return False


if __name__ == "__main__":
    lista = ListaEnLazadaDoble()
    lista.insertar_inicio(40)
    lista.insertar_inicio(50)
    lista.insertar_final(33)
    lista.insertar_final(98)
    lista.mostrar()

    lista.insertar_despues(50, 120)
    lista.mostrar()

    lista.mostrar_inverso()

    print("suma", lista.sumar_datos())

    lista.ordenar_descendente()
    lista.mostrar()
