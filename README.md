# AEGIS - AntiDoS

[zum Deutschen README](README_DE.md)

> the open source (D)DoS prevention system

![AEGIS](doc/img/aegis_logo_with_name.jpg)

AEGIS aims to defend your system against denial-of-service attacks through efficient user-space packet processing. It is build during a software project at the TU Ilmenau.

This project was rated [best softwareproject 2021](doc/img/Bestes%20Softwareprojekt.pdf) by the University of Ilmenau.

### Software Project
This lecture teaches students of computer science and engineering informatics methods and techniques of software engineering. By embedding the activities in the software development process, the knowledge is deepened. The course contains the development of software architecture goals, description approaches of the different models and documents, procedure with the development (processes), decision making, architecture styles/patterns and their quality characteristics, as well as the examination/evaluation of architectures.

The members and developers of this project are: 
- Fabienne Göpfert [@fabgoepfert](https://github.com/fabgoepfert)
- Felix Husslein [@felixhusslein](https://github.com/felixhusslein)
- Tim Häußler [@tlhaeussler](https://github.com/tlhaeussler)
- Robert Jeutter [@Wieerwill](https://github.com/wieerwill)
- Johannes Lang [@JojoBande](https://github.com/JojoBande)
- Leon Leisten
- Jakob Lerch [@jklerch](https://github.com/jklerch)
- Tobias Scholz

### TU Ilmenau
Ilmenau University of Technology is a university of the Free State of Thuringia in Ilmenau. It has five faculties of which one teaches computer science in bachelor

### The Problem with (D)DoS
Denial-of-service attacks are a serious and ever-growing threat.
In the digital age, many systems are connected via the Internet or private networks. Many companies, hospitals and public authorities have become popular targets of attack due to inadequate protective measures and high impact ([infopoint-security.de](https://www.infopoint-security.de/cyber-angriffe-auf-deutsche-krankenhaeuser-sind-um-220-prozent-gestiegen/a26177/)). Such attacks are usually carried out for financial or even political reasons, but rarely for the mere disruption or destruction of the target.

In DoS\footnote{Denial of Service} and DDoS\footnote{Distributed Denial of Service} attacks, servers and infrastructures are overloaded with a flood of meaningless requests to such an extent that they are prevented from operating normally. This can result in users no longer being able to reach the services offered by the operator and data can be lost in the attack.
In this case, even weak computers can cause great damage to much more powerful recipients. In botnets, the attacks can additionally be coordinated by several computers at the same time, originate from a wide variety of networks ([tecchannel.de](https://www.tecchannel.de/a/trend-micro-latente-gefahr-durch-botnet-sdbot,2024687)) and thus simultaneously increase the attack power and make detection more difficult.

The imbalance between simplicity in generating attacks versus complex and resource-intensive DoS defenses further exacerbates the problem. Although occasional successes are achieved in the fight against DoS attacks (e.g., shutting down some large "DoS-for-hire" websites), the volume of DoS attack data continues to grow. Between 2014 and 2017 alone, the frequency of DoS attacks has increased by a factor of 2.5 and the attack volume is almost doubling every year ([ns-cdn.neustar.biz](https://ns-cdn.neustar.biz/creative_services/biz/neustar/www/resources/whitepapers/it-security/ddos/2016-apr-ddos-report.pdf)). Damage is estimated at between $20,000 and $40,000 per hour worldwide ([datacenterknowledge.com](https://www.datacenterknowledge.com/archives/2016/05/13/number-of-costly-dos-related-data-center-outages-rising)).

In the area of commercial DoS defenses, some approaches have stood out (e.g., [Project Shield](https://projectshield.withgoogle.com/landing), [Cloudflare](https://www.cloudflare.com/ddos/), or [AWS Shield](https://aws.amazon.com/de/shield/)). However, the use of commercial solutions poses some problems, such as sometimes significant costs or the problem of the necessary trust that must be placed in the operator of a DoS defense. Consequently, an efficient defense against DoS attacks with own means is often a desired goal - especially if several systems can be protected at the same time.

The goal of this software project is to create a system between the Internet connection and the internal network that can effectively defend against (D)DoS attacks at a high bandwidth and in continuous operation, while users can still access their services without restrictions. The resulting application implements (D)DoS traffic inspection and an intelligent rule generator, protecting internal networks from external threats that would overload the system. It includes traffic analysis algorithms that can detect and filter out malicious traffic without affecting the user experience and without causing downtime.

### related links
[DPDK](https://www.dpdk.org/)

[TU Ilmenau](https://www.tu-ilmenau.de)
