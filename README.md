# Zabbix Public

Community Zabbix templates and practical monitoring documentation maintained by **Apamate**.

[Español](README.es.md)

## Template catalog

| Template | Export format | Reported validation | Guide |
|---|---|---|---|
| [IBM Storage Monitoring by REST API](templates/ibm/ibm_storage_monitoring_by_rest_api.yaml) | Zabbix 7.4 | IBM FlashSystem 5000, firmware 8.4.0.6, as recorded in the supplied template | [Installation](docs/ibm/README.md) |

The catalog will grow as more templates and documentation are contributed. Compatibility with other models or Zabbix versions is not yet confirmed.

## Getting started

1. Open the template guide and review requirements.
2. Download the YAML using the file's **Raw / Download raw file** option, or download the repository ZIP.
3. Import the YAML into Zabbix and configure the host macros described in the guide.
4. Verify data collection and discovery before relying on alerts.

## Repository layout

- `templates/<vendor>/`: importable Zabbix templates.
- `docs/<vendor>/`: setup, validation and troubleshooting guides.
- `CHANGELOG.md`: changes to published resources.

## Contributing

Use Issues for problems and suggestions, or submit a pull request. Include the Zabbix version, device model, firmware, reproduction steps and sanitized errors. Remove credentials, tokens, internal addresses and identifying device data from examples.

This is a community project, not an official IBM or Zabbix integration. 

## License

The templates and documentation in this repository are available under the [MIT License](LICENSE). Copyright (c) 2026 Apamate.
