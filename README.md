import sys

class Estudiante:
    def __init__(self, doc, nom, ape):
        self.documento = doc
        self.nombres = nom
        self.apellidos = ape

    def __str__(self):
        return f"Documento: {self.documento}, Nombres: {self.nombres}, Apellidos: {self.apellidos}"

class Curso:
    def __init__(self, codigo, nombre):
        self.codigo = codigo
        self.nombre = nombre
        self.estudiantes = []

    def adicionar_estudiante(self, estudiante):
        self.estudiantes.append(estudiante)

    def __str__(self):
        estudiantes_str = "\n  ".join(str(est) for est in self.estudiantes)
        return f"Curso: {self.codigo} - {self.nombre}\nEstudiantes:\n  {estudiantes_str if estudiantes_str else 'Sin estudiantes'}"

class Pila:
    def __init__(self):
        self.items = []

    def isEmpty(self):
        return self.items == []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        return self.items.pop() if not self.isEmpty() else None

    def list_items(self):
        return self.items[::-1]

class Queue:
    def __init__(self):
        self.items = []

    def isEmpty(self):
        return self.items == []

    def enqueue(self, item):
        self.items.insert(0, item)

    def dequeue(self):
        return self.items.pop() if not self.isEmpty() else None

    def list_items(self):
        return self.items[::-1]

def main():
    pila_cursos = Pila()
    cola_cursos = Queue()

    while True:
        opc = input("************Sistema de Gestión de Cursos***************\n" +
                    "1. Adicionar un curso a la pila" +
                    "\n2. Adicionar un estudiante a un curso en la pila" +
                    "\n3. Sacar un curso de la pila y mostrar sus datos" +
                    "\n4. Listar todos los cursos de la pila sin sacarlos" +
                    "\n5. Adicionar un curso a la cola" +
                    "\n6. Sacar un curso de la cola y mostrar sus datos" +
                    "\n7. Listar todos los cursos de la cola sin sacarlos" +
                    "\n8. Salir" +
                    "\nSeleccione la opción que desea: ")

        if opc == "1":
            codigo = input("Ingrese el código del curso: ")
            nombre = input("Ingrese el nombre del curso: ")
            curso = Curso(codigo, nombre)
            pila_cursos.push(curso)
            print("Curso añadido a la pila.")

        elif opc == "2":
            if pila_cursos.isEmpty():
                print("La pila de cursos está vacía.")
            else:
                print("Cursos en la pila:")
                for i, curso in enumerate(pila_cursos.list_items(), 1):
                    print(f"{i}. {curso.codigo} - {curso.nombre}")
                num = int(input("Seleccione el curso por número: ")) - 1
                if 0 <= num < len(pila_cursos.items):
                    doc = input("Ingrese el documento del estudiante: ")
                    nom = input("Ingrese los nombres del estudiante: ")
                    ape = input("Ingrese los apellidos del estudiante: ")
                    estudiante = Estudiante(doc, nom, ape)
                    pila_cursos.items[num].adicionar_estudiante(estudiante)
                    print("Estudiante añadido al curso en la pila.")
                else:
                    print("Número de curso no válido.")

        elif opc == "3":
            curso = pila_cursos.pop()
            if curso:
                print("Curso sacado de la pila: ", curso)
            else:
                print("La pila de cursos está vacía.")

        elif opc == "4":
            print("Cursos en la pila:")
            for curso in pila_cursos.list_items():
                print(curso)

        elif opc == "5":
            codigo = input("Ingrese el código del curso: ")
            nombre = input("Ingrese el nombre del curso: ")
            curso = Curso(codigo, nombre)
            cola_cursos.enqueue(curso)
            print("Curso añadido a la cola.")

        elif opc == "6":
            curso = cola_cursos.dequeue()
            if curso:
                print("Curso sacado de la cola: ", curso)
            else:
                print("La cola de cursos está vacía.")

        elif opc == "7":
            print("Cursos en la cola:")
            for curso in cola_cursos.list_items():
                print(curso)

        elif opc == "8":
            print("Saliendo del programa...")
            break

        else:
            print("Opción no válida, por favor seleccione una opción correcta.")

if __name__ == "__main__":
    sys.exit(main())
