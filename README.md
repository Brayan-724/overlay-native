> [!WARNING]
> **Archive:** The project will continue with slint in [this repo](https://github.com/Brayan-724/stream-overlay)


# Overlay Native

Un cliente de overlay nativo para Twitch Chat que muestra mensajes de chat como ventanas flotantes semi-transparentes en el escritorio.

## 🚀 Características

- **Multiplataforma**: Soporte nativo para Linux (GTK) y Windows (WinAPI)
- **Overlay en tiempo real**: Muestra mensajes de Twitch chat como ventanas flotantes
- **Ventanas semi-transparentes**: Overlay no intrusivo con transparencia configurable
- **Barra de progreso**: Indicador visual del tiempo de vida de cada mensaje
- **Posicionamiento aleatorio**: Los mensajes aparecen en posiciones aleatorias en la pantalla
- **Gestión automática**: Las ventanas se cierran automáticamente después de 10 segundos
- **Renderizado de emotes**: Soporte básico (implementado parcialmente)

## 📋 Requisitos del Sistema

### Linux
- GTK 3.0+
- GDK 3.0+
- X11 (para funcionalidades específicas de ventanas)
- Rust 1.70+

### Windows
- Windows 10/11
- Visual Studio Build Tools o Visual Studio Community (o MSYS2 + MinGW)
- Rust 1.70+

## 🛠️ Instalación

Ver [Guía de Instalación](docs/INSTALLATION.md) para instrucciones detalladas por plataforma.

```bash
# Clonar el repositorio
git clone https://github.com/Brayan-724/overlay-native/
cd overlay-native

# Compilar y ejecutar
cargo run
```

## 📖 Documentación

- [Especificaciones Linux](docs/LINUX_SPECS.md) - Detalles técnicos para la implementación GTK
- [Especificaciones Windows](docs/WINDOWS_SPECS.md) - Detalles técnicos para la implementación WinAPI
- [Arquitectura del Código](docs/ARCHITECTURE.md) - Estructura y diseño del proyecto
- [Guía de Instalación](docs/INSTALLATION.md) - Instrucciones de compilación por plataforma

## 🏗️ Arquitectura

El proyecto está estructurado con módulos específicos por plataforma:

```
src/
├── main.rs          # Punto de entrada principal y gestión de Twitch IRC (twitch-irc)
├── connection.rs    # (Reservado) Lógica de conexión/abstracción futura
├── window.rs        # Implementación GTK (Linux)
├── windows.rs       # Implementación WinAPI (Windows)
└── x11.rs           # Funcionalidades específicas de X11
```

## 🎮 Uso

1. Ejecuta la aplicación con `cargo run`
2. La aplicación se conectará automáticamente al canal de Twitch configurado
3. Los mensajes de chat aparecerán como ventanas flotantes en tu pantalla
4. Cada ventana muestra:
   - Nombre de usuario (en negrita)
   - Contenido del mensaje
   - Emotes de Twitch (si están presentes)
   - Barra de progreso indicando el tiempo restante

## ⚙️ Configuración

Actualmente el canal está hardcodeado en `main.rs`. Para cambiar el canal:

```rust
client.join("tu_canal_aqui".to_owned()).unwrap();
```

## 📦 Dependencias

Crates externas (mínimas sugeridas, ver Cargo.toml para exactas):
- anyhow = "1.0.83"
- tokio = { version = "1.37.0", features = ["rt-multi-thread"] }
- twitch-irc = "5.0.1"
- rand = "0.8.5"
- reqwest = "0.12.4"
- winapi = { version = "0.3", features = ["winuser", "wingdi", "windef", "libloaderapi"] }
- gtk = "0.17.1"
- gdk = "0.17.1"
- pango = "0.17.1"
- glib = "0.17.8"
- glib-macros = "0.17.8"
- gdkx11 = "0.17"
- x11rb = { version = "0.11.1", features = ["randr"] }

Dependencias de sistema:
- Linux: pkg-config, GTK 3 (headers y dev: ej. libgtk-3-dev), X11 en ejecución, (recomendado) OpenSSL dev para TLS.
- Windows: Rust (rustup), y una toolchain: Visual Studio Build Tools (MSVC) o MSYS2 + MinGW; con MSYS2 se recomienda instalar `mingw-w64-x86_64-gtk3` y `mingw-w64-x86_64-pkg-config` si se compila GTK.

## 🤝 Contribuir

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📝 Licencia

Este proyecto está bajo la licencia MIT. Ver el archivo `LICENSE` para más detalles.

## 🐛 Problemas Conocidos

- En Windows, las ventanas pueden no aparecer correctamente si no se tienen los permisos adecuados
- En Linux, requiere un servidor X11 funcionando
- Los emotes pueden tardar en cargar dependiendo de la conexión a internet (implementado parcialmente)

## 🔧 Desarrollo

Para desarrollo local:

```bash
# Ejecutar en modo debug
cargo run

# Ejecutar tests
cargo test

# Compilar para release
cargo build --release
```

## 📊 Estado del Proyecto

- ✅ Conexión a Twitch IRC (via twitch-irc)
- ✅ Renderizado de ventanas en Windows
- ✅ Renderizado de ventanas en Linux
- ✅ Barra de progreso funcional
- ✅ Gestión de memoria y limpieza
- 🔄 Carga de emotes (implementado parcialmente)
