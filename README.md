# Proveedores Versiones

Repositorio de versiones para código de app de Proveedores.

## 📋 Descripción

Este repositorio gestiona el control de versiones y releases del sistema Proveedores, siguiendo las mejores prácticas de versionado semántico y documentación de cambios.

## 🗂️ Estructura del Repositorio

```
proveedores_versiones/
├── VERSION                 # Versión actual del proyecto
├── CHANGELOG.md           # Registro histórico de cambios
├── VERSIONING.md         # Guía de versionado completa
├── .gitignore            # Archivos excluidos del control de versiones
└── versions/             # Directorio de versiones
    ├── templates/        # Plantillas para nuevas versiones
    │   ├── version.json
    │   └── RELEASE_NOTES.md
    └── X.Y.Z/           # Carpetas por versión
        ├── version.json       # Metadata de la versión
        ├── RELEASE_NOTES.md   # Notas de versión
        └── src/              # Código fuente (opcional)
```

## 🚀 Inicio Rápido

### Ver Versión Actual

```bash
cat VERSION
```

### Ver Historial de Cambios

```bash
cat CHANGELOG.md
```

### Ver Detalles de una Versión

```bash
cat versions/1.0.0/version.json
cat versions/1.0.0/RELEASE_NOTES.md
```

## 📚 Documentación

- **[VERSIONING.md](VERSIONING.md)**: Guía completa del sistema de versionado
- **[CHANGELOG.md](CHANGELOG.md)**: Registro histórico de todos los cambios
- **[versions/templates/](versions/templates/)**: Plantillas para crear nuevas versiones

## 🏷️ Versionado Semántico

Este proyecto utiliza [Versionado Semántico 2.0.0](https://semver.org/lang/es/):

- **MAJOR**: Cambios incompatibles con versiones anteriores
- **MINOR**: Nueva funcionalidad compatible hacia atrás
- **PATCH**: Correcciones de bugs compatibles

Formato: `MAJOR.MINOR.PATCH` (ejemplo: `1.2.3`)

## 📝 Crear una Nueva Versión

1. **Crear directorio para la nueva versión:**
   ```bash
   mkdir -p versions/X.Y.Z
   ```

2. **Copiar y editar plantillas:**
   ```bash
   cp versions/templates/version.json versions/X.Y.Z/
   cp versions/templates/RELEASE_NOTES.md versions/X.Y.Z/
   ```

3. **Actualizar archivos:**
   - Editar `versions/X.Y.Z/version.json`
   - Editar `versions/X.Y.Z/RELEASE_NOTES.md`
   - Actualizar `CHANGELOG.md`
   - Actualizar `VERSION`

4. **Commit y crear tag:**
   ```bash
   git add .
   git commit -m "Release version X.Y.Z"
   git tag -a vX.Y.Z -m "Version X.Y.Z"
   git push origin main --tags
   ```

## 🔍 Consultar Versiones

### Listar todas las versiones

```bash
ls -1 versions/ | grep -E '^[0-9]+\.'
```

### Ver información de versión específica

```bash
# Formato JSON
cat versions/1.0.0/version.json | jq '.'

# Notas de versión
cat versions/1.0.0/RELEASE_NOTES.md
```

## 📖 Categorías de Cambios

- **Added**: Nuevas características
- **Changed**: Cambios en funcionalidad existente
- **Deprecated**: Características obsoletas
- **Removed**: Características eliminadas
- **Fixed**: Correcciones de bugs
- **Security**: Correcciones de seguridad

## 🤝 Contribuir

Para contribuir con nuevas versiones o actualizaciones:

1. Lee la [Guía de Versionado](VERSIONING.md)
2. Sigue el formato de [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/)
3. Documenta todos los cambios apropiadamente
4. Asegúrate de actualizar tanto `version.json` como `RELEASE_NOTES.md`

## 📄 Licencia

Ver archivo [LICENSE](LICENSE) para más detalles.

## 📞 Contacto

Para preguntas o soporte, contactar al equipo de desarrollo del proyecto Proveedores.
