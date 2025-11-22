# 🚦 Proyecto Flutter: App de Tránsito  
### Documentación técnica completa — Arquitectura, pantallas, servicios y pruebas

---

## 📌 1. Descripción del Proyecto

**TransitoApp** es una aplicación móvil desarrollada en **Flutter** cuyo objetivo es:

- Mostrar incidentes de tránsito en tiempo real.  
- Permitir a los usuarios **reportar nuevos incidentes**.  
- Gestionar un historial de reportes personales.  
- Incluir **mapas, geolocalización**, estadísticas y manejo de estado con **Provider**.

La app está diseñada para funcionar de forma completamente local (data simulada con almacenamiento persistente) pero estructurada para conectar fácilmente a una API real en producción.

---

## 📌 2. Arquitectura del Proyecto

Arquitectura basada en principios **limpios, escalables y modulares**:

```
transito_app/
├── lib/
│   ├── main.dart
│   ├── models/
│   │   ├── incident.dart
│   │   └── user_report.dart
│   ├── services/
│   │   ├── location_service.dart
│   │   ├── storage_service.dart
│   │   └── data_service.dart
│   ├── providers/
│   │   └── incident_provider.dart
│   ├── screens/
│   │   ├── home_screen.dart
│   │   ├── traffic_status_screen.dart
│   │   ├── report_screen.dart
│   │   └── my_reports_screen.dart
│   ├── widgets/
│   │   ├── incident_card.dart
│   │   └── status_indicator.dart
│   └── utils/
│       └── constants.dart
├── assets/
├── android/
├── ios/
└── pubspec.yaml
```

Características de la arquitectura:

- **Provider** para el manejo global del estado.  
- **Servicios desacoplados** para ubicación, almacenamiento y datos.  
- **Modelos inmutables** con `copyWith`, serialización y deserialización.  
- Separación de **UI**, **lógica**, **datos**, **servicios** y **utilidades**.

---

## 📌 3. Configuración Inicial

### 3.1 Crear proyecto
```bash
flutter create transito_app
cd transito_app
code .
```

### 3.2 Dependencias recomendadas (pubspec.yaml)

```yaml
dependencies:
  flutter:
    sdk: flutter

  provider: ^6.1.1
  geolocator: ^11.0.0
  geocoding: ^2.1.1
  permission_handler: ^11.1.0
  shared_preferences: ^2.2.2
  http: ^1.1.0
  uuid: ^4.3.3
  intl: ^0.19.0
```

### 3.3 Instalar dependencias
```bash
flutter pub get
```

---

## 📌 4. Modelos de Datos

### 4.1 Modelo `Incident`

Incluye:
- Tipo de incidente  
- Severidad  
- Ubicación  
- Coordenadas  
- Timestamp  
- Estado (activo/resuelto)

### 4.2 Modelo `UserReport`

Incluye:
- ID de reporte  
- Usuario  
- Incidente asociado  
- Estado del reporte (pendiente/confirmado/rechazado)  
- Contador de votos  

Ambos modelos incluyen:
- `toJson()`  
- `fromJson()`  
- `copyWith()`  

---

## 📌 5. Servicios

### 5.1 LocationService
- Solicitud de permisos
- Obtener ubicación actual
- Geocodificación inversa
- Cálculo de distancias

### 5.2 StorageService
- Almacenamiento persistente con SharedPreferences  
- Guardado y carga de incidentes y reportes  
- Generación/peristencia de ID de usuario  

### 5.3 DataService  
Simula un backend real:  
- Carga de incidentes iniciales (mock data)  
- Creación de nuevos reportes  
- Devuelve incidentes y reportes persistidos  

Ready para migrar a API REST/GraphQL.  

---

## 📌 6. Provider: Lógica de Negocio

`IncidentProvider` maneja:
- Lista de incidentes
- Lista de reportes del usuario
- Estados de carga/errores
- Creación de reportes nuevos
- Carga inicial de datos
- Actualizaciones de estado

Se integra en `main.dart` mediante:

```dart
MultiProvider(
  providers: [
    ChangeNotifierProvider(create: (_) => IncidentProvider()),
  ],
  child: TransitoApp(),
);
```

---

## 📌 7. Pantallas

### 7.1 HomeScreen
Navegación con **NavigationBar (Material 3)**:  
- Estado del Tránsito  
- Reportar incidente  
- Mis reportes  

### 7.2 TrafficStatusScreen
- Lista de incidentes
- Resumen general (bajo/medio/alto)
- Refresh manual
- Indicadores visuales
- Carga inicial automática

### 7.3 ReportScreen
Formulario completo con:
- Tipo de incidente
- Ubicación manual/automática (GPS)
- Selección de severidad
- Descripción
- Validación de formulario
- Indicador de progreso
- Mensaje de éxito/error

### 7.4 MyReportsScreen
- Historial del usuario
- Estadísticas (total/pendientes/confirmados)
- Estados visuales con badges
- Lista ordenada por fecha

---

## 📌 8. Widgets principales

### 8.1 `IncidentCard`
Tarjeta reutilizable que muestra:
- Icono según tipo
- Título y descripción
- Ubicación
- Severidad
- Tiempo transcurrido

### 8.2 `StatusIndicator`
Pequeño componente gráfico para los contadores de severidad.

---

## 📌 9. Permisos requeridos

### Android (AndroidManifest.xml)

```xml
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.INTERNET" />
```

### iOS (Info.plist)

```xml
<key>NSLocationWhenInUseUsageDescription</key>
<string>Necesitamos tu ubicación para mostrar incidentes cercanos.</string>
```

---

## 📌 10. Pruebas

### 10.1 Pruebas Unitarias
Modelos, servicios y funciones puras.

Ejemplos:
- Serialización JSON  
- Cálculo de distancias  
- Copias con `copyWith()`  

### 10.2 Pruebas de Widgets
- Renderizado correcto de IncidentCard  
- Renderizado correcto en listas  

### 10.3 Pruebas de Integración
- Navegación entre pantallas  
- Flujo completo crear reporte → aparecer en historial  
- Refresh de listas  

### Ejecutar test:
```bash
flutter test
```

---

## 📌 11. Compilación y despliegue

### Android APK
```bash
flutter build apk --release
```

### AppBundle
```bash
flutter build appbundle --release
```

### iOS
```bash
flutter build ios --release
```

---

## 📌 12. Roadmap (Siguientes mejoras)

- Integración API real (backend Express/Node, Firebase, Supabase o FastAPI)
- Autenticación con Firebase Auth
- Integración con Google Maps
- Notificaciones push (Firebase Messaging)
- Panel admin para validación de reportes
- Filtros avanzados (mapa de calor, severidad, distancia)
- Temas personalizados (dark/light)

---

## 📌 13. Licencia recomendada

MIT o Apache 2.0 para proyectos open-source.

---

## 📌 14. Créditos

Autores del proyecto:  
**Claud-IA & ChatGPT — 2025**

---

¿Deseas que agregue un **diagrama de arquitectura**, un **diagrama de navegación**, o que convierta esta guía en un README acompañado de imágenes para GitHub?
