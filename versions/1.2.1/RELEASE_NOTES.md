# Release Notes - Version 1.2.1

**Fecha de Lanzamiento:** 2026-02-05  
**Tipo de Release:** Patch  
**Estado:** Stable

## Resumen

Actualización centrada en mejoras del instalador, configuración y mantenimiento, incluyendo limpieza segura de instalaciones anteriores, configuración modular y accesos directos.

## Nuevas Características

- ✨ Utilidad de limpieza segura integrada en el instalador.
- ✨ Sección About con versión, licencia y notas de versión en la UI.
- ✨ Accesos directos opcionales para la aplicación y la web.

## Mejoras

- 🚀 Configuración modular en config/config.ini con VERSION persistente.
- 🚀 Flujo de instalación con valores por defecto y prompts más claros.
- 🚀 Integridad de instalación verificada al finalizar.

## Correcciones

- 🐛 Evita bloqueos durante limpieza de carpetas antiguas.
- 🐛 Correcciones en rutas y compatibilidad con estructuras previas.
- 🐛 Mejoras en compatibilidad de arranque y shortcuts.

## Cambios de Ruptura

- No hay cambios de ruptura.

## Notas de Actualización

1. Ejecuta INSTALAR.bat.
2. Acepta la creación de backup si se detecta una instalación previa.
3. Verifica que config/config.ini se haya generado.

## Problemas Conocidos

- Si la distribución es generada con archivos en uso, el ZIP puede fallar al crear. Cierra la app/editores y reintenta.

## Documentación

- DATABASE_CLEANUP.md
- LOAD_SAMPLE_DATA.md
- USER_AUTHENTICATION.md
- UPGRADE_GUIDE.md

## Contribuidores

- Equipo Proveedores

## Checksums

```
SHA256: B090CA686D2DEA887DC25094FB42173C28B593907E95A9DFA5B9EB0F7DF2DFDC
```
