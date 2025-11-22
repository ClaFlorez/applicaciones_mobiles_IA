# 📦 SDKs y Herramientas Necesarias para Flutter  
Guía completa — Enlaces oficiales y explicación clara para GitHub

---

## 🧭 1. Flutter SDK (obligatorio)

Flutter es el framework principal. Descárgalo desde su sitio oficial según tu sistema operativo:

🔗 **Descarga Flutter (Windows, macOS, Linux)**  
https://docs.flutter.dev/get-started/install

Incluye:
- Motor Flutter
- Compilador Dart
- Herramientas de build
- `flutter doctor`

---

## 🤖 2. Android SDK (obligatorio para apps Android)

El Android SDK viene incluido con **Android Studio**, que es la forma recomendada de instalarlo.

🔗 **Android Studio (incluye Android SDK)**  
https://developer.android.com/studio

Instala desde:
**Android Studio → More Actions → SDK Manager**

Asegúrate de instalar:
- Android SDK Platform (API 33 o API 34 recomendadas)
- Android SDK Build-Tools
- Android Emulator
- Platform-tools

Para aceptar las licencias:

```bash
flutter doctor --android-licenses
```

---

## 🍏 3. Xcode (solo macOS, obligatorio para iOS)

Si planeas compilar apps para iPhone/iPad, necesitas Xcode.

🔗 **Xcode (App Store oficial)**  
https://apps.apple.com/us/app/xcode/id497799835

Incluye:
- SDK de iOS
- Firmado de apps
- Simuladores iOS

Activar licencia después de instalar:

```bash
sudo xcodebuild -license
```

---

## 🎯 4. Dart SDK (opcional)

No es necesario instalarlo si ya usas Flutter porque viene integrado.  
Solo instálalo por separado si trabajarás con Dart sin Flutter.

🔗 **Descargar Dart SDK**  
https://dart.dev/get-dart

---

## 🛠️ 5. Android Command Line Tools (opcional)

Solo necesitas esto si NO quieres instalar Android Studio.

🔗 **Herramientas CLI del Android SDK**  
https://developer.android.com/studio#command-tools

Permiten instalar componentes del SDK así:

```bash
sdkmanager "platform-tools" "platforms;android-34" "build-tools;34.0.0"
```

---

## 📱 6. Emuladores y dispositivos

### Emuladores Android (desde Android Studio)
- Pixel 5 o Pixel 7 recomendados  
- API 33+  
- Imagen **x86_64** (más rápida)

### Simuladores iOS (solo macOS)
- Se instalan desde Xcode  
- Requieren chip Intel o Apple Silicon

---

## 🧪 7. Verificación con flutter doctor

Después de instalar todo:

```bash
flutter doctor
```

Debe mostrar ✔ en:
- Flutter
- Android toolchain
- Android Studio
- Xcode (si estás en macOS)
- Chrome (si usas Flutter Web)
- Dispositivos disponibles

---

## 📄 Archivo creado automáticamente

Este archivo resume todos los SDKs necesarios para comenzar con Flutter desde cero, ideal para colocarlo en un repositorio en GitHub junto a tus otros tutoriales sobre Flutter.

