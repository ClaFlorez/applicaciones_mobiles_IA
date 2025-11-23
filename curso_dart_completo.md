# Curso Completo de Dart — Para estudiantes que ya dominan Python

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

Exercice Récapitulatif Final
Contexte: Vous devez créer un programme de gestion de notes d'étudiants.

Cahier des charges
1. Créez une liste de 5 notes (nombres décimaux entre 0 et 20)
2. Calculez et affichez:
   - La moyenne des notes
   - La note la plus élevée
   - La note la plus basse
   - Le nombre de notes >= 10
3.Pour chaque note, affichez: - Le numéro de la note (1, 2, 3, etc.)
   - La valeur de la note - Une appréciation selon le barème:
     por >= 16: "Excellent" por >= 14: "Très bien" por >= 12: "Bien" por >= 10: "Assez bien" por < 10: "Insuffisant"  
4.Déterminez et affichez la mention finale selon la moyenne:
  - >= 16: "Mention Très Bien"
  - >= 14: "Mention Bien"
  - >= 12: "Mention Assez Bien"
  - >= 10: "Mention Passable"
  - < 10: "Non admis"
5. Utilisez les concepts suivants:
  - Variables (int, double, String, List)
  - Boucles (for ou for-in)
  - Conditions (if-else if-else ou switch)
  - Opérateurs (arithmétiques, comparaison)
  - Interpolation de chaînes

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

=== Análisis de notas ===

Nota 1: 15.5 - Muy bien
Nota 2: 12.0 - Bien
Nota 3: 18.5 - Excelente
Nota 4: 9.5 - Insuficiente
Nota 5: 14.0 - Muy bien

=== Estadísticas ===
Media: 13.90
Nota máxima: 18.50
Nota mínima: 9.50
Número de notas ≥ 10: 4

=== Resultado final ===
Mención: Mención Aceptable

---

## Parte 9 — Practicas 

