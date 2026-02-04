# Guía de Versionado - Proveedores App

## Introducción

Este documento describe el sistema de versionado utilizado para la aplicación Proveedores. Seguimos las mejores prácticas de la industria para garantizar un control de versiones claro y consistente.

## Versionado Semántico

Este proyecto utiliza [Versionado Semántico 2.0.0](https://semver.org/lang/es/). Las versiones siguen el formato:

```
MAJOR.MINOR.PATCH
```

Donde:

- **MAJOR**: Cambios incompatibles con versiones anteriores (breaking changes)
- **MINOR**: Nueva funcionalidad compatible con versiones anteriores
- **PATCH**: Correcciones de bugs compatibles con versiones anteriores

### Ejemplos

- `1.0.0` → `1.0.1`: Corrección de bug
- `1.0.0` → `1.1.0`: Nueva funcionalidad
- `1.0.0` → `2.0.0`: Cambio incompatible

## Estructura de Directorios

```
proveedores_versiones/
├── VERSION                      # Versión actual del proyecto
├── CHANGELOG.md                 # Registro histórico de cambios
├── VERSIONING.md               # Este documento
├── .gitignore                  # Archivos ignorados
└── versions/                   # Directorio de versiones
    ├── templates/              # Plantillas para nuevas versiones
    │   ├── version.json
    │   └── RELEASE_NOTES.md
    ├── 1.0.0/                 # Ejemplo: Versión 1.0.0
    │   ├── version.json       # Metadata de la versión
    │   ├── RELEASE_NOTES.md   # Notas de versión
    │   └── src/               # Código fuente (opcional)
    └── X.Y.Z/                 # Futuras versiones
```

## Archivos Clave

### VERSION

Archivo de texto simple que contiene la versión actual del proyecto:

```
1.0.0
```

### CHANGELOG.md

Registro cronológico de todos los cambios notables. Sigue el formato [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/).

Categorías de cambios:
- **Added**: Nuevas características
- **Changed**: Cambios en funcionalidad existente
- **Deprecated**: Características obsoletas (pero aún disponibles)
- **Removed**: Características eliminadas
- **Fixed**: Correcciones de bugs
- **Security**: Correcciones de vulnerabilidades

### version.json

Metadata estructurada de cada versión en formato JSON:

```json
{
  "version": "1.0.0",
  "release_date": "2026-02-04",
  "release_name": "Initial Release",
  "type": "major",
  "status": "stable",
  "description": "Descripción de la versión",
  "changes": {
    "added": [],
    "changed": [],
    "deprecated": [],
    "removed": [],
    "fixed": [],
    "security": []
  },
  "compatibility": {
    "minimum_version": "1.0.0",
    "breaking_changes": false
  },
  "files": {
    "source": [],
    "documentation": [],
    "configuration": []
  },
  "checksum": {
    "algorithm": "sha256",
    "value": ""
  },
  "authors": [],
  "notes": ""
}
```

### RELEASE_NOTES.md

Notas detalladas de cada versión en formato Markdown, diseñadas para ser leídas por usuarios finales y desarrolladores.

## Proceso de Release

### 1. Preparación de Nueva Versión

1. Determinar el tipo de versión (MAJOR, MINOR, PATCH)
2. Crear directorio para la nueva versión:
   ```bash
   mkdir -p versions/X.Y.Z
   ```

### 2. Documentar Cambios

1. Copiar plantillas:
   ```bash
   cp versions/templates/version.json versions/X.Y.Z/
   cp versions/templates/RELEASE_NOTES.md versions/X.Y.Z/
   ```

2. Editar `versions/X.Y.Z/version.json` con los datos de la versión

3. Editar `versions/X.Y.Z/RELEASE_NOTES.md` con notas detalladas

4. Actualizar `CHANGELOG.md` con los cambios

### 3. Actualizar Versión Actual

1. Actualizar archivo `VERSION`:
   ```bash
   echo "X.Y.Z" > VERSION
   ```

### 4. Commit y Tag

1. Hacer commit de los cambios:
   ```bash
   git add .
   git commit -m "Release version X.Y.Z"
   ```

2. Crear tag Git:
   ```bash
   git tag -a vX.Y.Z -m "Version X.Y.Z"
   ```

3. Push con tags:
   ```bash
   git push origin main --tags
   ```

## Estados de Versión

- **alpha**: Versión muy temprana, inestable
- **beta**: Versión de prueba, relativamente estable
- **rc** (Release Candidate): Candidato a versión final
- **stable**: Versión final, lista para producción

## Compatibilidad

### Versiones Compatibles

Dos versiones son compatibles si:
- Tienen el mismo número MAJOR
- La versión MINOR.PATCH es igual o mayor

Ejemplo: `1.2.0` es compatible con `1.0.0`, pero `2.0.0` NO es compatible con `1.x.x`

### Breaking Changes

Un "breaking change" es cualquier cambio que:
- Elimina o renombra APIs públicas
- Cambia el comportamiento de funciones existentes
- Requiere cambios en el código del usuario
- Modifica el formato de datos o configuración

Los breaking changes SIEMPRE requieren incrementar el número MAJOR.

## Pre-releases

Para versiones pre-release, se puede usar el formato:

```
X.Y.Z-alpha.N
X.Y.Z-beta.N
X.Y.Z-rc.N
```

Ejemplos:
- `1.0.0-alpha.1`: Primera versión alpha de 1.0.0
- `1.0.0-beta.2`: Segunda versión beta de 1.0.0
- `1.0.0-rc.1`: Primer release candidate de 1.0.0

## Checksums

Para garantizar la integridad de cada versión, se generan checksums SHA-256:

```bash
# Generar checksum del directorio de versión
find versions/X.Y.Z -type f -exec sha256sum {} \; | sha256sum
```

## Mejores Prácticas

1. **Documentar todos los cambios**: Cada cambio debe estar en el CHANGELOG
2. **Usar commits descriptivos**: Facilita generar notas de versión
3. **Mantener compatibilidad**: Evitar breaking changes en versiones MINOR/PATCH
4. **Probar antes de release**: Validar que todo funciona correctamente
5. **Comunicar cambios**: Notificar a usuarios sobre nuevas versiones
6. **Archivar versiones antiguas**: Mantener historial completo
7. **Documentar breaking changes**: Ser explícito sobre incompatibilidades
8. **Incluir instrucciones de migración**: Facilitar actualizaciones

## Herramientas Recomendadas

- **Git Tags**: Para marcar versiones
- **GitHub Releases**: Para publicar versiones
- **Conventional Commits**: Para mensajes de commit estructurados
- **Semantic Release**: Para automatizar versionado

## Referencias

- [Semantic Versioning 2.0.0](https://semver.org/lang/es/)
- [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/)
- [Conventional Commits](https://www.conventionalcommits.org/es/)

## Soporte

Para preguntas sobre el sistema de versionado, contactar al equipo de desarrollo o revisar la documentación del proyecto.
