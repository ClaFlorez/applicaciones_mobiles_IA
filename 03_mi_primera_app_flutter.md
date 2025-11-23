# 🚀 Mi Primera App Flutter — Guía Completa con Arquitectura Sencilla pero Profesional

Esta guía te acompaña **desde el proyecto vacío** hasta una **app funcional** con una arquitectura limpia, ideal para:

- Practicar Flutter desde cero
- Explicar el flujo en tu canal **Claud-IA**
- Publicar el código en **GitHub** con un README profesional

La app ejemplo será una **Lista de Tareas (To-Do)** simple pero bien estructurada: podrás **agregar, marcar como completada y eliminar tareas**.

---

## 1. Objetivo del Proyecto

Construir una app Flutter llamada **Mi Primera App** con:

- Una pantalla principal con lista de tareas
- Botón flotante para agregar nuevas tareas
- Posibilidad de marcar tareas como completadas
- Posibilidad de eliminar tareas
- Arquitectura organizada en:
  - `models/`
  - `providers/`
  - `screens/`
  - `widgets/`

> La idea es que tu primer proyecto ya tenga una estructura escalable, no solo un `main.dart` gigante.

---

## 2. Crear el proyecto Flutter

En tu terminal:

```bash
cd ~/Proyectos        # o la carpeta donde trabajes
flutter create mi_primera_app
cd mi_primera_app
code .                # si usas VS Code
```

Esto te genera la estructura base de Flutter.

---

## 3. Limpiar el proyecto inicial

Por defecto, Flutter crea un demo del contador. Vamos a:

1. Abrir `lib/main.dart`
2. Eliminar el contenido y reemplazarlo por una base limpia que usaremos con nuestra arquitectura.

---

## 4. Estructura de carpetas recomendada

Dentro de `lib/`, crea estas carpetas:

```text
lib/
├── main.dart
├── models/
│   └── task.dart
├── providers/
│   └── task_provider.dart
├── screens/
│   └── home_screen.dart
└── widgets/
    ├── task_list.dart
    └── add_task_dialog.dart
```

En VS Code puedes crear las carpetas desde el explorador o con clic derecho → New Folder.

---

## 5. Configurar `pubspec.yaml` (Provider)

Vamos a usar **provider** para manejo de estado simple.

Abre `pubspec.yaml` y en `dependencies:` agrega:

```yaml
dependencies:
  flutter:
    sdk: flutter

  cupertino_icons: ^1.0.6
  provider: ^6.1.1
```

Luego ejecuta en la terminal:

```bash
flutter pub get
```

---

## 6. `main.dart` — Punto de entrada de la app

Crea o reemplaza `lib/main.dart` con lo siguiente:

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'providers/task_provider.dart';
import 'screens/home_screen.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MultiProvider(
      providers: [
        ChangeNotifierProvider(create: (_) => TaskProvider()),
      ],
      child: MaterialApp(
        debugShowCheckedModeBanner: false,
        title: 'Mi Primera App',
        theme: ThemeData(
          colorScheme: ColorScheme.fromSeed(seedColor: Colors.blue),
          useMaterial3: true,
        ),
        home: const HomeScreen(),
      ),
    );
  }
}
```

Puntos clave:

- `MultiProvider` inyecta el **TaskProvider** en todo el árbol de widgets.
- `home: const HomeScreen()` define la pantalla inicial.

---

## 7. Modelo de datos: `Task`

Crea el archivo `lib/models/task.dart`:

```dart
class Task {
  final String id;
  final String title;
  final bool isCompleted;

  Task({
    required this.id,
    required this.title,
    this.isCompleted = false,
  });

  Task copyWith({
    String? id,
    String? title,
    bool? isCompleted,
  }) {
    return Task(
      id: id ?? this.id,
      title: title ?? this.title,
      isCompleted: isCompleted ?? this.isCompleted,
    );
  }
}
```

- `id`: identificador único (luego podemos usar UUID si queremos).
- `title`: texto de la tarea.
- `isCompleted`: indica si ya se completó.

`copyWith` te permite crear nuevas instancias modificando solo algunos campos (patrón inmutable).

---

## 8. Lógica de negocio: `TaskProvider`

Crea `lib/providers/task_provider.dart`:

```dart
import 'package:flutter/material.dart';
import 'package:uuid/uuid.dart';
import '../models/task.dart';

