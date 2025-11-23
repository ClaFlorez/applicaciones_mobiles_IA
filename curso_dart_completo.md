# Curso Completo de Dart — Para estudiantes que ya dominan Python

(Basado en el PDF original subido)

## Parte 1 — Introducción a Dart y Flutter

### 1.1 ¿Qué es Dart?
Dart es un lenguaje multiplataforma optimizado por Google para crear aplicaciones móviles, web, escritorio y backend desde una sola base de código.

### 1.2 ¿Qué es Flutter?
Framework de Google basado en Dart para crear interfaces modernas, fluidas y multiplataforma.

### 1.3 Similitudes con Python
- Sintaxis clara  
- Colecciones poderosas  
- Fácil curva de aprendizaje  

### 1.4 Diferencias importantes
- Dart es tipado estático  
- Null safety obligatorio  
- Llaves y punto y coma  

---

## Parte 2 — Fundamentos del Lenguaje

### 2.1 main()
```dart
void main() {
  print("Hola Mundo");
}
```

### 2.2 Comentarios
```dart
// Comentario simple
/* Comentario multilínea */
/// Comentario de documentación
```

### 2.3 print y cadenas
```dart
var nombre = "Claudia";
print("Hola " + nombre);
print("Hola $nombre");
```

---

## Parte 3 — Tipos de Datos

### 3.1 Variables
```dart
var edad = 25;
int x = 10;
String texto = "Hola";
```

### 3.2 final y const
```dart
final fecha = DateTime.now();
const pi = 3.1416;
```

### 3.3 Strings
```dart
String s = "Hola";
print(s.length);
```

### 3.4 int y double
```dart
int a = 10;
double b = 5.5;
```

### 3.5 Booleanos
```dart
bool activo = true;
```

### 3.6 dynamic
```dart
dynamic v = 10;
v = "texto";
```

### 3.7 Null safety
```dart
String? nombre = null;
var x = nombre ?? "Sin nombre";
```

### 3.8 late
```dart
late String titulo;
titulo = "Curso Dart";
```

---

## Parte 4 — Colecciones

### 4.1 List
```dart
List<int> numeros = [1,2,3];
numeros.add(4);
```

### 4.2 Map
```dart
Map<String,int> edades = {"Ana":20};
```

### 4.3 Set
```dart
Set<int> valores = {1,2,3};
```

---

## Parte 5 — Operadores

### 5.1 Aritméticos
```dart
10 + 3;
10 - 3;
10 * 3;
10 / 3;
10 ~/ 3;
10 % 3;
```

### 5.2 Incrementos
```dart
int x = 5;
x++;
++x;
x--;
--x;
```

### 5.3 Comparación
```dart
a == b;
a != b;
a > b;
```

### 5.4 Lógicos
```dart
&&, ||, !
```

### 5.5 Ternario
```dart
var r = edad >= 18 ? "Adulto" : "Menor";
```

### 5.6 Null aware
```dart
nombre ?? "Anónimo";
nombre ??= "Default";
valor?.length;
```

---

## Parte 6 — Control de Flujo

### 6.1 if / else
```dart
if (x > 10) print("Mayor");
else print("Menor");
```

### 6.2 switch
```dart
switch(dia){
  case 1: print("Lunes");
}
```

### 6.3 Bucles
```dart
for(int i=0; i<5; i++) print(i);

for(var n in numeros) print(n);

while(x<5){ x++; }
```

---

## Parte 7 — Funciones (Intro)
```dart
int sumar(int a, int b){
  return a + b;
}
```

---

## Parte 8 — Ejercicio Final: Gestión de Notas

Código completo basado en el enunciado:

```dart
void main() {
  List<double> notas = [15.5, 12.0, 18.5, 9.5, 14.0];

  double suma = 0;
  double notaMax = notas[0];
  double notaMin = notas[0];
  int aprobadas = 0;

  for (var nota in notas) {
    suma += nota;
    if (nota > notaMax) notaMax = nota;
    if (nota < notaMin) notaMin = nota;
    if (nota >= 10) aprobadas++;
  }

  double media = suma / notas.length;

  print('=== Análisis de notas ===\n');

  for (int i = 0; i < notas.length; i++) {
    double nota = notas[i];
    String apreciacion;

    if (nota >= 16) {
      apreciacion = 'Excelente';
    } else if (nota >= 14) {
      apreciacion = 'Muy bien';
    } else if (nota >= 12) {
      apreciacion = 'Bien';
    } else if (nota >= 10) {
      apreciacion = 'Aceptable';
    } else {
      apreciacion = 'Insuficiente';
    }

    print('Nota ${i + 1}: ${nota.toStringAsFixed(1)} - ' + apreciacion);
  }

  print('\n=== Estadísticas ===');
  print('Media: ${media.toStringAsFixed(2)}');
  print('Nota máxima: ${notaMax.toStringAsFixed(2)}');
  print('Nota mínima: ${notaMin.toStringAsFixed(2)}');
  print('Número de notas ≥ 10: $aprobadas');

  print('\n=== Resultado final ===');
  String mencion;

  if (media >= 16) mencion = 'Mención Muy Bien';
  else if (media >= 14) mencion = 'Mención Bien';
  else if (media >= 12) mencion = 'Mención Aceptable';
  else if (media >= 10) mencion = 'Mención Suficiente';
  else mencion = 'No admitido';

  print('Mención: ' + mencion);
}
```

---

## Parte 9 — Próximos pasos
- Clases y objetos  
- async/await  
- Flutter Widgets  
- Manejo de estado  
- Integración de API  
- Persistencia local  

---

_Este archivo está listo para GitHub y para utilizarlo en tu repositorio de aprendizaje de Dart._
