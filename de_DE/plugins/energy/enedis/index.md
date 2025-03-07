# Enedis Plugin

Plugin zur Wiederherstellung von Stromverbrauchsdaten von intelligenten Zählern *(Linky zum Beispiel)* durch die Befragung der [Kundenkonto **Enedis**](https://mon-compte.enedis.fr/auth/XUI/#login/&realm=/enedis&forward=true){:target = "\_ leer"}.

>**Wichtig**
>
>Das Plugin wurde im Februar 2021 komplett neu geschrieben **die offizielle Enedis Data-Connect API**. Wenn Sie das Plugin zuvor verwendet haben, laden wir Sie ein, ein neues Gerät zu erstellen oder alle Steuerelemente eines früheren Geräts zu löschen.

Es ist möglich, auf Daten von zuzugreifen **Verbrauch**, von **Produktion** oder zu den 2 Messarten direkt in einem Gerät.

Für jede Messart werden 5 Daten angegeben :
- die **stündlicher Verbrauch** pro halbe Stunde *(in kW)*.
- die **Täglicher Verbrauch** *(in kWh)*.
- die **monatlicher Verbrauch** *(in kWh)*.
- die **Jahresverbrauch** *(in kWh)*.
- die **maximale Kraft** *(in kVA)*.

>**INFORMATION**  
>    
>Da die Daten nicht in Echtzeit verfügbar sind, ruft das Plugin die Stromverbrauchsdaten vom Vortag ab.

Solange das Plugin nicht alle Daten vom Vortag abgerufen hat, werden die Enedis-Server weiterhin stündlich zwischen 7.00 und 20.00 Uhr abgefragt. Andernfalls werden Anrufe bis zum nächsten Tag ausgesetzt.

# Configuration

Wie jedes Jeedom-Plugin auch das Plugin **Enedis** muss nach der Installation aktiviert werden.

## Abhängigkeitsmanagement

Das Plugin erfordert das Vorhandensein des Linux-Pakets `php-mbstring`, das normalerweise standardmäßig vorhanden ist, daher muss der Abhängigkeitsstatus sein **In Ordnung** sobald das Plugin installiert ist. Andernfalls klicken Sie auf die Schaltfläche **Beleben** um das fehlende Paket zu installieren.

## Plugin Konfiguration

Wenn Sie dies noch nicht getan haben, autorisieren Sie zunächst die Freigabe von Enedis-Daten mit Jeedom, indem Sie auf die Schaltfläche klicken **Autorisieren Sie den Zugriff auf Enedis-Server : Ich greife auf meinen Enedis-Kundenbereich zu** von der Plugin-Konfigurationsseite :      

![Lien espace-client Enedis](./images/link_enedis.png)

Sie werden dann zu dieser Seite weitergeleitet, auf der Sie informieren müssen **Ihre Anmeldedaten für den Jeedom-Markt** Klicken Sie dann auf die Schaltfläche **Bestätigen** :      

![Authentification compte Market Jeedom](./images/Auth_Jeedom.png)

Weiterleitung zur Enedis-Einwilligungsseite, auf der dies erforderlich ist **Aktivieren Sie das Kontrollkästchen** und klicken Sie auf **Bestätigen** :     

![Autorisation Enedis](./images/Auth_Enedis.png)

Sobald die Datenfreigabe überprüft wurde, wird diese Seite angezeigt :     

![Succès](./images/Auth_Enedis_success.png)

>**Wichtig**
>    
>Wenn Sie auf keine dieser Seiten zugreifen können, deaktivieren Sie den Browser-Werbeblocker.

## Gerätekonfiguration

Zugriff auf die verschiedenen Geräte **Enedis**, Gehe zum Menü **Plugins → Energie → Enedis**.

>**INFORMATION**
>    
>Die Schaltfläche **+ Hinzufügen** Ermöglicht das Hinzufügen eines neuen Messgeräts / einer neuen PDL.

Nachdem die Datenfreigabe auf der Plugin-Konfigurationsseite autorisiert wurde, müssen Sie nur noch eingeben **die Identifikationsnummer der Lieferstelle** besorgt *(PDL)* und der **Art der Messung** zurück zu bekommen.

Während der ersten Sicherung eines aktiven und konfigurierten Geräts erstellt das Plugin automatisch die erforderlichen Befehle und integriert die seit dem 1. Januar des laufenden Jahres auf der Enedis-Site verfügbaren Historien. Dieser Vorgang dauert wahrscheinlich einige Minuten. Sie können den Fortschritt über das Menü verfolgen **Analyse → Protokolle** *(meldet sich an ``debug``)*.

>**TIPP**
>
>Wenn das Plugin aus dem einen oder anderen Grund die Historien beim Erstellen der Bestellungen nicht abrufen konnte, reicht es aus, die Bestellungen zu löschen und dann die Ausrüstung zu speichern, um die Bestellungen und ihre Historie erneut zu generieren.

>**INFORMATION**
>
>Die stündlichen Verbrauchsdaten werden höchstens in den letzten 7 Tagen abgerufen.

## Daten hinzufügen

Es ist möglich, Historien bei Bedarf bis zu 3 Jahren direkt von der Enedis-Site aus zu integrieren. Klicken Sie dazu einfach auf die blaue Schaltfläche **Historische Ergänzungen** von der Registerkarte **Aufträge** eines Ausrüstungsgegenstandes in der Spalte **Aktion** der betreffenden Bestellung :

![Ajout d'historiques](./images/enedis_addHistory.png)

Wählen Sie dann das Startdatum und klicken Sie auf **In Ordnung** um den Prozess zu initiieren.

Die Daten für Tag, Monat, Jahr und maximale Leistung werden ab dem gewählten Datum bis zum 1. Januar des laufenden Jahres integriert. Die stündlichen Daten werden, wenn sie vorliegen, bis zu 7 Tage nach dem gewählten Datum integriert.

>**INFORMATION**
>
>Diese zeitlichen Einschränkungen werden von Enedis festgelegt.

# Widget-Vorlage

>**INFORMATION**
>     
>Die Widget-Vorlage wird sowohl auf Desktop- als auch auf Mobilversionen angezeigt.

Das Plugin bietet die Möglichkeit, Verbrauchs- und / oder Produktionsdaten in einer Widget-Vorlage anzuzeigen, die das Erscheinungsbild eines Zählers imitiert *Linky*. Der Klick auf die Schaltfläche "**- \.| +**" ermöglicht den Wechsel vom Verbrauch zur Produktion für diejenigen, die Zugang zu zwei Arten von Maßnahmen haben.

![Widget-Vorlage](./images/enedis_screenshot1.png)

Um diese Option zu aktivieren, aktivieren Sie einfach das Kontrollkästchen **Widget-Vorlage** auf der allgemeinen Seite der betreffenden Ausrüstung. Sobald das Kontrollkästchen aktiviert ist, können Sie mit einer Option die Hintergrundfarbe des Widgets auswählen *(Standardmäßig 163, 204, 40)*.

>**TIPP**
>     
>In der Desktop-Version passen sich die im Widget angezeigten Informationen an die Größe an, wenn die Größe der Kachel geändert wird.
