# 6
## Regeln

für einen erfolgreichen OpenStack-Einsatz

Note: ... die folgenden 6 Regeln zu bedenken, wenn Sie OpenStack bei
sich im Unternehmen einsetzen. Vorab: die sind nicht nach Wichtigkeit
geordnet, und auch nicht chronologisch. Ich empfehle Ihnen, Sie alle
als gleich wichtig zu betrachten und sie alle zu bedenken, bevor Sie
mit einer Umsetzung loslegen.


# 1

Wähle deine OpenStack-Komponenten

Note: OpenStack ist nicht ein monolithisches
Softwareprojekt. OpenStack besteht aus nicht weniger als 60
Teilprojekten, von denen nur 6 als Core-Komponenten gelten (das sind
jene, die eine Compute-Cloud mit Basisfunktionalität
ausmachen). Welche man sonst noch braucht, ist sehr stark abhängig vom
unternehmensspezifischen Einsatz: welche Services möchte ich mit
OpenStack anbieten? Überlege ich einen reinen Private-, Public- oder
Hybridcloud-Einsatz? Plane ich eine Einführung von
OpenStack-Funktionalität in Phasen? Was wollen meine Benutzer oder
Kunden von mir?

Beispiele: Automatisierung beliebig komplexer virtueller Umgebungen
ist normalerweise ein Muss für alle OpenStack-Anwendungen (OpenStack
Heat). Im Telco-Bereich findet sich oft Bedarf für Application Catalog
Management; in diesem Fall ist der Einsatz von OpenStack Murano
zumindest anzudenken. Im klassischen Webhosting-Bereich wird man
DNSaaS eher brauchen als anderswo, das wäre dann ein Fall für
OpenStack Designate. Forschungseinrichtungen haben oft Bedarf für Big
Data as a Service (OpenStack Sahara für Hadoop, Spark).


# 2

Wähle deine Plattform

Note: wenn ich weiß, welche OpenStack-Services ich zumindest
mittelfristig einsetzen will, kann ich unter den recht vielfältigen
OpenStack Distro-Versionen mit der Auswahl beginnen. Nicht jeder
Anbieter von OpenStack-Distros bietet Unterstützung für jedes
Teilprojekt, und auch die Qualität der Packages für einzelne
Linux-Distros ist unterschiedlich. Dazu kommen Unterschiede in der
Unterstützung für Virtualisierungskomponenten (reicht uns Libvirt/KVM,
oder brauchen wir in unserer OpenStack-Umgebung auch Hyper-V oder
VMware?), Storage und Networking.

Man ist normalerweise ziemlich schlecht beraten, wenn das wesentliche
Kriterium für die Auswahl einer OpenStack-Distro ausschließlich die
bestehende Supportbeziehung mit einem bestimmten Hersteller ist. Der
Einsatz einer OpenStack-Umgebung geht normalerweise auch mit einem
recht fundamentalen Umbau in der Rechenzentrumsarchitektur einher; man
trifft also ohnehin schon weitreichende strategische
Entscheidungen. Da kann man durchaus auch schonmal den
Distro-Anbieter überdenken. Es hilft mir nicht, eine gute Beziehung zu
SUSE zu haben, wenn deren Produkt für mich nicht passt, gleiches gilt
für Red Hat, Canonical, oder Mirantis.


# 3

Wähle deine Deployment-Automatisierung

Note: Eine OpenStack-Produktionsumgebung manuell, ohne Zuhilfenahme
von Deployment-Automation installieren zu wollen, sollte eigentlich
ein Entlassungsgrund sein: das wäre keine fahrlässige Inkompetenz,
sondern da wäre Vorsatz zu unterstellen. Gleiches gilt aber in
abgeschwächter Form auch für den Versuch, die Deployment-Automation
für das eigene Unternehmen selbst zu entwickeln. Zum Vergleich: Red
Hats *eigenes* unterstützte Deployment-Methode ist jetzt in der
dritten Iteration, und wir reden von einem Unternehmen mit tausenden
Entwicklern.

