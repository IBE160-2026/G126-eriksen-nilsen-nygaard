# Tilbakemelding på product brief

| | |
|---|---|
| **Gruppe** | G126 – G126-eriksen-nilsen-nygaard |
| **Product brief** | `product-brief.md` (commit de5f4e4), lest sammen med `addendum.md` |
| **Tilbakemelding fra** | Faglærer i IBE160 (utarbeidet med KI-støtte) |
| **Dato** | 2026-10-06 |

## Samlet vurdering

- **Bør revideres før dere går videre.** Rett punktene markert «Endre» før dere lager PRD og arkitektur.

**Det som er bra:**

1. Briefen er usedvanlig godt skrevet, med en svært konkret primærbruker (den «pop-finans»-informerte investoren som har lest *The Psychology of Money*, men mangler verktøyene) og et tydelig problem. Ideen om at uenigheten mellom agentene *er* produktet, og at brukeren skal skrive sin egen beslutning med «hva må være sant for at dette skal gå bra?», er original og pedagogisk sterk.
2. Dere har tenkt grundig på grenser: ingen anbefalinger, ingen opsjoner eller krypto, ingen betaling eller megler-kobling, og et hardt krav om at ingen tall når brukeren uten kilde. Addendumet besvarer emnets dimensjoner (data inn/ut, beslutningspunkter, sikkerhet, kjøp/salg) på en ryddig måte.

**De viktigste endringene:**

1. V1 er for stor: fire inngangsveier, fem agenter pluss oversetter, kildelenkede tall fra regnskap, overlapp mot fondsbeholdninger, norsk skatte- og kontolag, kontoer med GDPR-krav og beslutningshistorikk. Definer en mye smalere minimal versjon.
2. Markedsdata er den største ukjente: regnskapstall med kildehenvisning, kurshistorikk og fondenes beholdninger krever datakilder som ofte er betalte, begrensede eller krever nøkkel. Briefen sier ikke hvilke kilder dere skal bruke, eller hvordan sensor kan kjøre appen.
3. Flere suksesskriterier kan ikke måles i emnet (100 brukere første måned, 20 % gjenbruk, 60 % registrerte beslutninger). Behold de funksjonelle og tekniske kriteriene, og gjør dem konkrete nok til å bli tester.

## Vanskelighetsgrad og gjennomførbarhet

### Vurdert vanskelighetsgrad

- **Vanskelig**

**Sammenlignbart med:** 5) KI-styrt sensurering av eksamensoppgaver (vanskelig) – flere KI-vurderinger som skal være faglig forsvarlige, strenge krav til korrekthet (ingen tall uten kilde), og personopplysninger som må beskyttes. I tillegg kommer integrasjon mot markedsdata.

**Begrunnelse:**

| Faktor | Nivå (lav / middels / høy) | Kommentar |
|---|---|---|
| Domenelogikk – hvor mange og hvor kompliserte regler og beregninger må stemme? | Høy | Overlapp og konsentrasjon på tvers av fond og enkeltaksjer, norske skatteregler (ASK, fondskonto, skjermingsfradrag) og verdsettelsesbegreper. Feil her gir brukeren feil grunnlag for en reell beslutning. |
| Datamodell – antall entiteter og relasjoner mellom dem | Middels | Bruker, beholdning, instrument, fondsbeholdninger, analyse, agentinnlegg, kilde og beslutning. |
| Brukere, roller og innlogging | Middels | Én rolle, men konto er påkrevd, med radnivå-isolasjon, kryptering, eksport og sletting. |
| KI-funksjonalitet i appen, f.eks. kall til språkmodell, prompts i koden og håndtering av usikre svar | Høy | Orkestrering av fem agenter og en oversetter, oppløsning av fri tekst til ett instrument, kildekontroll av hvert tall og konsekvent avvisning av «bør jeg kjøpe?». |
| Integrasjoner og eksterne tjenester, f.eks. API-er, betaling og e-post | Høy | Markedsdata (regnskap, kurser, fondsbeholdninger) og språkmodell-API. Begge koster eller er begrenset. |
| Sanntid, samtidighet eller flere brukere som påvirker hverandre | Middels | Ingen sanntidskurser, men analysen skal fullføres innen 90 sekunder med flere agentkall i rekkefølge eller parallelt. |
| Filhåndtering, f.eks. opplasting, PDF-lesing og eksport | Middels | Regnskapstall skal kunne spores til rapporten de kommer fra, og brukerdata skal kunne eksporteres. |
| Sikkerhet og personvern | Høy | Personlige finansopplysninger under GDPR, EU-hosting og kryptering. Godt beskrevet, men krevende å gjennomføre og dokumentere. |

**Hva vanskelighetsgraden betyr for dere:**

- _Vanskelig:_ Et vanskelig prosjekt gir større mulighet for toppkarakter, men også større risiko. Definer en minimal versjon som sikkert kan bli ferdig, og legg resten i tydelige trinn etterpå. For Motvekt betyr det: én inngang (et navn), et lite, fast utvalg instrumenter med lagrede data, tre agenter (analytiker, bull, bear) og en beslutningslogg – før porteføljeagent, skattelag og flere inngangsveier.

### Gjennomførbarhet med BMAD og Claude Code

Dere skal planlegge med BMAD (product brief → PRD → arkitektur → epics og stories) og implementere med Claude Code. Vurderingen under tar hensyn til at det må være tid til hele denne flyten, og til testing, retting og README til slutt.

| Spørsmål | Vurdering (OK / risiko / stor risiko) | Kommentar |
|---|---|---|
| **Tid og omfang** – kan v1 realistisk bli ferdig og stabil i løpet av semesteret, med tid til flere iterasjoner? | Stor risiko | Hvert av områdene (agentrådet, kildekontroll, porteføljeoverlapp, skattelag, kontoer med GDPR) er et betydelig arbeid. Alle samtidig er neppe realistisk med BMAD-flyten i tillegg. |
| **BMAD-flyten** – er briefen konkret nok til at PRD, arkitektur og stories kan lages uten store hull, og blir det overkommelig mange stories? | Risiko | Produktet er svært godt beskrevet, men datakildene og agentenes nøyaktige oppgaver (inn- og utdata) mangler. Antallet stories blir høyt med dagens scope. |
| **Egnet for Claude Code** – bruker løsningen en vanlig, godt dokumentert teknologistakk som Claude Code håndterer godt, eller krever den nisjeteknologi, spesialmaskinvare eller mye manuell konfigurasjon? | Risiko | Webapp og LLM-kall er greit. Agentorkestrering og integrasjon mot markedsdata-API-er er mer krevende og krever mye prøving og feiling. |
| **Kontroll på KI-ens arbeid** – kan gruppen selv avgjøre om koden gjør det riktige? Krever domenet kunnskap gruppen ikke har, f.eks. avanserte beregninger eller fagregler, så er det vanskelig å kvalitetssikre. | Risiko | Dere har god finansfaglig kunnskap, og det er en styrke. Likevel må dere kunne avgjøre om analytikerens tall stemmer med kilden, om overlappberegningen er riktig og om skattereglene er korrekt anvendt i koden, for hver analyse. Lag faste eksempler med fasit, og vurder å gjøre skatte- og overlappdelen regelstyrt i stedet for KI-styrt. |
| **Testbarhet** – finnes det tydelige regler og forventede resultater som tester kan skrives mot? | Risiko | «Ingen tall uten kilde» og overlappberegning kan testes godt. Agentenes argumenter er vanskeligere; test struktur og avvisningsregler med faste testspørsmål og mock-svar. |
| **Kjørbar for sensor** – kan appen kjøres lokalt etter README, uten gruppens nøkler, betalte kontoer eller egen infrastruktur? | Stor risiko | Krever språkmodell-nøkkel, markedsdata-nøkkel og EU-hosting slik det er beskrevet. Sensor må kunne kjøre lokalt med lagrede data og mock-svar. |
| **Avhengigheter og kostnader** – krever løsningen betalte API-er, f.eks. språkmodeller, og finnes det en plan for kostnad, testmodus eller mock-data? | Stor risiko | Seks agentkall per analyse og et revisjonskrav på 100 analyser gir merkbar kostnad. Ingen plan for modell, datakilde, kostnad eller mock er beskrevet. |

**Konklusjon om gjennomførbarhet:**

- **Lite realistisk uten vesentlige endringer.** Se forslagene under.

**Forslag til justering av omfang eller vanskelighetsgrad:**

1. Avgrens til et fast utvalg på f.eks. 10–20 aksjer og fond med data lagret i repoet (nøkkeltall med kilde, fondsbeholdninger). Det fjerner avhengigheten av markedsdata-API, gjør kildekontrollen testbar og lar sensor kjøre appen.
2. V1: én inngang (brukeren skriver et navn fra utvalget), tre agenter (analytiker, bull, bear) med oversetter-tekst, og beslutningslogg. Legg porteføljeagent og overlapp i trinn 2, og skattelaget i trinn 3. Flytt «lim inn et innlegg», sammenligning og hold/selg til visjonen.
3. Gjør skatte- og kontodelen som regelstyrt kode med faste regler fra Skatteetaten, ikke som en KI-agent. Da kan dere teste den mot fasit. Vurder også om kontoer kan erstattes av lokal lagring i v1, slik at GDPR-kravene blir enklere.

## Hvorfor product brief er viktig for mappen

Product brief er utgangspunktet for PRD, arkitektur, stories og til slutt koden. Del 1 av mappen vurderes blant annet på om sensor kan følge en sporbar vei fra plan til ferdig app. Den vurderes også på om appen gjør det dere har beskrevet, om den er testet, om den er godt designet, og om den kan kjøres etter README. Et uklart, for stort eller for lite brief gjør alt dette vanskeligere senere. Det er mye enklere å rette nå enn sent i semesteret.

## 1. Gjennomgang av briefens deler

