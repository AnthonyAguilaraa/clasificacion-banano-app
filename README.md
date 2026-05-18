# 🍌 Clasificación de Banano

Una aplicación móvil desarrollada en **Flutter** que utiliza **inteligencia artificial** para clasificar automáticamente el tipo y estado de madurez de los bananos mediante fotografías.

## 📋 Tabla de Contenidos

- [Características](#características)
- [Requisitos](#requisitos)
- [Instalación](#instalación)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Uso](#uso)
- [Tecnologías](#tecnologías)
- [Idiomas Soportados](#idiomas-soportados)
- [Modelos de IA](#modelos-de-ia)

## ✨ Características

- 📸 **Captura de Fotos**: Toma fotos en tiempo real con la cámara del dispositivo
- 🖼️ **Carga desde Galería**: Selecciona imágenes de tu galería de fotos
- 🤖 **Clasificación con IA**: Usa un modelo MobileNetV2 entrenado para clasificar bananos
- 🌍 **Multiidioma**: Soporte para español (es) e inglés (en)
- 📊 **Resultados Detallados**: Visualiza la clasificación con confianza y detalles
- 🔍 **Análisis en Tiempo Real**: Procesa las imágenes directamente en el dispositivo

## 📱 Requisitos

### Hardware
- Dispositivo Android 8.0+ o iOS 12.0+
- Cámara trasera/frontal
- 100 MB de espacio libre

### Software
- Flutter 3.10.0 o superior
- Dart 3.10.0 o superior
- SDK de Android / Xcode (según el sistema objetivo)

## 🚀 Instalación

### 1. Clonar el repositorio

```bash
git clone https://github.com/tu-usuario/clasificacion-banano-app.git
cd clasificacion-banano-app/app_banano
```

### 2. Instalar dependencias

```bash
flutter pub get
```

### 3. Configurar permisos (Android)

El archivo `AndroidManifest.xml` incluye permisos para:
- 📷 Acceso a cámara
- 📁 Acceso a galería
- 📝 Lectura y escritura de almacenamiento

### 4. Ejecutar la aplicación

```bash
flutter run
```

Para dispositivos específicos:
```bash
flutter run -d <device-id>  # Android
flutter run -d <device-id>  # iOS
```

## 📂 Estructura del Proyecto

```
app_banano/
├── lib/
│   ├── main.dart                 # Punto de entrada de la aplicación
│   ├── core/
│   │   └── utils.dart           # Funciones utilitarias
│   ├── data/
│   │   ├── models/
│   │   │   └── banana_type.dart # Modelo de datos de banano
│   │   └── services/
│   │       └── tflite_service.dart # Servicio de inferencia con TFLite
│   └── presentation/
│       └── screens/
│           ├── home_screen.dart        # Pantalla principal
│           ├── scanner_screen.dart     # Pantalla de escaneo
│           ├── detail_screen.dart      # Pantalla de detalles
│           └── PhotoCaptureScreen.dart # Captura de fotos
├── assets/
│   ├── images/                  # Imágenes de la interfaz
│   ├── models/
│   │   ├── banano_mobileNetV2.tflite  # Modelo de IA
│   │   └── labels.txt                  # Etiquetas de clasificación
│   └── translations/
│       ├── es.json             # Traducciones al español
│       └── en.json             # Traducciones al inglés
├── android/                     # Configuración de Android
├── ios/                         # Configuración de iOS
└── pubspec.yaml                 # Dependencias del proyecto
```

## 🎯 Uso

### Flujo Principal

1. **Inicia la aplicación** → Se abre la `HomeScreen`
2. **Selecciona una opción**:
   - 📷 **Capturar Foto**: Accede a la cámara en tiempo real
   - 🖼️ **Cargar Galería**: Selecciona una imagen guardada
3. **La IA procesa la imagen** y clasifica el banano
4. **Ver Resultados**: Se muestra el tipo de banano y nivel de confianza en `DetailScreen`

### Permisos Necesarios

La aplicación solicita autorización para:
- ✅ Acceso a la cámara
- ✅ Acceso al almacenamiento

## 🛠️ Tecnologías

### Dependencias Principales

| Librería | Versión | Propósito |
|----------|---------|-----------|
| **flutter** | SDK | Framework principal |
| **camera** | ^0.11.3 | Captura de fotos en tiempo real |
| **image_picker** | ^1.0.4 | Selector de imágenes de galería |
| **tflite_flutter** | ^0.12.1 | Inferencia de modelos TFLite |
| **easy_localization** | ^3.0.8 | Soporte multiidioma |
| **image** | ^4.7.2 | Procesamiento de imágenes |
| **permission_handler** | ^12.0.1 | Gestión de permisos |

### Arquitectura

La aplicación sigue una estructura **MVVM (Model-View-ViewModel)**:

- **Models**: `BananaType` - Estructura de datos de clasificación
- **Services**: `TfliteService` - Lógica de inferencia y procesamiento
- **Screens**: Interfaz de usuario responsiva
- **Core**: Utilidades compartidas

## 🌍 Idiomas Soportados

| Idioma | Código | Archivo |
|--------|--------|---------|
| Español | `es` | `assets/translations/es.json` |
| English | `en` | `assets/translations/en.json` |

El idioma se selecciona automáticamente según la configuración del dispositivo.

## 🤖 Modelos de IA

### MobileNetV2
- **Archivo**: `banano_mobileNetV2.tflite`
- **Tamaño**: Optimizado para dispositivos móviles
- **Entrada**: Imágenes de 224x224 píxeles en RGB
- **Salida**: Probabilidades de clasificación para cada tipo de banano

### Procesamiento de Imágenes
```dart
// Redimensionamiento: 224x224
// Normalización: Valores RGB 0-255
// Preprocesamiento: Aplicado por el modelo
```

## 📈 Flujo de Clasificación

```
Imagen (cámara/galería)
    ↓
TfliteService.loadModel()
    ↓
Preprocesar imagen (224x224)
    ↓
Inferencia con MobileNetV2
    ↓
Obtener probabilidades
    ↓
Retornar clasificación
    ↓
DetailScreen (mostrar resultados)
```

## 🔧 Compilación para Producción

### Android
```bash
flutter build apk --release
# o para App Bundle
flutter build appbundle --release
```

### iOS
```bash
flutter build ipa --release
```

## 📝 Configuración de Desarrollo

### Configurar dispositivo Android
```bash
flutter doctor
```

### Hot Reload
Durante el desarrollo, la aplicación soporta hot reload:
```bash
r   # Hot reload
R   # Full restart
```

## 🐛 Troubleshooting

### Error: "No se encontró cámara disponible"
- Verifica que el dispositivo tiene cámara
- Comprueba los permisos en Configuración → Aplicaciones

### Error: "Modelo no cargado"
- Asegúrate que `banano_mobileNetV2.tflite` está en `assets/models/`
- Verifica que el archivo está incluido en `pubspec.yaml`

### Rendimiento lento
- Reduce la resolución de la imagen
- Usa dispositivos con al menos 2GB de RAM

## 📄 Licencia

Este proyecto está disponible bajo la licencia MIT.

## 👨‍💻 Autor

Desarrollado como herramienta de clasificación inteligente de bananos.

## 📞 Soporte

Para reportar problemas o sugerencias, abre un **Issue** en el repositorio.

---

**Última actualización**: Enero 2025
