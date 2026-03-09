# Release Notes - Versión 1.3.1

**Fecha de Lanzamiento:** 2026-03-09  
**Tipo de Release:** Patch  
**Estado:** Stable  
**Versión anterior:** 1.3.0

---

## Resumen

Versión 1.3.1 es una release de corrección y estabilización del instalador. Resuelve múltiples fallas críticas en el proceso de instalación y migración de datos que afectaban upgrades desde v1.0, v1.2.1 y v1.3.0. Introduce soporte completo de tablas LOV (List of Values), gestión de contactos múltiples por proveedor con tipo de contacto referenciado, y un instalador NSIS robusto para Windows.

---

## ✨ Nuevas Características

### Instalador NSIS para Windows
- Instalador nativo `.exe` con asistente gráfico (NSIS 3.x)
- Detección automática de instalación existente con opción de actualizar o instalar desde cero
- Pantalla de configuración de empresa y logo durante la instalación
- Selección de componentes: servicio de Windows, accesos directos, limpieza de archivos obsoletos
- El instalador detiene automáticamente instancias en ejecución (servicio + procesos Python) antes de copiar archivos — elimina el error *"Error abriendo archivo para escritura"*

### Sistema de Contactos por Tipo (LOV)
- Nueva tabla `contact_types` con tipos predefinidos: General, Compras, Ventas, Contabilidad, Técnico, Logística
- `supplier_contacts.contact_type_id` ahora referencia la tabla LOV en lugar de usar texto libre
- Migración automática rellena `contact_type_id` en bases de datos con la columna legacy `contact_type`

### Pipeline de Migración Completo
- `migrate_db_schema.py` ahora se ejecuta automáticamente en upgrades in-place — agrega columnas FK faltantes sin pérdida de datos
- `init_lovs.py` se ejecuta en toda instalación nueva y upgrade — siembra datos LOV idempotentemente
- `migrate_supplier_contacts.py` se ejecuta en todos los escenarios de upgrade (no solo migraciones entre rutas)

---

## 🚀 Mejoras

### Instalador
- `requirements.txt` ahora se despliega correctamente a `$INSTDIR` — resuelve falla de `pip install` en instalaciones nuevas
- Upgrades in-place (v1.0 / v1.2.1 / v1.3.0 → v1.3.1) ahora aplican cambios de esquema y datos LOV
- Ruta de `cleanup_installation.ps1` corregida para resolverse relativa a `$installPath` en lugar de la raíz del disco
- `migrate_supplier_contacts.py` es idempotente: omite proveedores que ya tienen contactos

### Soporte Multi-Versión
| Origen | Migración de datos | Esquema | LOV | Contactos |
|---|---|---|---|---|
| v0.1 (flat) | ✅ migrate_database.py | ✅ | ✅ | ✅ |
| v1.0 (in-place) | — | ✅ | ✅ | ✅ |
| v1.2.1 (in-place) | — | ✅ backfill contact_type_id | ✅ | ✅ |
| v1.3.0 (in-place) | — | ✅ (no-op) | ✅ (no-op) | ✅ (no-op) |

---

## 🐛 Correcciones

- **Base de datos vacía (0 bytes) en instalación nueva** — `database.py:init_db()` importaba `models` con `import models` (cargaba un segundo módulo `database` independiente creando un `Base` separado; `create_all()` no encontraba tablas). Corregido invirtiendo el orden: `from . import models` primero.
- **Error `table supplier_contacts has no column named contact_type`** — `migrate_database.py` y `migrate_supplier_contacts.py` usaban la columna legacy `contact_type` (texto). Ambos scripts corregidos para usar `contact_type_id` (FK).
- **`init_lovs.py` no sembraba `ContactType`** — la tabla `contact_types` nunca se creaba ni se llenaba. Corregido agregando `ContactType` al import, a la lista de tablas, y a los datos por defecto.
- **`migrate_db_schema.py` nunca se llamaba durante upgrades** — los upgrades in-place no ejecutaban ningún script de migración de esquema. Corregido en `setup-auto.ps1`.
- **`migrate_supplier_contacts.py` no era idempotente** — una segunda ejecución duplicaba todos los contactos. Corregido con verificación de contactos existentes por `supplier_id`.
- **`cleanup_installation.ps1` no encontrado** — ruta construida con `Split-Path $PSScriptRoot -Parent` producía `C:\scripts\...` en lugar de `C:\SistemaProveedores\scripts\...`. Corregido usando `$installPath` directamente.
- **Contactos no migrados en migración cross-path (v0.1 → v1.x)** — el bloque `migrate_supplier_contacts.py` estaba dentro del bloque `isSameDb == false`, por lo que nunca ejecutaba para upgrades in-place. Movido fuera del bloque.

---

## ⚠️ Cambios de Ruptura

- La columna `contact_type` (texto) en `supplier_contacts` queda en desuso. La columna `contact_type_id` (FK a `contact_types`) es el campo oficial. La columna legacy se preserva por compatibilidad pero no se usa en código nuevo.

---

## 📋 Notas de Actualización

### Desde v1.3.0 o v1.2.1 (in-place)
1. Ejecuta el instalador NSIS `.exe` sobre la instalación existente.
2. Elige **"Actualizar"** en la pantalla de tipo de instalación.
3. El instalador aplica cambios de esquema, siembra LOV faltantes y migra contactos automáticamente.
4. La base de datos y configuración existentes se preservan.

### Desde v1.0 (in-place)
1. Igual que arriba. Adicionalmente se agregarán las columnas FK nuevas a las tablas existentes.

### Desde v0.1 (estructura flat)
1. El instalador detecta la estructura antigua y ejecuta una migración completa de datos al nuevo esquema.
2. Se crea un backup automático antes de migrar.

---

## 🐞 Problemas Conocidos

- Las plantillas de órdenes personalizadas (`config/order_template_*.html`) se sobreescriben durante la instalación/upgrade.
- Botón de compartir por email/WhatsApp en órdenes no implementado.
- El desinstalador no elimina todos los archivos/carpetas; requiere limpieza manual en algunos casos.
- La vista previa de órdenes puede mostrar una segunda vista al imprimir.

---

## 📁 Archivos Modificados

- `api/database.py` — corrección de import de modelos en `init_db()`
- `api/init_lovs.py` — agrega `ContactType` al seeding
- `scripts/migrate_database.py` — delega contactos a script dedicado
- `scripts/migrate_supplier_contacts.py` — usa `contact_type_id`, es idempotente, backfill para v1.2.1
- `installers/setup-auto.ps1` — llama `migrate_db_schema.py`, `init_lovs.py` en upgrades in-place; contactos fuera del bloque `isSameDb`; ruta de cleanup corregida
- `installers/modules/Initialize-System.ps1` — llama `init_lovs.py` después de crear DB
- `installers/proveedores.nsi` — despliega `requirements.txt`; detiene instancias antes de copiar archivos

---

## 👥 Contribuidores

Equipo de Desarrollo Proveedores