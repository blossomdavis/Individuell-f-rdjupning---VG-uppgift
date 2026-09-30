# Individuell fördjupning VG-uppgift
```
Kurs: Introduktion till yrkesrollen och grunderna i IT-infrastruktur (MYH 2025/4008)

Examinationsform: Individuell teknisk fördjupningsuppgift (Summativ examination)

Av: Blossom Davis
Datum: 2026-10-02
```

## Moment A: Avancerad Nätverksanalys & Trafikflöden
*Illustration av datatrafikflöde och TCP/IP:*

![alt text](image.png)

### Vad händer - steg för steg
**1. DNS-uppslag**

Klienten "Labbmiljö" vill nå hemsidan "Systementor.se". För att datorn ska veta att vi vill komma till systementor.se används: DNS-uppslag. 

Datorn skickar en förfrågan till DNS-servern, även kallad Domain Name System som översätter sökningen 
"systementor.se" till en publik IP-adress, som sedan returneras till datorn. 

**2. Destination och Gateway**

Nu har datorn fått IP-adressen till målet, dock ligger IP-adressen utanför nätverket. För att kunna ta oss till det andra subnätet behövs det att data skickas genom 
Standard Gateway (routern).

Om datorn inte har MAC-adressen till routern  används ARP (Adress Resolution Protocol), den hjälper datorn att hitta MAC-adressen som tillhör routerns IP-adress.

**3. Inkapslingen (TCP/IP-modellen)**

Nu byggs datapaketet ihop (uppifrån och ner) på klienten. 

- **Applikations lagret** genererar datan - en förfrågan om att besöka systementor.se. 

- **Transport lagret** lägger på en TCP-header med en slumpmässig (52431) source-port och en destination-port (443 för https). 

*Applikations och Transport lagret skapar ett "segment".*

- **Nätverks lagret** lägger på en IP-header med datorns lokala IP som source och "systementor.se" publika IP som destination. 

*Segmentet och IP-header skapar ett "paket"*

- **Länk lagret** kapslar in paketet i en "frame" där den lägger på sin egen MAC-adress som source och routerns MAC-adress som destination. 

- **Fysiska lagret** omvandlar frame:n till elektriska signaler eller radiovågar (bits) och skickas genom kabeln eller luften. (*Den lila kopplingen symboliserar elektricitet genom kabel för att överföra bits.*)

**4. Lokal överföring**\
**4a. Switchen**\
Switchen tar emot signalerna och läser destinationens MAC-adress och skickar vidare den till rätt port som leder till routern. 

**4b. Routern**\
Routern tar emot den och dekapslar frame-header och trailer för att visa paketet. Sedan läser den av destinationens (systementor.se) IP-adress i IP-header, för att veta vart den ska. 

Routern byter ut datorns privata IP-adress till routerns publika IP-adress, via Network Adress Translation (NAT). Routern packar sedan in paketet i en ny frame (med nya MAC-adresser) justerad till nästa nätverk och skickar det vidare till internetleverantören (ISP).

**5. Transport över Internet**\
Men innan den har nått destinationen så har den hoppat mellan ett flertal routrar över internet (BGP-protokollet). 

Till sist när paketet når destinationen passerar den brandväggar och en Load Balancer som dirigerar trafiken rätt. Servern tar emot paketet, dekapslar paketet och hanterar TCP-handskakningen och förbereder ett svar.

Svaret skickas tillbaka på samma sätt, den omvända vägen.


## Moment B: Jämförande OS- och Behörighetsanalys
- Beskrivning av företagscenariot och syftet med behörigheterna osv. 

### Linux
- Dokumentation av kommandon (groupadd, chown, chmod, setgid), samt resultat.

```
```

### Windows
- Dokumentation av kommandon (net ..., icacls), samt resultat. 

```
```

### Test av kommandon
- bob lyckas i "Gemensamt" men misslyckas i "Ledning"

```
```

### Analys
*Jämförelsetabell:*


| Linux | Windows |
|----------|----------|
| Enkel modell | Mer detaljerade inställningar för specifika användare/grupper. |
| Tre nivåer: User, Group, Others. Tre rättigheter: Read, Write, Execute | Flexibel. Ingen strikt indelning. | 

### Arv
Windows (NTFS): använder arv som standard. När man skapar en fil så får filen automatiskt samma rättigheter som mappen den ligger i. Man kan ändra rättigheterna eller ta bort arvet. 

Linux (POSIX): Använder inte automatiskt arv, utan "standard-rättigheter". Behörigheter sätts efter systemets standardmask - umask. Man kan ändra detta genom inställningen Set Group ID (SGID). 

### Slutsats 
**Linux** är mer förutsägbara och enkla i sin administration. User, Group och Others-strukturen gör det enkelt att se helheten och vem som har tillgång till vad. Dock blir det standardiserade arvet "osynligt", vilket gör det svårt att undvika misstag. Linux är stabil och lätt att använda men kräver mer manuell konfiguration med mer avancerade behörigheter. 

**Windows** är mer flexibla och erbjuder att man ska kunna skräddarsy detaljerade listor med behörigheter. Det automatiska arvet gör det enklare för stora organisationer att konfigurera. Flexibiliteten kan dock göra det mer utmanande med säkerheten med "labyrinter" och överlappande arv. 

## Moment C: Spårbarhet & Överlämningsdokumentation
INNAN INLÄMNING - "Kan en extern tekniker ta över och återställa miljön enbart utifrån detta dokument utan att behöva ställa frågor?"  
