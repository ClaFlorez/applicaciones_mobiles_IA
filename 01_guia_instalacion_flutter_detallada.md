# 🧭 Guía detallada para instalar, configurar y crear tu primera app Flutter (desde cero)

Esta guía está pensada como referencia **paso a paso**, al estilo de un desarrollador senior: concreta, ordenada y sin relleno.  
Te lleva desde **cero instalación** hasta tener una **app Flutter corriendo en un emulador o dispositivo físico**.

---

## 0. Requisitos previos

Antes de instalar Flutter, asegúrate de tener:

- Un sistema operativo compatible:
  - **Windows 10/11** (64 bits)
  - **macOS** (Intel o Apple Silicon)
  - **Linux** (distribución moderna, 64 bits)
- Al menos **8 GB de RAM** (recomendado 16 GB si vas a usar emuladores).
- Espacio en disco: mínimo **10–15 GB libres** para SDKs, emuladores, etc.
- Conexión a Internet estable.

Opcional pero muy recomendable:
- Una cuenta de Google (para Play Store).
- Una cuenta de Apple (si piensas compilar para iOS).

---

## 1. Descargar e instalar Flutter SDK

La instalación de Flutter siempre empieza descargando el **SDK** y configurando el **PATH** para poder usar el comando `flutter` en la terminal.

> 💡 Consejo: siempre usa el **canal stable**, a menos que tengas una razón fuerte para usar beta o master.

---

### 1.1. Instalación en Windows

1. Crea una carpeta para tus herramientas, por ejemplo:
   - `C:\src`

2. Descarga el archivo `.zip` de Flutter (canal stable) desde la web oficial y guárdalo en `C:\src`.

3. Extrae el zip en `C:\src`, te quedará algo como:
   - `C:\src\flutter`

4. Configura la variable de entorno **PATH**:

   - Abre: **Panel de control → Sistema → Configuración avanzada del sistema → Variables de entorno**.
   - En *Variables del sistema* busca `Path` → **Editar**.
   - Agrega una nueva entrada:
     - `C:\src\flutter\bin`

5. Cierra todas las terminales abiertas y abre **PowerShell** o **CMD** nuevo.

6. Verifica la instalación:

   ```bash
   flutter --version
   ```

   Si ves la versión de Flutter, el PATH está bien configurado.

---

### 1.2. Instalación en macOS

1. Crea una carpeta para herramientas, por ejemplo:

   ```bash
   mkdir -p $HOME/development
   cd $HOME/development
   ```

2. Clona el repo de Flutter (canal stable):

   ```bash
   git clone https://github.com/flutter/flutter.git -b stable
   ```

3. Agrega Flutter al PATH (si usas `zsh`):

   ```bash
   echo 'export PATH="$PATH:$HOME/development/flutter/bin"' >> ~/.zshrc
   source ~/.zshrc
   ```

   Si usas `bash`:

   ```bash
   echo 'export PATH="$PATH:$HOME/development/flutter/bin"' >> ~/.bash_profile
   source ~/.bash_profile
   ```

4. Verifica:

   ```bash
   flutter --version
   ```

---

### 1.3. Instalación en Linux

1. Crea una carpeta para herramientas:

   ```bash
   mkdir -p $HOME/development
   cd $HOME/development
   ```

2. Clona Flutter (stable):

   ```bash
   git clone https://github.com/flutter/flutter.git -b stable
   ```

