# AEGIS - AntiDoS

[switch to english README](README.md)

> das quelloffene (D)DoS-Präventionssystem

![AEGIS](doc/img/aegis_logo_with_name.jpg)

AEGIS zielt darauf ab, Ihr System gegen Denial-of-Service-Angriffe durch eine effiziente Verarbeitung von Paketen im Benutzerraum zu schützen. Es wurde im Rahmen eines Softwareprojektes an der TU Ilmenau entwickelt.

Dieses Projekt wurde von der Universität Ilmenau zum [besten Softwareprojekt 2021](doc/img/Bestes%20Softwareprojekt.pdf) ausgezeichnet.


### Software Project
Die Vorlesung vermittelt Studierenden der Informatik und Ingenieurinformatik Methoden und Techniken des Software-Engineering. Durch die Einbettung der Aktivitäten in den Softwareentwicklungsprozess wird das Wissen vertieft. Die Lehrveranstaltung beinhaltet die Entwicklung von Softwarearchitekturzielen, Beschreibungsansätze der verschiedenen Modelle und Dokumente, Vorgehen bei der Entwicklung (Prozesse), Entscheidungsfindung, Architekturstile/-muster und deren Qualitätsmerkmale, sowie die Prüfung/Bewertung von Architekturen.

DIe Mitglieder dieses Projektes sind:
- Fabienne Göpfert [@fabgoepfert](https://github.com/fabgoepfert)
- Felix Husslein [@felixhusslein](https://github.com/felixhusslein)
- Tim Häußler [@tlhaeussler](https://github.com/tlhaeussler)
- Robert Jeutter [@Wieerwill](https://github.com/wieerwill)
- Johannes Lang [@JojoBande](https://github.com/JojoBande)
- Leon Leisten
- Jakob Lerch [@jklerch](https://github.com/jklerch)
- Tobias Scholz

### TU Ilmenau
Die Technische Universität Ilmenau ist eine Universität des Freistaates Thüringen in Ilmenau. Sie hat fünf Fakultäten, von denen eine die Informatik im Bachelor lehrt.

### Das Problem mit (D)DoS
Denial-of-Service-Angriffe stellen eine ernstzunehmende und stetig wachsende Bedrohung dar.
Im digitalen Zeitalter sind viele Systeme über das Internet oder private Netzwerke miteinander verbunden. Viele Unternehmen, Krankenhäuser und Behörden sind durch unzureichende Schutzmaßnahmen und große Wirkung zu beliebten Angriffszielen geworden ([infopoint-security.de](https://www.infopoint-security.de/cyber-angriffe-auf-deutsche-krankenhaeuser-sind-um-220-prozent-gestiegen/a26177/)). Bei solchen Angriffe werden in der Regel finanzielle oder auch politische Gründe verfolgt, selten aber auch die bloße Störung oder Destruktion des Ziels.

Bei DoS\footnote{Denial of Service, dt.: Verweigerung des Dienstes, Nichtverfügbarkeit des Dienstes}- und DDoS\footnote{Distributed Denial of Service}-Attacken werden Server und Infrastrukturen mit einer Flut sinnloser Anfragen so stark überlastet, dass sie von ihrem normalen Betrieb abgebracht werden. Daraus kann resultieren, dass Nutzer die angebotenen Dienste des Betreibers nicht mehr erreichen und Daten bei dem Angriff verloren gehen können.
Hierbei können schon schwache Rechner große Schaden bei deutlich leistungsfähigeren Empfängern auslösen. In Botnetzen können die Angriffe zusätzlich von mehreren Computern gleichzeitig koordiniert werden, aus verschiedensten Netzwerken stammen ([tecchannel.de](https://www.tecchannel.de/a/trend-micro-latente-gefahr-durch-botnet-sdbot,2024687)) und damit gleichzeitig die Angriffskraft verstärken und die Erkennung erschweren.

Das Ungleichgewicht zwischen der Einfachheit bei der Erzeugung von Angriffen gegenüber komplexer und ressourcenintensiver DoS-Abwehr verschärft das Problem zusätzlich. Obwohl gelegentlich Erfolge im Kampf gegen DoS-Angriffe erzielt werden (z.B. Stilllegung einiger großer ,,DoS-for-Hire'' Webseiten), vergrößert sich das Datenvolumen der DoS-Angriffe stetig weiter. Allein zwischen 2014 und 2017 hat sich die Frequenz von DoS-Angriffen um den Faktor 2,5 vergrößert und das Angriffsvolumen verdoppelt sich fast jährlich ([ns-cdn.neustar.biz](https://ns-cdn.neustar.biz/creative_services/biz/neustar/www/resources/whitepapers/it-security/ddos/2016-apr-ddos-report.pdf)). Die Schäden werden weltweit zwischen 20.000 und 40.000 US-Dollar pro Stunde geschätzt ([datacenterknowledge.com](https://www.datacenterknowledge.com/archives/2016/05/13/number-of-costly-dos-related-data-center-outages-rising)).

Im Bereich kommerzieller DoS-Abwehr haben sich einige Ansätze hervorgetan (z.B. [Project Shield](https://projectshield.withgoogle.com/landing), [Cloudflare](https://www.cloudflare.com/ddos/) oder [AWS Shield](https://aws.amazon.com/de/shield/)). Der Einsatz kommerzieller Lösungen birgt jedoch einige Probleme, etwa mitunter erhebliche Kosten oder das Problem des notwendigen Vertrauens, welches dem Betreiber einer DoS-Abwehr entgegengebracht werden muss. Folglich ist eine effiziente Abwehr von DoS-Angriffen mit eigenen Mitteln ein oft gewünschtes Ziel - insbesondere wenn sich dadurch mehrere Systeme zugleich schützen lassen.

Ziel dieses Softwareprojekts ist es, ein System zwischen der Internet-Anbindung und dem internem Netzwerk zu schaffen, das bei einer hohen Bandbreite und im Dauerbetrieb effektiv (D)DoS Angriffe abwehren kann, während Nutzer weiterhin ohne Einschränkungen auf ihre Dienste zugreifen können. Die entstehende Anwendung implementiert eine (D)DoS-Verkehrs-Inspektion und einen intelligenten Regelgenerator, wodurch interne Netzwerke vor externen Bedrohungen, die zu einer Überlastung des Systems führen würden, geschützt sind. Es enthält Algorithmen zur Verkehrsanalyse, die bösartigen Verkehr erkennen und ausfiltern können, ohne die Benutzererfahrung zu beeinträchtigen und ohne zu Ausfallzeiten zu führen.

### weiterführende Links
[DPDK](https://www.dpdk.org/)

[TU Ilmenau](https://www.tu-ilmenau.de)