class TaskProvider with ChangeNotifier {
  final List<Task> _tasks = [];
  final Uuid _uuid = const Uuid();

  List<Task> get tasks => List.unmodifiable(_tasks);

  void addTask(String title) {
    if (title.trim().isEmpty) return;

    final newTask = Task(
      id: _uuid.v4(),
      title: title.trim(),
    );

    _tasks.insert(0, newTask);
    notifyListeners();
  }

  void toggleTask(String id) {
    final index = _tasks.indexWhere((task) => task.id == id);
    if (index == -1) return;

    final task = _tasks[index];
    _tasks[index] = task.copyWith(isCompleted: !task.isCompleted);
    notifyListeners();
  }

  void removeTask(String id) {
    _tasks.removeWhere((task) => task.id == id);
    notifyListeners();
  }

  void clearCompleted() {
    _tasks.removeWhere((task) => task.isCompleted);
    notifyListeners();
  }
}
```

> Nota: agrega la dependencia `uuid` en `pubspec.yaml` si quieres IDs bonitos:

```yaml
dependencies:
  uuid: ^4.3.3
```

Y luego:

```bash
flutter pub get
```

---

## 9. Pantalla principal: `HomeScreen`

Crea `lib/screens/home_screen.dart`:

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import '../providers/task_provider.dart';
import '../widgets/task_list.dart';
import '../widgets/add_task_dialog.dart';

class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});

  @override
  Widget build(BuildContext context) {
    final taskProvider = context.watch<TaskProvider>();
    final totalTasks = taskProvider.tasks.length;
    final completedTasks =
        taskProvider.tasks.where((t) => t.isCompleted).length;

    return Scaffold(
      appBar: AppBar(
        title: const Text('Mi Primera App - To-Do'),
        centerTitle: true,
        actions: [
          IconButton(
            icon: const Icon(Icons.delete_sweep_outlined),
            tooltip: 'Eliminar tareas completadas',
            onPressed: completedTasks == 0
                ? null
                : () {
                    taskProvider.clearCompleted();
                  },
          ),
        ],
      ),
      body: Column(
        children: [
          Padding(
            padding: const EdgeInsets.all(16),
            child: Row(
              mainAxisAlignment: MainAxisAlignment.spaceBetween,
              children: [
                Text(
                  'Total: $totalTasks',
                  style: const TextStyle(fontSize: 16),
                ),
                Text(
                  'Completadas: $completedTasks',
                  style: const TextStyle(fontSize: 16),
                ),
              ],
            ),
          ),
          const Divider(height: 0),
          const Expanded(
            child: TaskList(),
          ),
        ],
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          showDialog(
            context: context,
            builder: (_) => const AddTaskDialog(),
          );
        },
        child: const Icon(Icons.add),
      ),
    );
  }
}
```

Esta pantalla:

- Muestra el resumen (total/completadas).
- Muestra la lista de tareas con `TaskList`.
- Tiene un FAB para abrir el diálogo de nueva tarea.

---

## 10. Widget de lista de tareas: `TaskList`

Crea `lib/widgets/task_list.dart`:

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import '../providers/task_provider.dart';

class TaskList extends StatelessWidget {
  const TaskList({super.key});

