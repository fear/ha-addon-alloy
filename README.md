# Homelab-Apps für Home Assistant

Quelle: Gitea `felix/ha-addon-alloy` (intern), gespiegelt nach GitHub, damit der HA-Supervisor das Repository
ohne Anmeldung und mit gültigem Zertifikat laden kann. Keine Geheimnisse im Repo (nur Konfiguration und das
öffentliche Root-Zertifikat der Heim-CA).

## Homelab Alloy (`homelab_alloy`)

Schickt das HAOS-Journal (HA Core, Supervisor, alle Apps) per Grafana Alloy an Loki. Label `host` frei wählbar,
Root-CA der Heim-CA im Image, Alloy-Version fest und per SHA256 geprüft, Web-UI nur innerhalb des Containers.

Abgeleitet von https://github.com/ecohash-co/ha-addon-alloy (MIT, siehe `homelab_alloy/LICENSE.ecohash`).

### Neue Alloy-Version
`ALLOY_VERSION` und `ALLOY_SHA256` (aus `SHA256SUMS` des Releases) im Dockerfile ändern und `version` in
`homelab_alloy/config.yaml` erhöhen – HA bietet das Update dann von selbst an.
