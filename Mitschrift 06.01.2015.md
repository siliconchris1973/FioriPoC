ivv SAP Portal und Fiori Showcase - 06.01.2015
Umgebung:
SAP Portal 7.4 SP 8 - neu installiert

Ablauf des Showcases:
1. Fiori Showcase auf Desktop aufsetzen
2. News-Seite mit WebPage Composer bereitstellen
3. OpenText für News-Seite nutzen

SAP Fiori ShowCase
- Urlaubsantrag
- Geburtstagsliste
- BW-Reports, wenn die Zeit noch reicht

Was gebraucht wird:
SAP Fiori Launchpad im Portal
SAP ERP mit SAP Fiori Principal Apps
SAP NetWeaver Gateway

Landscape:

+-----------+
| Launchpad |					SAP Portal
|           |
| SAP Portal|
| Java 7.40 |
+-----------+
      | ODATA / HTML
+-----------+
| NW Gateway|
  - - - - - - -
|           |					Frontend Server
| SAP Fiori |
| UI AddOns |
|           |
| ABAP 7.31 |
+-----------+
      | Trusted RFC
+-----------+
| SAP Fiori |					Backend Server
|Integration|
| Services  |
|           |
| ERP 6.0   |
+-----------+

Release Stände:
SAP Portal
NW Java 7.4 SPS 08

Frontend Server
NW ABAP 7.31 SPS 04 oder
        7.4 SPS 04

Backend Server
ERP 6 auf ECC 6.0 SP 15 mit EHP 7 SPS 02
NW ABAP 7.0 SPS 18 oder
        7.31 SPS 04

Installations-Optionen:
1. Frontend- und Backend-Server auf einer Maschine
2. Frontend- und Backend-Server auf getrennten Systemen - gewählte Variante


Installation der UI AddOns auf dem Frontend-Server
http://help.sap.com/saphelp_fiorierpx1_100/helpdata/en/d0/fa7252752e9f11e10000000a441470/content.htm

UI ADD-ON 1.0 FOR NW 7.03
FIORI ERP APPLICATIONS X1 1.0
FIORI APPROVE REQUESTS X1 1.0


Installation der Integrations-Komponenten auf dem Backend-Server
http://help.sap.com/saphelp_fiorierpx1_100/helpdata/en/be/8e7a528741a011e10000000a441470/content.htm

FIORI ERP APPLICATIONS X1 1.0

SAP NetWeaver Gateway
Konfiguration entsprechend Anweisungen von SAP
http://help.sap.com/saphelp_gateway20sp07/helpdata/en/4c/a670b0e36c4c01ae2b9a042056f9dc/content.htm?frameset=/en/57/a41787789c4eca867d9a09696fc42c/frameset.htm&current_toc=/en/57/a41787789c4eca867d9a09696fc42c/plain.htm&node_id=17&show_children=false


Einrichtung Frontend Server:
Siehe auch SAP Note 2062518
Siehe auch SAP Note 2062465

Anlage neuer eingehender HTTP-Port 8001 
icm/server_port_2 PROT=HTTP, PORT=8001

Transaktion SICF
default_host/sap/opu/odata/iwfnd/userservice
default_host/sap/opu/odata/sap/epm_oia_fiori_gw_service_srv
default_host/sap/opu/odata/sap/epm_oia_fiori_srv

Einrichtung Trusted RFC 
URL für Benutzerkontenaktivierung bearbeiten 
	-> OData Service USERREQUESTMANAGEMENT
	-> Activation URL http://ap8a212.ivv-verbund.de:8881/fiori/usermgmt

Nummernkreis für Benutzer wurde unverändert belassen.
Dies ist nur bei produktivem Einsatz, bei dem evtl. auch externe Nutzer einen Fiori Service nutzen sollen.

RFC Destination 
Im T1H Mandant 200 - Transaktion SM59 - Neue RFC Verbindung Typ 3

Name: TGW_CLNT_000
Beschreibung: RFC Destination für Benutzerreplikation
Ziel: ap8a212.ivv-verbund.de 01
User: DDIC
Pwd: xxxx
Mandant 000

Im TGW Mandant 000 - Erzeugung RFC-Destination für Benutzerreplikation anlegen
Implementierungstyp: IWBEPUM
RFC-Destination Name: TGW_CLNT_000



SPRO -> SAP NetWeaver -> Gateway-Service-Aktivierung -> Backend-ODFATA-Channel SAP NW Gateway EINstellungen: