<<<<<<< HEAD
# Individuell fördjupning - VG-uppgift

Kurs: Introduktion till yrkesrollen och grunderna i IT-infrastruktur (MYH 2025/4008)
Examinationsform: Individuell teknisk fördjupningsuppgift (Summativ examination)
Av: Blossom Davis
Datum: 2026-10-02

## Moment A: Avancerad Nätverksanalys &amp; Trafikflöden
Illustration av datatrafikflöde:
![text](länk)


### Vad händer - steg för steg
1. a
2. b
3. c
4. d
5. e

Tydliggör pakethuvuden, MAC-adresser, IP-adresser, Postnummer

## Moment B: Jämförande OS- och Behörighetsanalys
- Sätta upp en identisk behörighetsstruktur i både Linux och Windows samt göra en djupgående jämförelse.
- Dokumentera och analysera 


## Moment C: Spårbarhet &amp; Överlämningsdokumentation
Färdigställa en komplett system- och driftdokumentation för hela labbmiljön.

Innehåll i dokumentationen:

Nätverkskarta/topologi och IP-plan.

Systemarkitektur och installerade tjänster.

Instruktioner för återställning/backup (step-by-step).

Länkar till konfigurationsskript i Git-repositoryt.


INNAN INLÄMNING: "Kan en extern tekniker ta över och återställa miljön enbart utifrån detta dokument utan att behöva ställa frågor?"
=======
# Individuell-f-rdjupning---VG-uppgift

LILA: elektricitet genom kabel för att överföra bits

1. Klienten "Labb-miljö" vill nå hemsidan "Systementor.se". För att datorn ska veta att vi vill komma till systementor.se används: DNS-uppslag. 

Datorn skickar en förfrågan till DNS-servern, även kallad Domain Name System som översätter sökningen 
"systementor.se" till en publik ip-adress, som returneras till datorn. 

2. Nu har datorn fått ip-adressen till målet, dock ligger ip-adressen utanför nätverket. De är i olika LAN-nätverk ihopkopplade med olika routrar. För att nå hemsidan behöver meddelandet resa genom WAN genom routern. För att kunna ta oss ut på nätet behövs det att data skickas genom 
Standard Gateway (även kallad router). 


SWITCHEN läser destinationens mac-adress och skickar vidare den till routern. 


Routern decapsulate frame:ns header och trailer för att visa packet. den läser sedan av destinationen "systementor.se". Och sedan placerar den i en ny frame till nästa LAN. 


För att skicka datapacket mellan olika subnät används ARP (adress resolution protocol), 
den hjälper datorn att hitta MAC-adressen (Hårdvaruadressen) som tillhör routerns ip-adress. 

Nu kommer vi till enkapsuleringen (TCP/IP-modellen). Datorn har nu sänt iväg en förfrågan att besöka systementor.se. 

Applikations lagret genererar datan och ett datapaket (http/https) sätts ihop av datorn. 

För att kunna skicka iväg den genererade datan behöver datorn en transport väg. Transport lagret (TCP/UDP) lägger på en TCP-header med källport (en random?) och en mål port (443). 

Applikations och Transport lagret skapar ett "segment". 

Sedan kommer nätverkslagret (IP), här läggs det på en IP-header med källa och mål. IP:adresserna skapar då ett packet. 


Data-link lager (Ethernet/Wi-Fi) denna del kapslar in allt i en frame med datorns MAC-adress
som källa och routerns MAC-adress om mål. 

Routing/NAT
När paketet når den lokala routern så byter routern ut källans ip-adress mot den publika ip-adressen (och sparar kopplingen). Routern skickar paketet vidare till internetleverantörens (ISP) router.

Men innan den har nått slutdestinationen så har den hoppat mellan ett flertal routrar över internet (BGP-protokollet). 

Paketet når destinationen där de passerar brandväggar och (Load Balancer) som dirigerar trafiken rätt.Målservern tar emot paketet, dekapslar paketet och hanterar tcp-handskakningen och förbereder ett svar.

Svaret skickas tillbaka den omvända vägen. 
>>>>>>> c4f8795 (började beskriva datatrafikflöde)
