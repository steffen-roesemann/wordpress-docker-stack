# Wordpress-Docker-Stack
> Wordpress-Docker-Stack ist eine Docker-Compose Datei für die Installation von Wordpress, MySQL, und Adminer in Docker-Containern

Dieses Repository enthält eine Docker-Compose-Datei, um einen Wordpress-Blog mit einer MySQL-Datenbank und der grafischen Konfigurationsoberfläche Adminer für (My-)SQL-Datenbanken über Docker-Container realisieren zu können.

Das Repository dient als persönliches Backup für den Einsatz in einem privaten LAN.

Die Lauffähigkeit der Docker-Container wurde auf einem Ubuntu 23.04 ("Lunar Lobster") getestet.

## Sicherheitsaspekte beim Verwenden von Wordpress-Docker-Stack

Die Verwendung des Wordpress-Docker-Stacks in einer produktiven Umgebung ist NICHT empfohlen, insbesondere über unsichere Netzwerke wie das Internet. Die in der docker-compose.yml gesetzten Passwörter für den administrativen Datenbanknutzer root und den Datenbanknutzer wordpress sind standardmäßig unsicher. Darüber hinaus ermöglicht der Wordpress-Docker-Stack keine sichere Kommunikationsverbinung über TLS via https-Protokoll, so dass die eingegebenen Inhalte und Zugangsdaten im Klartext über http übertragen werden.

## Download des Repositorys und Starten der Docker-Container

```shell
# Klonen des Repositorys und Wechsel in das Verzeichnis
git clone https://github.com/steffen-roesemann/wordpress-docker-stack
cd wordpress-docker-stack

# Starten der Docker-Container für Wordpress, MySQL und Adminer als Dienst
docker-compose up -d
```

Mit dem Starten der Docker-Container über die docker-compose.yml wird ein Verzeichnis "wordpress" im aktuellen Verzeichnis angelegt, in das die Dateien von Wordpress abgelegt werden und bei zukünftigem Bedarf lokal bearbeitet werden können.

Über einen Webbrowser können die Docker-Container dann wie folgt aufgerufen werden:

Für den Wordpress-Blog:

- http://localhost:8080 oder http://{ip-adresse-des-hosts}:8080

Für Adminer:

- http://localhost:8081 oder http://{ip-adresse-des-hosts}:8081

## Hinweise zum Arbeiten mit den Docker-Containern

```shell
# Stoppen der laufenden Container-Dienste
docker-compose down

# Updaten der verwendeten Images
docker-compose pull

# Neustarten der Container als Dienst
docker-compose up -d

# Laufende Docker-Container anzeigen lassen
docker ps

# Alle Docker-Container, Images und Netzwerke löschen (ACHTUNG! Löscht auch alles andere!)
docker system prune -a

# Das Docker-Volume der MySQL-Datenbank anzeigen und löschen
docker volume ls
docker volume rm {Name_des_Ordners}_wordpressdb
```

## Backup und Restore der Wordpress-Datenbank des MySQL-Docker-Containers

```shell
# Backup der Wordpress-Datenbank aus der Docker-MySQL-Datenbank
docker ps # zum Anzeigen des Namens des Docker-Containers
docker exec {Name-des-Ordners}_wordpressdb_1 /usr/bin/mysqldump -u root --password=root wordpress > backup.sql

# Restore des Backups
docker ps # zum Anzeigen des Namens des Docker-Containers
cat backup.sql | docker exec -i {Name-des-Ordners}_wordpressdb_1 /usr/bin/mysql -u root --password=root wordpress
```

## Nutzungsbedingungen

Die folgenden Bedingungen regeln die Nutzung dieser Software. Durch die Verwendung erklären 
ihr euch mit den nachstehenden Bedingungen einverstanden:

Die Software wird "wie sie ist" zur Verfügung gestellt, ohne jegliche ausdrückliche oder stillschweigende Gewährleistung. Dies schließt, aber ist nicht beschränkt auf, Gewährleistungen hinsichtlich der Eignung für einen bestimmten Zweck, der Marktgängigkeit und der Nichtverletzung von Rechten Dritter ein.

Ich übernehme keine Verantwortung oder Haftung für die Richtigkeit, Vollständigkeit, Zuverlässigkeit oder Aktualität der Software oder der damit erzielten Ergebnisse.

In keinem Fall hafte ich für direkte, indirekte, zufällige, besondere oder Folgeschäden, die sich aus der Nutzung oder Unmöglichkeit der Nutzung der Software ergeben, einschließlich, aber nicht beschränkt auf entgangenen Gewinn, Datenverlust, Geschäftsunterbrechung oder jegliche andere kommerzielle Schäden oder Verluste.

Ihr stimmt zu, die Software nur in Übereinstimmung mit den geltenden Gesetzen und Vorschriften zu nutzen. Ich übernehme keine Verantwortung für rechtliche Konsequenzen, die sich aus einer rechtswidrigen Nutzung der Software ergeben.

Ihr erkennt an, dass die Software möglicherweise Fehler, Unvollkommenheiten oder technische Probleme aufweisen kann. Ich übernehme keine Verantwortung für etwaige Schäden oder Datenverluste, die durch solche Probleme verursacht werden.

Jegliche Kommunikation, die über die Software erfolgt, liegt in eurer Verantwortung. Ich hafte nicht für den Inhalt solcher Kommunikation oder die Verwendung, die ihr davon macht.

Durch die Verwendung dieser Software erklärt ihr euch damit einverstanden, auf jegliche Ansprüche, Klagen oder Forderungen gegenüber mir zu verzichten, die sich aus der Nutzung der Software ergeben könnte.