*Welche* Deployment Automation man einsetzen möchte, ist hauptsächlich
abhängig von der gewählten Plattform. Und sie bedeutet oft eine
Festlegung auf einen bestimmten Hersteller: OSP Director bei Red Hat,
Juju bei Ubuntu, Chef/Crowbar bei SUSE OpenStack Cloud. Aber es gibt
Community-Alternativen, wie OpenStack-Ansible.


# 4

Halte dich an Open-Source-Komponenten

Note: OpenStack steht unter der Apache Software License, hierbei
handelt es sich um eine freizügige Lizenz: es ist grundsätzlich
zulässig und möglich, nicht open-source-lizenzierte Software gemeinsam
mit OpenStack zu betreiben. Das hat sehr stark zur Popularität von
OpenStack beigetragen und ist vermutlich mit ein Grund für den großen
Erfolg von OpenStack -- im Gegensatz zur Private Cloud-Lösung
Eucalyptus, die unter der GPL3 steht. Allerdings zieht dieser Umstand
auch Anbieter an, deren Motivation im OpenStack-Kontext als eher
fragwürdig betrachtet werden muss. Für einen erfolgreichen Einsatz von
OpenStack-Komponenten gilt daher:

* setze nur solche Plugins und Backends für OpenStack-Komponenten ein,
  deren Entwicklung upstream, d.h. als Teil eines
  OpenStack-Teilprojekts erfolgt. Finger weg von
  out-of-tree-Komponenten.
* im Zweifelsfall empfiehlt sich generell die Verwendung von
  Komponenten, die vollständig unter einer Open Source-Lizenz stehen.


# 5

Orchestrierung ist Pflicht

Note: Ohne **durchgehende** Orchestrierung lässt sich OpenStack nicht
sinnvoll verwalten. Das bedeutet, in einer produktiven
OpenStack-Umgebung *muss* es Log-Aggregation und -Suche,
vereinheitliches qualitatives und quantitatives Monitoring,
vereinheitliches Hardening, und automatisierte Updates geben. Wenn
jemand per SSH als root an eine Kiste ranmuss, um ein kritisches
Problem zu fixen, dann hat man gewaltig was falsch gemacht. Auch
hierfür gibt es Standardlösungen von Herstellern und aus der
OpenStack-Community, wer diese einsetzt, macht's richtig -- wer nicht,
handelt grob fahrlässig.

Im sinnvollen OpenStack-Einsatz gilt das auch für die Verwaltung
virtueller Umgebungen. OpenStack bietet eine Vielzahl an
Möglichkeiten, wie virtuelle Umgebungen vollautomatisiert hochgezogen
und verwaltet werden können (OpenStack Heat, Juju, Ansible, Cloudify,
CloudFoundry und andere).


# 6

Arbeite mit Experten

Note: OpenStack ist nicht nur ein komplexes, sondern auch ein
verhältnismäßig junges Fachgebiet. Obwohl OpenStack bereits seit 7
Jahren existiert, ist es erst seit etwa 3 Jahren
unternehmenstauglich. Zudem haben wir speziell in Mitteleuropa
gegenüber anderen Märkten (USA, Israel) das Problem, dass es bei uns
nie eine große Migration in Public Clouds gegeben hat. Vielen
Unternehmen fehlt daher nicht nur Wissen über OpenStack im Speziellen,
sondern über Cloud-Technologie im Allgemeinen. Für einen erfolgreichen
OpenStack-Einsatz hat man also folgende Optionen:

- Junge Kolleg(inn)en fördern, die Cloud-Wissen bereits mitbringen
- Gezielt Cloud-Wissen aufbauen
- Externe Experten ins Team holen


1. **Wähle deine OpenStack-Komponenten**
2. **Wähle deine Plattform**
3. **Wähle deine Deployment-Automatisierung**
4. **Halte dich an Open-Source-Komponenten**
5. **Orchestrierung ist Pflicht**
6. **Arbeite mit Experten**
