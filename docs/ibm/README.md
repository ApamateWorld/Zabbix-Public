# IBM Storage Monitoring by REST API

[Español](README.es.md) · [Catalog](../../README.md) · [Template](../../templates/ibm/ibm_storage_monitoring_by_rest_api.yaml)

## Scope and validation

The supplied template records validation against IBM FlashSystem 5000, firmware 8.4.0.6. The export format is Zabbix 7.4. This publication was checked statically; the renamed export has not been re-imported or tested against a live device during publication.

One Script master item polls every 5 minutes, authenticates through `/rest/auth`, then requests `/lssystem`, `/lsnode`, `/lsenclosure`, `/lsdrive`, `/lsmdiskgrp` and `/lsportfc` using POST. Dependent items and low-level discovery process the response.

Includes 11 template items, 5 discovery rules and 23 item prototypes covering system capacity, nodes, enclosures, drives, pools and Fibre Channel ports. It does not provide historical performance metrics for latency, IOPS or throughput.

## Requirements and setup

1. Use a Zabbix instance that accepts the 7.4 export format. Back up an existing template before updating it.
2. Ensure the Zabbix server or assigned proxy can reach the storage HTTPS REST endpoint. The default port is 7443; adjust it for your system.
3. Prepare a dedicated account with permission to authenticate and run the listed read queries. The required IBM role must be verified on your device; do not assume every read-only role has API access.
4. In **Data collection → Templates → Import**, select the YAML and review the import preview. For updates, avoid deleting existing entities unless intended.
5. Link the template to a host. Set `{$IBM.API.URL}` explicitly to the correct base URL, or ensure `{HOST.CONN}` resolves to the intended storage address.
6. Override `{$IBM.API.USER}` with your monitoring account and set `{$IBM.API.PASSWORD}` at host level as secret text. The supplied username default is `admin`; replace it before use.
7. Review the timeout and pool capacity thresholds below.

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

## Validate collection

- Check the master item **IBM Storage: Get data** for successful JSON collection.
- Allow a polling cycle, then check dependent items and all five discovery rules.
- Compare system name, firmware, capacity and component status against the storage console.
- Review discovered Fibre Channel ports and thresholds for your actual topology.

## Alerts and troubleshooting

The export includes alerts for missing master data for 15 minutes, drive/node/enclosure/pool status, enclosure canister and power-supply counts, Fibre Channel status and pool utilization thresholds (80/90/95%).

For authentication errors, check credentials and API permissions. For connection or timeout failures, check URL, port, routing, HTTPS configuration and timeout. For JSON or preprocessing errors, compare the device response structure with the expected firmware response. A failure in any requested endpoint prevents the master item from returning its full dataset.

Do not attach raw authentication responses, tokens or full production datasets to public Issues. The raw master-item history is configured for one day and may contain device identifiers.

## Updating an existing installation

UUIDs are preserved from the supplied export. The template name and trigger references were renamed; the organization-specific group was anonymized as `Templates/Empresa Corp`. Review the import preview carefully to verify the intended update, and test before applying to production. No device polling logic was changed.
