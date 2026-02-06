# Changelog

Todas las modificaciones notables de este proyecto serán documentadas en este archivo.

El formato está basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/),
y este proyecto adhiere a [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.2.1] - 2026-02-05

### Added
- Utilidad de limpieza segura integrada en el instalador
- Sección About con versión, licencia y notas de versión en la UI
- Accesos directos opcionales para la aplicación y la web

### Improved
- Configuración modular en config/config.ini con VERSION persistente
- Flujo de instalación con valores por defecto y prompts más claros
- Verificación de integridad al finalizar instalación

### Fixed
- Bloqueos durante limpieza de carpetas antiguas
- Compatibilidad de rutas y arranque en instalaciones previas
- Actualización de accesos directos

## [0.1.0] - 2026-02-04

### Added
- Primera versión beta del sistema Proveedores (proveedores-v0.1.zip)
- Funcionalidades básicas del sistema de gestión
- Estructura de versión beta para pruebas internas

## [1.0.0] - 2026-02-04

### Added
- ✨ Database maintenance utilities (cleanup_database.py/.bat)
- ✨ Automatic sample data loader (load_sample_data.py/.bat)
- ✨ CSV import templates with examples (suppliers, items, prices)
- ✨ Configurable logo support via config.ini
- ✨ Server-side configuration API endpoints
- ✨ Patch installer for v0.1 upgrades (PATCH-v0.1.bat/ps1)
- ✨ Dynamic logo loading in UI
- ✨ Enhanced documentation (DATABASE_CLEANUP.md, LOAD_SAMPLE_DATA.md)
- ✨ Sample CSV files (import_proveedores.csv, import_lista_materiales.csv)

### Fixed
- 🐛 Import modal now pre-selects correct type
- 🐛 Fixed run.bat path (app\app.py)
- 🐛 Logo placeholder when no logo configured

### Improved
- 💡 CSV support for combined imports (items+suppliers+prices)
- 💡 Configuration preservation during upgrades
- 💡 Better import validation and error messages

### Distribution
- 📦 Distribution file: proveedores-v1.0.zip (~134 KB)
- 📦 Total files: 44 files
- 📦 Full backward compatibility with v0.1 data
