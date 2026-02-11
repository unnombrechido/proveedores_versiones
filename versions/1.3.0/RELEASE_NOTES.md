# Release Notes - Version 1.3.0

**Fecha de Lanzamiento:** 2026-02-10  
**Tipo de Release:** Minor  
**Estado:** Stable

## Resumen

Versión 1.3.0 introduce mejoras significativas en el sistema de configuración, logging mejorado para debugging, y correcciones en la compatibilidad de configuraciones entre versiones.

## Nuevas Características

- ✨ Sistema de logging avanzado en desktop_app.py con rotación automática de logs
- ✨ Control de modo debug a través de configuración, variable de entorno o línea de comandos
- ✨ Configuración estandarizada sin duplicados de claves antiguas/nuevas
- ✨ Compatibilidad automática entre formatos de configuración antiguos y nuevos

## Mejoras

- 🚀 Configuración modular completamente estandarizada
- 🚀 Logging con control de verbosidad y rotación automática (5MB por archivo)
- 🚀 Eliminación de claves duplicadas en configuración (NAME/company_name, etc.)
- 🚀 Instalador actualizado para mantener consistencia de configuración

## Correcciones

- 🐛 Resolución de conflictos entre claves de configuración antiguas y nuevas
- 🐛 Corrección en actualización de versión durante instalación
- 🐛 Mejoras en compatibilidad de configuración entre migraciones
- 🐛 Logging incontrolable eliminado de run.bat

## Cambios de Ruptura

- No hay cambios de ruptura.

## Notas de Actualización

1. Ejecuta INSTALAR.bat para actualización automática.
2. El sistema detectará configuraciones existentes y las migrará automáticamente.
3. Los logs ahora se rotan automáticamente para evitar crecimiento indefinido.

## Problemas Conocidos

- Modo debug debe habilitarse manualmente en configuración o variables de entorno.
- El servicio de Windows no está funcionando correctamente.
- La función de exportación está deshabilitada en la aplicación.
- La versión no se actualiza correctamente en la configuración durante la instalación.
- La vista previa de órdenes muestra una segunda vista previa al imprimir.
- El desinstalador no elimina carpetas/archivos completamente y requiere intervención manual.
- Importar desde una versión anterior puede causar discrepancias en configuración y datos.
- La aplicación no respeta la configuración de zoom al reabrirse.
- Los enlaces de Acerca de y Licencia están construidos incorrectamente.

## Documentación

- CONFIGURACIÓN.md (actualizado)
- LOGGING.md (nuevo)
- MIGRATION_GUIDE.md

## Contribuidores

Equipo de Desarrollo Proveedores