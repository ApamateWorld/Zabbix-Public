# Zabbix Public

Plantillas comunitarias de Zabbix y documentación práctica de monitoreo mantenidas por **Apamate**.

[English](README.md)

## Catálogo de plantillas

| Plantilla | Formato de exportación | Validación registrada | Guía |
|---|---|---|---|
| [IBM Storage Monitoring by REST API](templates/ibm/ibm_storage_monitoring_by_rest_api.yaml) | Zabbix 7.4 | IBM FlashSystem 5000, firmware 8.4.0.6, según la descripción de la plantilla original | [Instalación](docs/ibm/README.es.md) |

El catálogo crecerá con nuevas plantillas y documentación. No está confirmada la compatibilidad con otros modelos o versiones de Zabbix.

## Primeros pasos

1. Revisa los requisitos de la guía.
2. Descarga el YAML mediante **Raw / Download raw file**, o descarga el ZIP del repositorio.
3. Importa la plantilla en Zabbix y configura las macros del host.
4. Comprueba la recolección de datos y el descubrimiento antes de depender de las alertas.

## Organización

- `templates/<fabricante>/`: plantillas importables.
- `docs/<fabricante>/`: instalación, validaciones y solución de problemas.
- `CHANGELOG.md`: historial de cambios.

## Contribuciones

Puedes reportar problemas o sugerencias mediante Issues y proponer cambios mediante pull requests. Incluye versión de Zabbix, modelo, firmware, pasos para reproducir y errores anonimizados. Retira credenciales, tokens, direcciones internas y datos identificativos de los equipos.

Proyecto comunitario; no es una integración oficial de IBM ni de Zabbix. 

## Licencia

Las plantillas y la documentación de este repositorio están disponibles bajo la [licencia MIT](LICENSE). Copyright (c) 2026 Apamate.
