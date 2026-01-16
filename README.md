# 🔔 Notification Capture

APK para Android que captura todas las notificaciones usando NotificationListenerService.

## Características

- ✅ Captura notificaciones de **cualquier app**
- ✅ Filtro por **apps específicas** (selección múltiple)
- ✅ Filtro por **palabras clave** 
- ✅ Historial de últimas 500 notificaciones
- ✅ Exportar a portapapeles
- ✅ Copiar notificaciones individuales
- ✅ Detalle expandido (long press)
- ✅ Switch para activar/desactivar captura
- ✅ UI oscura moderna

## Requisitos

- Android 8.0+ (API 26)
- Permiso de acceso a notificaciones (se solicita automáticamente)

## Compilación

### Opción 1: Android Studio
1. Abrir el proyecto en Android Studio
2. Sync Gradle
3. Build > Build Bundle(s) / APK(s) > Build APK(s)

### Opción 2: Línea de comandos
```bash
cd NotificationCapture
./gradlew assembleDebug
# APK en: app/build/outputs/apk/debug/app-debug.apk
```

### Opción 3: Servicios online
Puedes usar servicios como:
- **APK Builder** (https://build.phonegap.com)
- **Buildozer** 
- **GitHub Actions** con workflow de Android

## Uso

1. **Instalar la APK** en tu dispositivo
2. **Abrir la app** - te pedirá permisos
3. **Activar el servicio** en Configuración > Apps > Acceso especial > Acceso a notificaciones
4. Las notificaciones se capturarán automáticamente

### Filtros

- **Por apps**: Toca "📱 Apps" para seleccionar qué apps capturar (vacío = todas)
- **Por palabras**: Toca "🔍 Keywords" para agregar palabras que deben estar presentes

### Acciones

- **Toca** una notificación para copiarla
- **Mantén presionado** para ver el detalle completo
- **Exportar** copia todas las notificaciones al portapapeles
- **Limpiar** elimina el historial

## Estructura del proyecto

```
NotificationCapture/
├── app/
│   ├── src/main/
│   │   ├── java/com/alexdev/notificationcapture/
│   │   │   ├── MainActivity.java          # UI principal
│   │   │   ├── NotificationCaptureService.java  # Servicio listener
│   │   │   └── NotificationReceiver.java  # Broadcast receiver
│   │   ├── res/
│   │   │   ├── layout/
│   │   │   │   ├── activity_main.xml
│   │   │   │   ├── item_notification.xml
│   │   │   │   └── dialog_keywords.xml
│   │   │   ├── values/
│   │   │   │   ├── strings.xml
│   │   │   │   └── styles.xml
│   │   │   └── drawable/
│   │   │       └── ic_launcher.xml
│   │   └── AndroidManifest.xml
│   └── build.gradle
├── build.gradle
├── settings.gradle
└── gradle.properties
```

## Personalización

### Agregar webhook/API
Edita `NotificationReceiver.java` para enviar notificaciones a un servidor:

```java
@Override
public void onReceive(Context context, Intent intent) {
    // Extraer datos
    String title = intent.getStringExtra("title");
    String text = intent.getStringExtra("text");
    
    // Enviar a tu API
    new Thread(() -> {
        // HTTP POST a tu servidor
    }).start();
}
```

### Enviar a Telegram
Agrega en el receiver:

```java
String botToken = "TU_BOT_TOKEN";
String chatId = "TU_CHAT_ID";
String url = "https://api.telegram.org/bot" + botToken + "/sendMessage";
// POST con chat_id y text
```

## Permisos requeridos

| Permiso | Uso |
|---------|-----|
| BIND_NOTIFICATION_LISTENER_SERVICE | Capturar notificaciones |
| POST_NOTIFICATIONS | Mostrar notificaciones propias |
| INTERNET | (Opcional) Enviar datos a servidor |

## Notas de seguridad

⚠️ Esta app tiene acceso a TODAS las notificaciones del dispositivo, incluyendo mensajes, códigos 2FA, etc. 

- Úsala solo en dispositivos de tu propiedad
- No distribuyas con datos sensibles
- El historial se guarda localmente en SharedPreferences

## Licencia

Uso personal/educativo. Modifica según necesites.
# aplicacionyape
