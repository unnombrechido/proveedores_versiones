# Changelog

Todas las modificaciones notables de este proyecto serán documentadas en este archivo.

El formato está basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/),
y este proyecto adhiere a [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.3.1] - 2026-03-09

### Added
- Instalador NSIS nativo para Windows con asistente gráfico
- Tabla `contact_types` LOV con tipos predefinidos (General, Compras, Ventas, Contabilidad, Técnico, Logística)
- `supplier_contacts.contact_type_id` referencia FK a `contact_types` en lugar de texto libre
- Detección y cierre automático de instancias en ejecución antes de instalar (evita archivos bloqueados)
- Pipeline de migración completo: `migrate_db_schema.py` + `init_lovs.py` + `migrate_supplier_contacts.py` para todos los escenarios de upgrade

### Fixed
- Base de datos vacía (0 bytes) en instalación nueva — import de modelos en `init_db()` creaba un `Base` separado sin tablas registradas
- Error `table supplier_contacts has no column named contact_type` durante migración desde v1.0
- `init_lovs.py` no sembraba la tabla `contact_types`
- `migrate_db_schema.py` nunca se ejecutaba durante upgrades in-place
- `migrate_supplier_contacts.py` no era idempotente (duplicaba contactos en segunda ejecución)
- Ruta de `cleanup_installation.ps1` resolviéndose a `C:\scripts\...` en lugar de `C:\SistemaProveedores\scripts\...`
- `requirements.txt` no se desplegaba al instalar, causando falla de `pip install`
- Migración de contactos omitida en upgrades in-place (estaba dentro del bloque `isSameDb == false`)

### Improved
- Soporte de upgrade desde v0.1, v1.0, v1.2.1 y v1.3.0 correctamente diferenciado
- `migrate_supplier_contacts.py` rellena `contact_type_id` en bases de datos v1.2.1 con columna legacy
- `init_lovs.py` se ejecuta en toda instalación nueva garantizando datos LOV siempre presentes

## [1.3.0] - 2026-02-10

### Added
- Sistema de logging avanzado con rotación automática en desktop_app.py
- Control de modo debug a través de configuración UI
- Compatibilidad automática entre formatos de configuración antiguos y nuevos

### Improved
- Configuración estandarizada sin duplicados de claves
- Instalador actualizado para consistencia de configuración
- Logging controlado con límites de tamaño

### Removed
- Claves duplicadas en configuración (NAME, ADDRESS, etc.)
- Logging incontrolable de run.bat

### Fixed
- Conflictos entre claves de configuración antiguas y nuevas
- Actualización de versión durante instalación
- Compatibilidad de configuración entre migraciones

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
