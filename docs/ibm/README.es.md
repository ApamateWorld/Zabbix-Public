# IBM Storage Monitoring by REST API

[English](README.md) · [Catálogo](../../README.es.md) · [Plantilla](../../templates/ibm/ibm_storage_monitoring_by_rest_api.yaml)

## Alcance y validación

La plantilla original registra validación en IBM FlashSystem 5000 con firmware 8.4.0.6. El formato de exportación es Zabbix 7.4. Se realizó una revisión estática para esta publicación; el YAML renombrado no se ha vuelto a importar ni probado contra un equipo durante la publicación.

Un ítem maestro Script consulta cada 5 minutos. Se autentica en `/rest/auth` y consulta por POST `/lssystem`, `/lsnode`, `/lsenclosure`, `/lsdrive`, `/lsmdiskgrp` y `/lsportfc`. Los ítems dependientes y el descubrimiento procesan el resultado.

Incluye 11 ítems, 5 reglas de descubrimiento y 23 prototipos de ítems para capacidad del sistema, nodos, gabinetes, discos, pools y puertos Fibre Channel. No incluye métricas históricas de latencia, IOPS ni rendimiento de transferencia.

## Requisitos e instalación

1. Utiliza una instancia que admita el formato de exportación 7.4. Respalda la plantilla existente si vas a actualizarla.
2. Comprueba el acceso HTTPS desde el servidor Zabbix o proxy asignado hacia la API del storage. El puerto predeterminado es 7443; ajústalo al equipo.
3. Prepara una cuenta dedicada con permisos para autenticarse y ejecutar las consultas indicadas. Verifica el rol necesario en el equipo; no todos los roles de lectura necesariamente permiten acceso a la API.
4. En **Data collection → Templates → Import**, selecciona el YAML y revisa la vista previa. En actualizaciones, evita eliminar entidades existentes si no es tu intención.
5. Vincula la plantilla a un host. Configura explícitamente `{$IBM.API.URL}` con la URL base correcta, o verifica que `{HOST.CONN}` corresponda al storage.
6. Sobrescribe `{$IBM.API.USER}` con la cuenta de monitoreo y configura `{$IBM.API.PASSWORD}` como texto secreto a nivel del host. El valor original de usuario es `admin`; reemplázalo antes de usar la plantilla.
7. Revisa timeout y umbrales de capacidad.

## Macros

| Macro | Default / Predeterminado | Description |
|---|---|---|
| `{$IBM.API.PASSWORD}` | `(empty / vacío)` | REST API password. |
| `{$IBM.API.TIMEOUT}` | `30s` | Timeout of the master Script item. |
| `{$IBM.API.URL}` | `https://{HOST.CONN}:7443/rest` | Base URL of the classic IBM Storage Virtualize REST API. |
| `{$IBM.API.USER}` | `admin` | REST API user. Replace with a restricted monitoring user. |
| `{$IBM.POOL.UTIL.DISASTER}` | `95` | Pool utilization disaster threshold, percent. |
| `{$IBM.POOL.UTIL.HIGH}` | `90` | Pool utilization high threshold, percent. |
| `{$IBM.POOL.UTIL.WARN}` | `80` | Pool utilization warning threshold, percent. |

## Validaciones

- Comprueba que **IBM Storage: Get data** recolecte JSON correctamente.
- Espera un ciclo de consulta y revisa los ítems dependientes y las cinco reglas de descubrimiento.
- Compara nombre, firmware, capacidades y estados con la consola del storage.
- Revisa los puertos Fibre Channel descubiertos y ajusta los umbrales a tu entorno.

## Alertas y solución de problemas

Incluye alertas por ausencia de datos durante 15 minutos; estado de discos, nodos, gabinetes y pools; cantidad de canisters y fuentes en línea; estado Fibre Channel y utilización de pools (80/90/95%).

Ante errores de autenticación, revisa credenciales y permisos. Ante fallos de conexión o timeout, comprueba URL, puerto, rutas, configuración HTTPS y tiempo de espera. Ante errores JSON o de preprocesamiento, compara la respuesta del equipo con el formato esperado. El fallo de cualquiera de los endpoints impide que el ítem maestro devuelva el conjunto completo.

No publiques respuestas de autenticación, tokens ni datasets de producción en Issues. El historial del ítem maestro se conserva un día y puede contener identificadores del equipo.

## Actualizar una instalación existente

Se conservaron los UUID originales. Se renombraron la plantilla y sus referencias en triggers, y el grupo corporativo quedó como `Templates/Empresa Corp`. Revisa la vista previa para confirmar la actualización esperada y prueba antes de aplicar en producción. No se modificó la lógica de consulta del equipo.
