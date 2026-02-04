# Directorio de Versiones

Este directorio contiene todas las versiones del proyecto Proveedores, organizadas en subdirectorios individuales.

## Estructura

Cada versión tiene su propio directorio con el siguiente formato:

```
X.Y.Z/
├── version.json       # Metadata de la versión en formato JSON
├── RELEASE_NOTES.md  # Notas de versión legibles
└── src/              # Código fuente (opcional)
```

## Carpetas Especiales

- **templates/**: Contiene plantillas para crear nuevas versiones
  - `version.json`: Plantilla de metadata
  - `RELEASE_NOTES.md`: Plantilla de notas de versión

## Crear una Nueva Versión

1. Copiar plantillas al nuevo directorio:
   ```bash
   cp -r templates/ X.Y.Z/
   ```

2. Editar los archivos copiados con los datos de la nueva versión

3. Actualizar el archivo VERSION en la raíz del repositorio

4. Actualizar CHANGELOG.md con los cambios

## Convenciones

- Use versionado semántico: MAJOR.MINOR.PATCH
- Incluya siempre version.json y RELEASE_NOTES.md
- Documente todos los cambios significativos
- Mantenga la consistencia en el formato

Para más información, consulte [VERSIONING.md](../VERSIONING.md) en la raíz del repositorio.
