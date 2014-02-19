Systemstartvorgang aus Sicht der Quadrokopter
=========

1.  Die Quadrokoptermodule werden gestartet.
2.  Die Quadrokoptermodule melden sich bei der API und erhalten ihre ID.
3.  Ein Quadrokoptermodul scannt den Funkraum und sendet das Ergebnis an die API. 
    Das Modul mit der niedrigsten ID führt die Suche aus.
4.  Die API weist den Quadrokoptermodulen einen Quadrokopter zu.
4b. Quadrokopter bedienen den Blink-Service. Der Benutzer weist mit dem Blink-Service (durch API) den Kanälen 
    der Quadrokopter eine Farbe zu oder die API lädt diese aus einer Datei.
5.  Die API sendet alle vorhandenen Quadrokopter-IDs an das Control-Modul. Das Control-Modul bietet den Service an.
6.  Die Quadrokoptermodule warten auf das Startsignal auf dem System Topic und verbinden sich mit den Quadrokoptern, 
    sobald sie start erhalten.
7.  Das Control-Modul führt den Startprozess aus, die Quadrokopter sind eventuell noch nicht verbunden mit dem 
    Quadrokoptermodul.