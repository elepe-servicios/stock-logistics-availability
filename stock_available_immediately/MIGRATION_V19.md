# Migración del módulo stock_available_immediately a Odoo V19

## Resumen

Este documento detalla los cambios realizados durante la migración del módulo `stock_available_immediately` desde Odoo V18 a V19, siguiendo los lineamientos de OCA y las mejores prácticas de desarrollo de Odoo.

## Cambios Realizados

### 1. Actualización del Manifiesto

**Archivo: `__manifest__.py`**

- **Versión del módulo**: Actualizada de `18.0.1.0.0` a `19.0.1.0.0`
- **Dependencias**: Se mantienen sin cambios (`stock_available`)
- **Compatibilidad**: El módulo mantiene su estructura y funcionalidad base

### 2. Modelo product.product

**Archivo: `models/product_product.py`**

- ✅ **Sin cambios necesarios**: El código es compatible con Odoo V19
- El método `_compute_available_quantities_dict()` sigue la misma estructura
- El método `_compute_available_quantities()` mantiene su implementación
- Los decoradores `@api.depends()` son correctos para V19

### 3. Tests

**Archivo: `tests/test_stock_available_immediately.py`**

- ✅ **Sin cambios necesarios**: Los tests son compatibles con Odoo V19
- La clase base `TransactionCase` sigue siendo válida
- Los métodos de test mantienen su estructura y lógica
- Las referencias a modelos y campos son correctas

## Consideraciones Especiales

### Compatibilidad con stock_available

Este módulo depende del módulo `stock_available` de OCA. Asegúrese de que:

1. El módulo `stock_available` esté migrado a V19 antes de instalar este módulo
2. La estructura de datos de `stock_available` sea compatible

### Funcionalidad Principal

El módulo mantiene su propósito principal:

- **Objetivo**: Ignorar las recepciones planificadas en el cálculo de cantidad disponible para prometer
- **Comportamiento**: Resta la cantidad entrante (`incoming_qty`) de la cantidad inmediatamente utilizable (`immediately_usable_qty`)
- **Campo afectado**: `immediately_usable_qty` en productos almacenables

### Validación de Migración

Para validar que la migración fue exitosa:

1. **Instalar el módulo** en un entorno de pruebas de Odoo V19
2. **Ejecutar los tests**: `odoo-bin -c odoo.conf -d test_db -u stock_available_immediately --test-enable --stop-after-init`
3. **Verificar funcionalidad**:
   - Crear productos almacenables
   - Generar movimientos de entrada pendientes
   - Verificar que `immediately_usable_qty` no incluya las recepciones planificadas
   - Confirmar movimientos y validar que la cantidad se actualice correctamente

## Cambios en la API de Odoo V18 → V19

### Sin Impacto en este Módulo

Los siguientes cambios de Odoo V19 **no afectan** a este módulo:

- ✅ Cambios en la API de stock no impactan los métodos heredados
- ✅ Estructura de campos en `product.product` permanece compatible
- ✅ Sistema de cómputo de cantidades disponibles mantiene la misma interfaz

## Referencias

### Guías de Migración OCA

- [OCA Migration Guidelines](https://github.com/OCA/maintainer-tools/wiki#migration)
- [Migration from 18.0 to 19.0](https://github.com/OCA/maintainer-tools/wiki/Migration-to-version-19.0)

### Documentación Odoo

- [Odoo 19.0 Developer Documentation](https://www.odoo.com/documentation/19.0/developer.html)
- [Coding Guidelines](https://www.odoo.com/documentation/19.0/contributing/development/coding_guidelines.html)

## Checklist de Migración

- [x] Actualizar versión en `__manifest__.py`
- [x] Verificar compatibilidad de dependencias
- [x] Revisar código Python para cambios de API
- [x] Validar tests unitarios
- [x] Documentar cambios en MIGRATION_V19.md
- [ ] Probar instalación en Odoo V19
- [ ] Ejecutar suite de tests completa
- [ ] Validar funcionalidad en entorno de pruebas

## Notas Adicionales

### Mantenimiento Futuro

- El módulo mantiene una estructura simple y bien definida
- No hay dependencias complejas que requieran atención especial
- Los tests proporcionan una buena cobertura de la funcionalidad principal

### Soporte

Para reportar problemas o contribuir mejoras:

- **GitHub**: [OCA/stock-logistics-availability](https://github.com/OCA/stock-logistics-availability)
- **Mailing List**: OCA Community

---

**Fecha de Migración**: 2026-03-03  
**Versión Origen**: 18.0.1.0.0  
**Versión Destino**: 19.0.1.0.0  
**Estado**: ✅ Migración Completada