| Del av brief | Status | Kommentar |
|---|---|---|
| Executive Summary – er det klart hva appen er, og hvilket problem den løser? | OK | Svært klart og godt formulert: et «råd» av KI-agenter som diskuterer et aksjetips, uten å gi anbefaling. |
| The Problem – er problemet konkret, med reelle situasjoner og brukere? | OK | Konkret og overbevisende, med eksempler som indeksfond som allerede gjør brukeren til Nvidia-aksjonær. |
| The Solution – beskriver løsningen brukeropplevelsen, ikke bare teknologi? | Juster | Beskriver opplevelsen godt. Det mangler likevel hva hver agent konkret får som input og leverer som output, og hvor tallene kommer fra. |
| What Makes This Different – er vurderingen ærlig og realistisk? | OK | Ærlig om at agentorkestrering ikke er en vollgrav. Påstanden om at produktet ikke krever konsesjon fra Finanstilsynet bør formuleres som en vurdering dere har gjort, ikke som et faktum. |
| Who This Serves – er primærbrukerne tydelige, og vet vi hva de trenger? | OK | En av de tydeligste primærbrukerne man kan få, med klar avgrensning mot aktive tradere og profesjonelle. |
| Success Criteria – kan kriteriene faktisk sjekkes eller testes? | Endre | De funksjonelle og tekniske kriteriene er gode utgangspunkt. Brukerutfall og forretningsmål (100 brukere, 20 % gjenbruk) kan ikke måles i emnet. Gjør de tekniske konkrete, f.eks. «for 20 faste testanalyser har hvert tall en kilde som stemmer», «spørsmålet ‘bør jeg kjøpe?’ avvises i alle testvarianter», «overlapp for testportefølje A beregnes til X %». |
| Scope – er det klart hva som er med i første versjon, og hva som ikke er det? | Endre | Svært tydelig «Explicitly out», men «In» er alt for stort. Del i v1 og senere trinn, og legg datakilder og demomodus inn i scope. |
| Vision – henger visjonen sammen med resten uten å blåse opp omfanget? | OK | Ambisiøs, men tydelig adskilt fra v1. |

## 2. Utgangspunkt for del 1 av mappen

Punktene følger kriteriene i sensorveiledningen for del 1. Vektene i parentes viser hvor mye hvert kriterium teller i del 1.

| Kriterium i del 1 | Hva briefen bør legge til rette for | Status | Kommentar |
|---|---|---|---|
| **1. Prosess og KI-styring** (30 %) | Brief som er presis nok til at PRD og stories kan bygges direkte på den, slik at krav kan spores fra brief til kode. | Juster | Godt grunnlag på produktnivå. Lagre agentenes prompts i repoet og dokumenter hvordan dere justerer dem; det blir et sentralt spor av KI-styring i dette prosjektet. |
| **2. Funksjonalitet og omfang** (20 %) | Realistisk omfang for gruppen og semesteret: en tydelig kjerneflyt som kan bli ferdig og stabil, og nok innhold til å vise reell funksjonalitet. | Endre | Omfanget er for stort. En smal v1 med agentrådet og beslutningsloggen gir fortsatt et vanskelig og interessant prosjekt. |
| **3. Kvalitetssikring og testing** (15 %) | Suksesskriterier og funksjoner som er konkrete nok til å bli testtilfeller. | Endre | Lag faste testanalyser med fasit for tall og kilder, og testspørsmål for avvisningsreglene. |
| **4. Design og brukeropplevelse** (10 %) | Tydelige brukere og brukssituasjoner som designet kan bygges rundt, gjerne med de viktigste skjermbildene eller flytene skissert. | OK | Tydelig bruker og situasjon (leser noe på mobilen og vil vurdere det). Skisser hvordan uenigheten mellom agentene vises, og hvordan beslutningen registreres. |
| **5. Kodekvalitet og arkitektur** (10 %) | Teknologivalg som er begrunnet og ikke mer komplekse enn appen trenger. | Juster | Skillet mellom grensesnitt og orkestreringstjeneste er fornuftig. Unngå at arkitekturen blir mer kompleks enn nødvendig, f.eks. med egne tjenester per agent. |
| **6. README og kjørbarhet** (10 %) | Løsning som andre kan kjøre lokalt uten betalte kontoer, og uten tilgang til gruppens egne tjenester og nøkler. | Endre | Planlegg lokal kjøring med lagrede markedsdata, `.env.example`, testbruker og mock-modus for agentene. |
| **7. Ryddighet i repoet** (5 %) | En plan for hvor hemmeligheter, testdata og dokumentasjon skal ligge. | Juster | Nøkler i `.env`, testdata (instrumenter, fiktive porteføljer) i egen mappe. Briefen og addendumet ligger i roten og kan flyttes til en mappe for planleggingsdokumenter. |

## 3. Neste steg for gruppen

1. Bestem datakilder, og vurder å bruke et fast utvalg instrumenter med lagrede data i v1.
2. Del Scope i v1 (én inngang, tre agenter, beslutningslogg) og senere trinn (portefølje, skatt, flere inngangsveier).
3. Beskriv hver agents input og output, og gjør skattedelen regelstyrt.
4. Skriv om suksesskriteriene til testbare kriterier, og gå deretter videre til PRD.

Oppdater product brief i repoet når dere har gjort endringene, slik at historikken viser hvordan planen utviklet seg. Det er en del av prosessen sensor ser etter.