3. Agrega Flutter al PATH en `~/.bashrc` o `~/.zshrc`:

   ```bash
   echo 'export PATH="$PATH:$HOME/development/flutter/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

4. Verifica:

   ```bash
   flutter --version
   ```

---

## 2. Ejecutar `flutter doctor` y resolver dependencias

Una vez que el comando `flutter` funciona, el siguiente paso SIEMPRE es:

```bash
flutter doctor
```

Este comando te mostrará un resumen del estado de tu entorno:

- ✅ Flutter SDK
- ⚠️ Android toolchain
- ⚠️ Xcode (si estás en macOS)
- ⚠️ Chrome (para Flutter Web)
- ⚠️ Android Studio / VS Code
- ⚠️ Dispositivos conectados

Tu objetivo es ir dejando todo en **[✓]** o al menos tener:

- Flutter ✅
- Android toolchain ✅
- Un editor (VS Code o Android Studio) ✅
- Algún dispositivo/emulador disponible ✅

Cada línea con error o warning suele decirte qué falta instalar.

---

## 3. Instalar herramientas de desarrollo móviles

### 3.1. Android Studio (para Android)

Instala Android Studio en **Windows, macOS o Linux**:

1. Descarga Android Studio desde la web oficial e instálalo.
2. Durante la instalación, asegúrate de incluir:
   - **Android SDK**
   - **Android SDK Platform-Tools**
   - **Android Emulator**

3. Una vez instalado, abre Android Studio y:
   - Ve a **More Actions → SDK Manager**.
   - Instala al menos:
     - Una versión reciente de **Android SDK** (ej. API 33+).
     - **Android SDK Build-Tools**.
   - Ve a **Device Manager** y crea un **emulador** (ej. Pixel 5, API 33).

4. Vuelve a la terminal y corre:

   ```bash
   flutter doctor --android-licenses
   ```

   Acepta todas las licencias escribiendo `y` cuando lo pida.

5. Verifica nuevamente:

   ```bash
   flutter doctor
   ```

Deberías ver algo como:

```text
[✓] Android toolchain - develop for Android devices
[✓] Android Studio
```

---

### 3.2. Xcode (para iOS, solo macOS)

Si quieres compilar para iOS, en macOS:

1. Instala **Xcode** desde la App Store.
2. Acepta la licencia:

   ```bash
   sudo xcodebuild -license
   ```

3. Selecciona la versión activa de Xcode:

   ```bash
   sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
   ```

4. Instala herramientas de línea de comando (si te las pide).

5. Verifica:

   ```bash
   flutter doctor
   ```

Debe aparecer algo como:

```text
[✓] Xcode - develop for iOS and macOS
```

> ⚠️ Para publicar en App Store necesitarás también una **cuenta de desarrollador de Apple**.

---

## 4. Elegir y configurar el editor de código

Puedes trabajar con:

### 4.1. VS Code (recomendado para empezar)

1. Instala **Visual Studio Code**.
2. Abre VS Code → pestaña **Extensions**.
3. Instala:
   - **Flutter** (extensión oficial)
   - **Dart** (si no se instaló automáticamente)

Estas extensiones te dan:

- Autocompletado
- Snippets
- Depuración integrada
- Comandos rápidos para crear/ejecutar proyectos Flutter

---

### 4.2. Android Studio (opción más pesada, pero completa)

Android Studio también trae soporte para Flutter:

1. Abre Android Studio → **Plugins**.
2. Instala:
   - Plugin **Flutter**.
   - Te pedirá instalar el plugin **Dart** también.

Puedes crear proyectos Flutter desde el propio Android Studio.

---

## 5. Crear tu primer proyecto Flutter

En cualquier sistema operativo, el flujo base es el mismo.

### 5.1. Crear el proyecto

En una terminal, ve a la carpeta donde quieras tus proyectos y ejecuta:

```bash
cd ~/Proyectos      # o la ruta que prefieras
flutter create mi_primer_app
cd mi_primer_app
```

Este comando genera una estructura inicial tipo:

```text
mi_primer_app/
├── android/
├── ios/
├── lib/
│   └── main.dart
├── test/
├── web/ (si está habilitado)
├── pubspec.yaml
└── ...
```

Los archivos más importantes al inicio:

- `lib/main.dart` → punto de entrada de la app.
- `pubspec.yaml` → dependencias, assets, nombre del proyecto.

---

## 6. Ejecutar la app en un emulador o dispositivo físico

### 6.1. Comprobar dispositivos disponibles

```bash
flutter devices
```

Puedes ver:

- Emuladores Android
- Dispositivos físicos conectados por USB
- Simuladores iOS (macOS)
- Chrome/Web (si tienes habilitado Flutter Web)

### 6.2. Levantar un emulador Android

- Desde Android Studio → **Device Manager → Play** sobre el emulador.
- O por línea de comando (si usas `emulator` de Android SDK).

Cuando el emulador esté encendido, verifica:

```bash
flutter devices
```

Debe listar el emulador.

### 6.3. Ejecutar la app

Con un dispositivo o emulador disponible:

```bash
flutter run
```

- Compilará la app
- La instalará en el dispositivo seleccionado
- Abrirá la app con la pantalla inicial de Flutter

**Hot reload:** con la app corriendo y la terminal activa, presiona:
- `r` → **hot reload** (cambia código y recarga rápido)
- `R` → **hot restart** (reinicia el estado)

---

## 7. Modificar la app inicial (test rápido de que todo funciona)

Abre `lib/main.dart` en tu editor y localiza el `Text('Flutter Demo Home Page')`.  
Cámbialo por algo como:

```dart
Text(
  'Hola, Claud-IA 🚀',
  style: TextStyle(fontSize: 24),
)
```

Guarda el archivo.  
Si estás usando `flutter run` con hot reload, presiona `r` en la terminal y verás el cambio al instante.

Esto confirma que:
- El entorno funciona
- El hot reload está operativo
- Tu editor y Flutter están bien conectados

---

## 8. Configuración de modo debug y release

### 8.1. Modo debug (por defecto)

- Más lento
- Incluye herramientas de desarrollo
- Ideal mientras estás programando

Ejecutar (es lo que hace `flutter run` por defecto):

```bash
flutter run --debug
```

### 8.2. Modo release (para pruebas de rendimiento / distribución)

- Código optimizado
- Sin herramientas de debug
- Peso de app menor

Para Android (APK release):

```bash
flutter build apk --release
```

Esto genera un APK en:

```text
build/app/outputs/flutter-apk/app-release.apk
```

Para Android App Bundle (para Play Store):

```bash
flutter build appbundle --release
```

Para iOS (requiere Xcode y cuenta Apple):

```bash
flutter build ios --release
```

---

## 9. Problemas típicos y soluciones rápidas

### 9.1. `flutter` no se reconoce como comando

- Verifica PATH:
  - Windows: revisa que `C:\src\flutter\bin` esté en Variables de entorno.
  - macOS/Linux: confirma que agregaste la línea correcta en `.bashrc`, `.zshrc` o `.bash_profile`.
- Cierra y vuelve a abrir la terminal.

### 9.2. `flutter doctor` muestra error en Android toolchain

- Abre Android Studio y revisa que:
  - Tienes instalado un **SDK de Android** reciente.
  - Aceptaste las licencias con `flutter doctor --android-licenses`.
- Reinstala o repara Android Studio si es necesario.

### 9.3. No aparece ningún dispositivo

- Asegúrate de que el **emulador está encendido**.
- Si es un dispositivo físico Android:
  - Activa **Opciones de desarrollador → Depuración USB**.
  - Conecta el cable USB y autoriza el ordenador.
- Vuelve a ejecutar:

  ```bash
  flutter devices
  ```

### 9.4. En macOS no me reconoce Xcode

- Verifica que esté correctamente seleccionado:

  ```bash
  sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
  ```

- Acepta la licencia:

  ```bash
  sudo xcodebuild -license
  ```

---

## 10. Flujo recomendado (resumen tipo checklist)

1. **Instalar Flutter SDK** y configurar PATH.
2. Ejecutar `flutter doctor` y anotar los problemas.
3. Instalar **Android Studio** (y Xcode si estás en macOS).
4. Crear un **emulador Android** o usar un dispositivo físico.
5. Instalar **VS Code o Android Studio** con plugin de Flutter.
6. Crear proyecto:
   ```bash
   flutter create mi_primer_proyecto
   ```
7. Ejecutar en emulador:
   ```bash
   flutter run
   ```
8. Probar hot reload y cambiar texto en `main.dart`.
9. Cuando todo funcione, generar **build de release**.

---

## 11. Próximos pasos después de la instalación

Una vez que ya tienes tu entorno funcionando, puedes avanzar a:

- Integrar **paquetes** desde `pub.dev` (ej. `http`, `provider`, `flutter_bloc`).
- Aprender **navegación** entre pantallas (Navigator 1.0 / 2.0, go_router).
- Manejo de estado (Provider, Riverpod, Bloc).
- Consumo de APIs REST / GraphQL.
- Persistencia local (SharedPreferences, Hive, SQLite).
- Temas claros/oscuros y diseño adaptativo.

---

> Esta guía está pensada para que puedas **instalar y configurar Flutter de forma fiable** en cualquier máquina, con una ruta clara de verificación usando `flutter doctor`, creación de proyecto y ejecución en dispositivos reales.
