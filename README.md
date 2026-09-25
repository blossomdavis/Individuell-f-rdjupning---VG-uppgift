# Individuell fördjupning - VG-uppgift

Kurs: Introduktion till yrkesrollen och grunderna i IT-infrastruktur (MYH 2025/4008)

Examinationsform: Individuell teknisk fördjupningsuppgift (Summativ examination)

Av: Blossom Davis\
Datum: 2026-10-02

## Moment A: Avancerad Nätverksanalys & Trafikflöden
Illustration av datatrafikflöde:

![text](länk)


### Vad händer - steg för steg
**1. DNS-uppslag**

Klienten "Labb-miljö" vill nå hemsidan "Systementor.se". För att datorn ska veta att vi vill komma till systementor.se används: DNS-uppslag. 

Datorn skickar en förfrågan till DNS-servern, även kallad Domain Name System som översätter sökningen 
"systementor.se" till en publik IP-adress, som returneras till datorn. 

**2. Destination och Gateway**

Nu har datorn fått IP-adressen till målet, dock ligger IP-adressen utanför nätverket. För att kunna ta oss till det andra subnätet behövs det att data skickas genom 
Standard Gateway (routern).

Om datorn inte har MAC-adressen till routern  används ARP (adress resolution protocol), den hjälper datorn att hitta MAC-adressen som tillhör routerns IP-adress.

**3. Inkapslingen (TCP/IP-modellen)**

Nu byggs datapaketet ihop (uppifrån och ner) på klienten. 

- **Applikations lagret** genererar datan - en förfrågan om att besöka systementor.se. 

- **Transport lagret** lägger på en TCP-header med en slumpmässig (52431) källport och en mål port (443 för https). 

*Applikations och Transport lagret skapar ett "segment".*

- **Nätverks lagret** lägger på en IP-header med datorns lokal IP som källa och "systementor.se" publika IP som mål-destination. 

*Segmentet och IP-header skapar ett "paket"*

- **Länk lagret** kapslar in paketet i en "frame" där den lägger på sin egen MAC-adress som källa och routerns MAC-adress som mål-destination. 

- **Fysiska lagret** omvandlar frame:n till elektriska signaler eller radiovågar (bits) och skickas genom kabeln eller luften. 

*Den lila kopplingen symboliserar elektricitet genom kabel för att överföra bits.*

**4. Lokal överföring**

**4a. Switchen**\
Switchen tar emot signalerna och läser destinationens MAC-adress och skickar vidare den till rätt port som leder till routern. 

**4b. Routern**\
Routern tar emot den och dekapslar frame-header och trailer för att visa paketet. Sedan läser den av destinationens (systementor.se) IP-adress i IP-header, för att veta vart den ska. 

Routern byter ut datorns privata IP-adress till routerns publika IP-adress, via Network Adress Translation (NAT). Routern packar sedan in paketet i en ny frame justerad till nästa nätverk och skickar det vidare till internetleverantören (ISP).

**5. Transport över Internet**\
Men innan den har nått mål-destinationen så har den hoppat mellan ett flertal routrar över internet (BGP-protokollet). 

Sedan när paketet når mål-destinationen passerar den brandväggar och en Load Balancer som dirigerar trafiken rätt. Målservern tar emot paketet, dekapslar paketet och hanterar TCP-handskakningen och förbereder ett svar.

Svaret skickas tillbaka på samma sätt, den omvända vägen.


## Moment B: Jämförande OS- och Behörighetsanalys
- Beskrivning av företagscenariot och syftet med behörigheterna osv. 

### Linux
- Dokumentation av kommandon (groupadd, chown, chmod, setgid), samt resultat.

### Windows
- Dokumentation av kommandon (net ..., icacls), samt resultat. 

### Test av kommandon
- bob lyckas i "Gemensamt" men misslyckas i "Ledning"


### Analys
- Hur arv fungerar (L: POSIX & W: NTFS), jämförelsetabell
- Flexibilitet i behörighetsmodeller (POSIX 3-nivåer och NTFS obegränsade)
- Slutsats kring säkerhet och admin i operativsystemen. 

## Moment C: Spårbarhet & Överlämningsdokumentation
Färdigställa en komplett system- och driftdokumentation för hela labbmiljön.

INNAN INLÄMNING: "Kan en extern tekniker ta över och återställa miljön enbart utifrån detta dokument utan att behöva ställa frågor?"  
