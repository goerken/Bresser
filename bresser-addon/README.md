# Bresser Weather Add-on für Home Assistant

Dieses Add-on ermöglicht die Integration von Bresser Wetterstationen in Home Assistant. Es stellt einen kleinen Webserver bereit, der Wetterdaten von der Bresser-Station entgegennimmt und diese als REST-API für Home Assistant bereitstellt.

## Features
- Empfängt Wetterdaten von Bresser WiFi Wetterstationen
- Stellt aktuelle Wetterdaten als REST-API zur Verfügung
- Loggt Wetterdaten als CSV-Dateien

## Installation
1. Kopiere den Ordner `bresser-addon` in das Verzeichnis `addons` oder `addons/local` deiner Home Assistant-Installation.
2. Gehe in Home Assistant zu **Einstellungen → Add-ons → Add-on Store**.
3. Klicke oben rechts auf die drei Punkte und wähle **Lokale Add-ons neu laden**.
4. Das Add-on "Bresser Weather Add-on" sollte nun erscheinen. Installiere und starte es.

## Konfiguration in Home Assistant
Füge in deiner `configuration.yaml` einen REST-Sensor hinzu, z.B.:

```yaml
sensor:
  - platform: rest
    resource: http://[IP_DEINES_HA]:8000/data
    name: Bresser Wetter
    value_template: "{{ value_json.temperature_c }}"
    json_attributes:
      - humidity
      - pressure_hpa
      - wind_speed_kmh
      - rain_mm
      - solar_radiation
```
Passe die IP-Adresse ggf. an.

## Hinweise
- Die Wetterstation muss so konfiguriert werden, dass sie ihre Daten an die URL `http://[IP_DEINES_HA]:8000/weatherstation/updateweatherstation.php` sendet.
- Die geloggten CSV-Dateien findest du im Ordner `logs` des Add-ons.

## Troubleshooting
- Stelle sicher, dass der Port 8000 in Home Assistant freigegeben ist.
- Prüfe die Add-on-Logs bei Problemen.

## Lizenz
Siehe [GitHub-Repository](https://github.com/raphv/bresser-home-assistant) für weitere Informationen.