void main() {
  // ---------------------------------------------------------
  // 1. VARIABLES NULLABLES
  // ---------------------------------------------------------

  // En Dart, una variable con ? puede contener null.
  // Esto es útil cuando no sabemos si tendrá valor.
  String? x = null;

  // Imprime el valor actual de x (aquí será null)
  print('The value of x is: $x');

  // Verificamos si x es null
  if (x == null) {
    print('x est null');
  }

  // ---------------------------------------------------------
  // 2. LISTAS EN DART (List<T>)
  // ---------------------------------------------------------

  // Declaración de una lista de enteros
  List<int> nombres = [1, 2, 3, 4, 5];

  // Lista vacía de enteros
  // List<int> vide = [];

  // Lista dinámica simple (mezcla de tipos)
  List<dynamic> mixteSimple = [1, 'texte', true];

  // ---------------------------------------------------------
  // 3. ACCEDER A LOS ELEMENTOS
  // ---------------------------------------------------------

  // Primer elemento (posición 0)
  print(nombres[0]); // → 1

  // Último elemento usando length - 1
  print(nombres[nombres.length - 1]); // → 5

  // ---------------------------------------------------------
  // 4. MODIFICAR UNA LISTA
  // ---------------------------------------------------------

  nombres.add(6);
  // Resultado: [1, 2, 3, 4, 5, 6]

  nombres.insert(0, 0);
  // Inserta 0 al inicio: [0, 1, 2, 3, 4, 5, 6]

  nombres.remove(3);
  // Elimina el *valor* 3 (la primera aparición)

  nombres.removeAt(0);
  // Elimina el elemento en el índice 0 (el primer elemento)

  // ---------------------------------------------------------
  // 5. PROPIEDADES Y MÉTODOS ÚTILES
  // ---------------------------------------------------------

  print('Longueur: ${nombres.length}');
  // Muestra cuántos elementos hay ahora

  nombres.sort();
  // Ordena la lista en orden ascendente

  nombres = nombres.reversed.toList();
  // Invierte el orden de la lista (reversed devuelve un iterable)

  // ---------------------------------------------------------
  // 6. CREAR UNA SUBLISTA
  // ---------------------------------------------------------

  // sublist(inicio, fin) -> fin NO es incluido
  var sousListe = nombres.sublist(1, 4);

  print('Sous-liste: $sousListe');
  print('Contenu: $nombres');

  // ---------------------------------------------------------
  // 7. OTRO EJEMPLO SIMPLE DE LISTA
  // ---------------------------------------------------------

  List<int> nombresIns = [1, 2, 3, 4, 5];

  nombresIns.add(6); // Añadimos un valor al final
  nombresIns.insert(5, 10); // Insertamos un valor al inicio

  print('Longueur (nombresIns): ${nombresIns.length}');
  print('Contenu (nombresIns): $nombresIns');

  // ---------------------------------------------------------
  // 8. LISTA DINÁMICA COMPLETA (EJEMPLO AVANZADO)
  // ---------------------------------------------------------

  List<dynamic> mixte = [
    1, // Entero
    'texte', // String
    true, // Booleano
    3.14, // Double
    {'nom': 'Ana'}, // Mapa
    [1, 2, 3], // Lista interna
  ];

  print("\nContenido de la lista dinámica:");
  print(mixte);

  // Acceder a elementos individuales
  print("\nAcceso individual:");
  print("Elemento 0 (int): ${mixte[0]}");
  print("Elemento 1 (string): ${mixte[1]}");
  print("Elemento 2 (bool): ${mixte[2]}");
  print("Elemento 3 (double): ${mixte[3]}");
  print("Elemento 4 (map - nom): ${mixte[4]['nom']}"); // Acceso dentro del mapa
  print(
    "Elemento 5 (lista interna): ${mixte[5][1]}",
  ); // Acceso dentro de la lista

  // Agregar un nuevo tipo (objeto DateTime)
  mixte.add(DateTime.now());

  // Modificar un valor
  mixte[1] = "modificado";

  print("\nDespués de modificaciones:");
  print(mixte);
  //  print(vide);
  print(mixteSimple);

  // dictionarios
  print("\n **** Diccionarios ****");
  // Création
  Map<String, dynamic> personne = {'nom': 'Alice', 'age': 25, 'ville': 'Paris'};
  Map<String, String> vide = {};
  // Accès
  print(personne['nom']);
  // Modification
  personne['age'] = 26;
  personne['email'] = 'alice@mail.com';

  // Suppression
  personne.remove('ville');

  // Propriétés et méthodes
  print(personne.length);
  print(personne.keys);
  print(personne.values);

  print("\n **** Diccionarios Manipulation de Maps ****");
  Map<String, dynamic> livre = {
    'titre': 'Le Petit Prince',
    'auteur': 'Saint-Exupéry',
    'annee': 1943,
  };
  livre['disponible'] = true;

  print('Clés: ${livre.keys}');

  print("\n **** Manipulation de Null ****");
  int? y;

  print("Antes: $y"); // null

  y ??= 5;
  print("Después: $y"); // 5

  y ??= 100;
  print("Intento de reasignación: $y"); // sigue siendo 5

  print("\n **** Manipulation opération arithmétiques ****");

  // Variables de départ
  int a = 10;
  int b = 3;

  // ----------------------------
  // 1. Addition
  // ----------------------------
  var addition = a + b; // 10 + 3 = 13
  print("Addition: $addition");

  // ----------------------------
  // 2. Soustraction
  // ----------------------------
  var soustraction = a - b; // 10 - 3 = 7
  print("Soustraction: $soustraction");

  // ----------------------------
  // 3. Multiplication
  // ----------------------------
  var multiplication = a * b; // 10 * 3 = 30
  print("Multiplication: $multiplication");

  // ----------------------------
  // 4. Division (résultat double)
  // ----------------------------
  double division = a / b; // 10 / 3 = 3.333...
  print("Division: $division");

  // ----------------------------
  // 5. Division entière (~/)
  // ----------------------------
  int divEntiere = a ~/ b; // 10 ~/ 3 = 3
  print("Division entière: $divEntiere");

  // ----------------------------
  // 6. Modulo (%)
  // ----------------------------
  // Reste de la division
  int modulo = a % b; // 10 % 3 = 1
  print("Modulo: $modulo");

  // ----------------------------
  // 7. Incrément / Décrément
  // ----------------------------

  int t = 5;

  print(t);

  t++; // Post-incrément: utilise x puis ajoute 1
  print("x après x++ : " + t.toString());

  ++t; // Pré-incrément: ajoute 1 AVANT d'utiliser x
  print("x après ++x : " + t.toString());

  t--; // Post-décrément
  print("x après x-- : " + t.toString());

  --t; // Pré-décrément
  print("x après --x : " + t.toString());

  // ----------------------------
  // 8. Puissance (pow)
  // ----------------------------
  // Nécessite : import 'dart:math'
  // pow(a, b) -> a^b (a puissance b)
  //
  // Exemple:
  // var puissance = pow(2, 3);  // 8

  t--; // Post-décrément
  print("x après x-- : $t");

  --t; // Pré-décrément
  print("x après --x : $t");

  // ----------------------------
  // 8. Puissance (pow)
  // ----------------------------
  // Nécessite : import 'dart:math'
  // pow(a, b) -> a^b (a puissance b)
  //
  // Exemple:
  // var puissance = pow(2, 3);  // 8

  int z = 3;

  z = z++ + ++z;
  print(z);
}
---