  @override
  Widget build(BuildContext context) {
    final taskProvider = context.watch<TaskProvider>();
    final tasks = taskProvider.tasks;

    if (tasks.isEmpty) {
      return Center(
        child: Padding(
          padding: const EdgeInsets.all(24.0),
          child: Text(
            'No tienes tareas todavía.
Toca el botón + para agregar una.',
            textAlign: TextAlign.center,
            style: TextStyle(
              fontSize: 16,
              color: Colors.grey[600],
            ),
          ),
        ),
      );
    }

    return ListView.separated(
      padding: const EdgeInsets.symmetric(horizontal: 8, vertical: 12),
      itemCount: tasks.length,
      separatorBuilder: (_, __) => const Divider(height: 1),
      itemBuilder: (context, index) {
        final task = tasks[index];

        return Dismissible(
          key: ValueKey(task.id),
          direction: DismissDirection.endToStart,
          background: Container(
            color: Colors.red,
            alignment: Alignment.centerRight,
            padding: const EdgeInsets.symmetric(horizontal: 16),
            child: const Icon(Icons.delete, color: Colors.white),
          ),
          onDismissed: (_) {
            taskProvider.removeTask(task.id);
          },
          child: ListTile(
            leading: Checkbox(
              value: task.isCompleted,
              onChanged: (_) => taskProvider.toggleTask(task.id),
            ),
            title: Text(
              task.title,
              style: TextStyle(
                decoration: task.isCompleted
                    ? TextDecoration.lineThrough
                    : TextDecoration.none,
                color: task.isCompleted ? Colors.grey : null,
              ),
            ),
          ),
        );
      },
    );
  }
}
```

Características:

- Muestra mensaje si no hay tareas.
- Cada tarea es **Dismissible** (se puede deslizar para borrar).
- Checkbox para marcar completada/no completada.

---

## 11. Diálogo para agregar tareas: `AddTaskDialog`

Crea `lib/widgets/add_task_dialog.dart`:

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import '../providers/task_provider.dart';

class AddTaskDialog extends StatefulWidget {
  const AddTaskDialog({super.key});

  @override
  State<AddTaskDialog> createState() => _AddTaskDialogState();
}

class _AddTaskDialogState extends State<AddTaskDialog> {
  final _formKey = GlobalKey<FormState>();
  final _controller = TextEditingController();

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  void _submit() {
    if (!_formKey.currentState!.validate()) return;

    final title = _controller.text.trim();
    context.read<TaskProvider>().addTask(title);
    Navigator.of(context).pop();
  }

  @override
  Widget build(BuildContext context) {
    return AlertDialog(
      title: const Text('Nueva tarea'),
      content: Form(
        key: _formKey,
        child: TextFormField(
          controller: _controller,
          autofocus: true,
          decoration: const InputDecoration(
            labelText: 'Descripción de la tarea',
            border: OutlineInputBorder(),
          ),
          validator: (value) {
            if (value == null || value.trim().isEmpty) {
              return 'Por favor escribe una tarea';
            }
            return null;
          },
          onFieldSubmitted: (_) => _submit(),
        ),
      },
      actions: [
        TextButton(
          onPressed: () => Navigator.of(context).pop(),
          child: const Text('Cancelar'),
        ),
        FilledButton(
          onPressed: _submit,
          child: const Text('Agregar'),
        ),
      ],
    );
  }
}
```

---

## 12. Probar la app

En la raíz del proyecto (`mi_primera_app`):

```bash
flutter pub get
flutter run
```

- Abre el emulador o conecta tu dispositivo.
- Verás la lista vacía.
- Pulsa el botón **+** y agrega algunas tareas.
- Marca algunas como completadas.
- Desliza hacia la izquierda para eliminarlas.
- Usa el icono de la papelera en el AppBar para eliminar todas las completadas.

---

## 13. Ideas para tu canal Claud-IA (explicación por capítulos)

Puedes dividir este proyecto en varios videos:

1. **Video 1 — Instalación y creación del proyecto**
   - `flutter create`
   - Explicación de la estructura.
   - Limpieza del `main.dart` inicial.

2. **Video 2 — Arquitectura básica y Provider**
   - Crear carpetas: models, providers, screens, widgets.
   - Explicar `Task`, `TaskProvider` y `MultiProvider`.

3. **Video 3 — UI principal**
   - Construir `HomeScreen`.
   - Mostrar resumen de tareas.
   - ListView básico.

4. **Video 4 — Interacción**
   - Crear `TaskList` y `AddTaskDialog`.
   - Mostrar Dismissible, Checkbox, validación de formularios.

5. **Video 5 — Mejoras y siguientes pasos**
   - Persistir tareas con `shared_preferences` o `Hive`.
   - Agregar tema dark/light.
   - Publicar el código en GitHub.

---

## 14. Siguientes pasos técnicos

- Guardar las tareas localmente (para que no se pierdan al cerrar la app).
- Agregar fechas de creación y orden por fecha.
- Separar rutas y temas en archivos propios.
- Internacionalización (es/en/fr).

---

> Con este mini proyecto, ya tienes una **app real**, con una **estructura cercana a producción**, perfecta para tu portafolio, tu GitHub y tus videos educativos de Claud-IA.
