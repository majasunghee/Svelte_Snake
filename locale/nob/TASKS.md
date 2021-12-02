# Lær Svelte ved å lage Snake

> Les på det språket du foretrekker:
>
> - [🇬🇧 English][tasks-eng]
> - [🇳🇴 Norsk bokmål][tasks-nob]

Et kurs av [Eirik Vågeskar](https://github.com/vages), med hjelp fra [Johannes Moskvil](https://github.com/johannbm), [Brede Kristensen](https://github.com/BredeYabo/), [Marcus Goplen](https://github.com/Goplen/), [Arve Seljebu](https://github.com/arve0/) og flere kolleger i [Knowit Objectnet](https://www.knowit.no/kontakt/selskap/knowit-objectnet-as/).

## Intro: Vi skal lage spillet Snake i Svelte

![Et kvadratisk rutet brett som inneholder en grønn slange og et rødt eple.
Overfor brettet ser man at poengsummen er 0.][gameplay-png]

### Svelte

[Svelte](https://svelte.dev) er et bittelite webrammeverk. Hjemmesiden presenterer det som følger:

> Svelte er en radikal ny tilnærming til å lage brukergrensesnitt. Mens tradisjonelle rammeverk som React og Vue gjør storparten av arbeidet sitt i nettleseren, flytter Svelte det til et kompileringssteg som finner sted når man bygger en app.
>
> I stedet for å bruke teknikker som virtuell-dom-sammenligning, skriver Svelte kode som oppdaterer domen med kirurgisk presisjon når tilstanden i appen endrer seg.
>
> Vi er stolte over at Svelte nylig ble stemt frem som det [best likte rammeverket](https://insights.stackoverflow.com/survey/2021#section-most-loved-dreaded-and-wanted-web-frameworks) med [de mest fornøyde utviklerne](https://2020.stateofjs.com/en-US/technologies/front-end-frameworks/) i to store undersøkelser blant programvareutviklere. Vi tror du også vil like det svært godt. Les [bloggposten som introduserte Svelte versjon 3](https://svelte.dev/blog/svelte-3-rethinking-reactivity) for å lære mer.

#### Fordelene med Svelte

Applikasjonene man skriver i Svelte blir som regel [mindre og raskere enn en tilsvarende applikasjon er i React eller Vue](https://www.freecodecamp.org/news/a-realworld-comparison-of-front-end-frameworks-with-benchmarks-2019-update-4be0d3c78075/).

![Faksimile fra
https://www.freecodecamp.org/news/a-realworld-comparison-of-front-end-frameworks-with-benchmarks-2019-update-4be0d3c78075/
som sammenligner overføringsstørrelse for Svelte og flere andre
rammeverk][transfer-size-png]

![Faksimile fra
https://www.freecodecamp.org/news/a-realworld-comparison-of-front-end-frameworks-with-benchmarks-2019-update-4be0d3c78075/
som sammenligner kildekodelinjer for Svelte og flere andre
rammeverk][source-code-size-png]

### Du må ha følgende på datamaskinen din

- [node](https://nodejs.org/en/)
- En tekstbehandler, fortrinnsvis [en der man kan installere støtte for Svelte](https://github.com/sveltejs/integrations#editor-extensions).
- En klone av [Vages/svelte-snake-workshop](https://github.com/Vages/svelte-snake-workshop)

Hvis du trenger hjelp til å installere ting, kan du sjekke [SETUP.md](./SETUP.md).

### Hvordan kurset pleier å være

Repoet [Vages/svelte-snake-workshop](https://github.com/Vages/svelte-snake-workshop) inneholder alt du trenger. Du kan bestemme tempo selv. Det er mulig å fullføre kurset helt på egen hånd.

Vi har delt kurset i 6 deler. Hver del inneholder to eller flere oppgaver. Hver oppgave starter med oppgavetekst, som av og til blir fulgt av hint. Du kan la være å lese hintene dersom du trenger en ekstra utfordring. Bytt til `task-X-begin` før du løser hver nye oppgave (eksempelvis `git checkout task-1.2-begin`). `task-X-end` er oppgavens fasit. For å fjerne koden du har lagt til og gå videre til ny oppgave, kan du skrive `git stash` og deretter `git checkout task-X-begin`.

Når vi holder kurset fysisk eller digitalt, pleier kursholderne å gå gjennom oppgaver og spørsmål i fellesskap med ujevne mellomrom. Du kan be om hjelp fra kursholderne når som helst.

Vi har laget så å si all styling på forhånd, slik at man kan bruke mest mulig tid på kode.

## Del 1: Enkel grafikk

Når du er ferdig med denne delen, skal spillet vise hvor slangen og eplet er på brettet.

### Opplæring: Slik ser en Svelte-fil ut

Svelte er en sammensmeltning av HTML, CSS og Javascript med noen forbedringer. I Svelte kan man skrive disse tre språkene i én og samme fil. Delene kalles for «script», «template» og «styling».

```svelte
<!-- script -->
<script>
  let answer = 42;
  let color = "red";
</script>

<!-- template -->
<div style="color: {color}">
  Hello world, the answer is {answer}
</div>

<!-- styling -->
<style>
  div {
    font-weight: bold;
  }
</style>
```

Man bruker krøllparenteser inni _template_ for å sette inn variabler, utregninger og funksjonskall.

```svelte
<script>
  let answer = 42;
</script>

<div>Meningen med livet er {a}.</div>
<div>Kvadratet av meningen er {a * a}</div>
<div>Meningen med livet har {Math.sign(a)} som fortegn</div>
```

Løs [oppgaven fra Svelte-opplæringen om å sette inn data](https://svelte.dev/tutorial/adding-data) før du går videre.

### Oppgave 1.1: Plasser eplet

Åpne filen `src/routes/_game/App.svelte`.

Brettet inneholder en `<div class="apple" />`. Variabelen `apple` inneholder en koordinat. Oppgaven din er å plassere eplet på den ruten på brettet som koordinaten angir.

Brettets X-akse peker mot høyre, og Y-aksen peker nedover. Konstanten `CELL_SIZE` inneholder sidelengden til hver rute.

![X-akse som peker mot høyre, Y-akse som peker ned.][axes-png]

Når du er ferdig, skal det se slik ut:

![Eplet et sted nær midten av brettet][apple-near-middle-of-board-png]

#### Hint: Style-attributtet

For å overstyre og legge til stil på elementer i HTML (ikke bare Svelte), kan man bruke attributtet `style`. Inni style skriver man CSS-utsagn.

```svelte
<div style="font-weight: bold;">Fet skrift</div>
```

#### Hint: left og top i css

Bruk CSS-egenskapene `left` og `top` for å forskyve elementer langs henholdsvis `x`- og `y`-aksene.

```svelte
<div style="top: 20px; left: 10px;">Forskjøvet</div>
```

#### Hint: For å avsløre nesten alt

For å plassere eplet, må du gjøre omtrent som følger:

```svelte
<div class="apple" style="left: {regnestykke1}px; top: {regnestykke2}px;" />
```

Du må benytte deg av `apple.x` og `apple.y` samt `CELL_SIZE` for å få til disse regnestykkene.

### Opplæring: each-blokker

Neste oppgave kommer til å kreve en each-blokk.

Løs denne oppgaven fra Svelte-opplæringen for å lære [hvordan each-blokker fungerer](https://svelte.dev/tutorial/each-blocks).

### Oppgave 1.2: Tegn slangen på skjermen

Oppgaven din er å tegne slangen på brettet.

Slangen er en samling koordinater som ligger i variabelen `snake`. Det første elementet er hodet. Tegn hver koordinat i kroppen som en `<div class="body-part" />`.

Slangen skal se slik ut når du er ferdig:

![Eple og slange plassert på brettet][task-1-2-end-png]

### Oppgave 1.3: Trekk posisjonsutregningen ut i en funksjon

Vi bruker utregningen (`left: {foo.x * CELL_SIZE}px; top: {foo.y * CELL_SIZE}px`) flere ganger i koden. Koden blir lettere å vedlikeholde dersom vi legger denne utregningen ett sted.

Oppgaven din er å flytte den nevnte utregningen over i en funksjon, `calculatePositionAsStyle(coordinate)`, og erstatte alle tilfeller der vi bruker utregningen med et kall til denne funksjonen. Funksjonen skal ta inn en koordinat og gi tilbake en streng med verdier for top og left.

## Del 2: Spillkontroller

Når du er ferdig med denne delen, skal det gå an å styre slangen med piltastene.

### Opplæring: Å lytte etter input

Løs følgende oppgaver fra Svelte-opplæringen før du går videre:

- [Lytte etter DOM-hendelser på et element](https://svelte.dev/tutorial/dom-events)
- [Lytte etter DOM-hendelser på selve vinduet](https://svelte.dev/tutorial/svelte-window)

### Oppgave 2.1: Lytt til trykk på tastaturet

Oppgaven din er å lytte etter trykk på tastaturet og sende dem videre til funksjonen `console.log`. Applikasjonen skal kunne «høre» tastetrykk uansett hvilken del av nettsiden som har fokus, slik at brukeren ikke skal måtte trykke på et spesifikt element på siden for at spillet skal registrere tastetrykkene.

Unngå å lytte på tastetrykk fra hele vinduet (`svelte:window` viser til vinduet i sin helhet). Legg heller til en lytter på det Svelte-spesifikke elementet som viser til `document.body`.

#### Hint: Tastetrykk-hendelsen

Tastetrykk-hendelsen heter `keydown`. I Svelte lytter man etter den med `on:keydown`.

#### Hint: svelte:body

Man lytter til `document.body` ved å bruke elementet `<svelte:body />`. Man kan lytte etter hendelser på det som med et hvilket som helst HTML-element.

### Opplæring: Å endre variabelverdier

Du kommer til å måtte vite hvordan du endrer variabler i den kommende seksjonen. Gjør følgende oppgaver fra Svelte-opplæringen før du fortsetter:

- [Oppdatere vanlige variabler](https://svelte.dev/tutorial/reactive-assignments)
- [Oppdatere arrays og objekter](https://svelte.dev/tutorial/updating-arrays-and-objects)

### Oppgave 2.2: Beveg slangen ett steg i samme retning som et tastetrykk

Oppgaven din er å oversette tastetrykk til bevegelse. Slangen skal bevege seg ett steg i oppgitt retning hver gang man trykker på en piltast. Unngå at slangen beveger seg når man trykker på andre taster.

For å gjøre dette lettere, har vi laget en funksjon `convertKeyboardKeyToDirection` i `utils.js`, som oversetter fra tastetrykk til en retning. Vi bruker himmelretningene for å vise til retningene på brettet: Vest er venstre, nord er opp.

Inntil videre skal slangen bevege seg også om den treffer seg selv eller en vegg. Game over kommer i en senere oppgave.

#### Hint: Viktige Array-funksjoner

- Den enkleste måten å legge til elementer i starten eller slutten i et array, er å bruke spredning (_spreading_): `[a, ...b]`. (Svelte reagerer ikke på push og pop; dette kommer vi tilbake til senere.)
- Funksjonen [Array.prototype.slice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) er nyttig når man vil fjerne elementer fra starten og slutten av et array.

#### Hint: Hjelpemidler i `utils.js`

I `utils.js` finner man:

- `add(coordinateA, coordinateB)`, for å legge sammen to vektorer/koordinater.
- `DIRECTION_TO_VECTOR`, for å gå fra himmelretning til retningsvektor.

Legg til linjen `import { DIRECTION_TO_VECTOR, add } from './utils'` øverst i `<script>` for å bruke dem.

## Del 3: Logikk

Når du er ferdig med denne delen, skal spilleren få poeng når slangen spiser et eple. Spillet skal stoppe hvis slangen er på en ulovlig posisjon. Og spillklokka skal tikke, slik at slangen beveger seg på jevnlige tidspunkter, heller enn når man trykker på piltastene.

### Opplæring: Dollartegnet i Svelte – reaktive utsagn.

I regneark, som Microsoft Excel, kan man skrive formler i cellene, for eksempel `=A1*B3`. Da havner resultatet av regnestykket i cellen, og resultatet oppdaterer seg automatisk når man endrer innholdet i cellene som regnestykket avhenger av. Slik er det vanligvis ikke i programmering: Man kan ikke si `a = 2; b = a * 2; a = 8` og regne med at `b` nå er 16 i stedet for 4 fordi det dobbelte av 8 er 16. Men du kan få det til i Svelte.

I Svelte kan vi få datamaskinen til å kjøre et _utsagn_ (statement) på nytt som reaksjon på endringer. Dette gjør vi ved å sette et dollartegn foran utsagnet. Utsagn som starter med et slikt dollartegn kalles for et _reaktivt utsagn_, fordi utsagnet kjøres på nytt som en reaksjon på noe annet.

Hvis utsagnet inneholder en tilegning til en variabel, kan Svelte holde verdien oppdatert for oss.

```svelte
<script>
  let b = 3;
  let c = 4;

  $: a = (b * c) / 2; // a === 6
  b = 6;
</script>

<div>
  <!-- 
    Uten `$: …` hadde a hatt verdien 6, 
    men den får automatisk verdien 12 etter 
    at man har gitt b en ny verdi. 
  -->
  Trekantens grunnlinje er {b}, og høyden er {c}. Arealet er {a}.
</div>
```

Løs [oppgaven om reaktive utsagn fra Svelte-opplæringen](https://svelte.dev/tutorial/reactive-statements) før du går videre.

Nesten et hvilket som helst utsagn kan stå etter dollartegnet, ikke bare utregninger. Man kan også skrive funksjonskall og if-setninger:

```svelte
<script>
  let lastUserInput = "";
  $: if (lastUserInput === "hello") {
    console.log("hello to you too"); // Svarer når brukeren skriver inn strengen hello
  }
</script>

<label>Skriv noe: <input bind:value={lastUserInput} /></label>
```

```svelte
<script>
  let lastUserInput = "";
  $: parrotOutput = parrot(lastUserInput); // Gjentar alt brukeren sier, fulgt av papegøyelyd

  function parrot(something) {
    return something + ", sqawk!";
  }
</script>

<label>Si noe: <input bind:value={lastUserInput} /></label>
<div>
  Papegøyen sier: {parrotOutput}
</div>
```

Et reaktivt utsagn kjøres én gang når appen lastes inn. Svelte kjører utsagnet på nytt hver gang en variabel som brukes inni utsagnet får en ny verdi. Svelte finner automatisk ut hvilke verdier et reaktivt utsagn avhenger av. Man trenger ikke oppgi avhengighetene selv, slik som med for eksempel `React.useEffect`.

Merk: Svelte merker bare endringer som kommer som følge av man bruker tilegnelsesoperatoren, `=` (for eksempel `foo.bar = "baz"`), og ikke som følge av metodekall (som `.push` og `.pop`). Se [opplæringsoppgaven om reaktivitet med objekter og arrays](https://svelte.dev/tutorial/updating-arrays-and-objects) for en dypere forklaring.

Når man skriver spill-logikk, kan man ofte oversette regler nesten direkte til reaktive utsagn: «Hvis `x === foo`, så gjør a, b og c» blir til `$: if (x === foo) { a(); b(); c(); }`.

### Oppgave 3.1: Gi poeng når slangen spiser eplet

Oppgaven din er å skrive et reaktivt utsagn med en if-setning slik at når slangehodet er på samme koordinat som eplet, øker antallet poeng med 1.

Lag en variabel `score`. Dette er antallet epler slangen har spist.

Når du har poeng-økningen til å virke, kan du sørge for at eplet får en ny, tilfeldig plassering på brettet idet slangen spiser det.

Merk: I denne oppgaven sparer du mye arbeid ved å bruke hjelpefunksjoner fra `utils.js`.

#### Hint: Hjelp i utils.js

I `utils.js` finner man funksjonen `isEqual` som sier om to koordinater er like, og funksjonen `pickRandomOpenSpace`, som trekker en passelig plassering for det nye eplet.

### Oppgave 3.2: Få slangen til å vokse når den spiser eplet

Oppgaven din er å få slangen til å vokse etter at den har spist et eple.

For å gjøre det lettere for deg, har vi trukket ut logikken for å regne ut neste slange som funksjonen `getNextSnake(snake, direction, ?shouldGrow)`. `shouldGrow` er et valgfritt tredje argument, og er en boolsk.

### Opplæring: Svelte-komponenters livssyklus, pluss setInterval

For å løse den kommende oppgaven, kommer du til å måtte kunne det du lærer av følgende oppgaver i Svelte-opplæringen:

- [Oppgaven om `onMount`](https://svelte.dev/tutorial/onmount)
- [Oppgaven om `onDestroy`](https://svelte.dev/tutorial/ondestroy) (som inneholder litt om `setInterval`)

### Oppgave 3.3: Få spillet til å tikke

Oppgaven din er å få slangen til bevege seg ved faste tidsintervaller i stedet for idet man trykker på piltaster. Når tiden for å bevege seg er inne, skal slangen bevege seg i den retningen som spilleren sist oppga. I demoversjonen av spillet er tidsintervallet 100 ms, men du kan endre dette om du vil.

### Oppgave 3.4 Stopp tikking når slangen dør

Når slangen treffer seg selv eller en vegg, er det _game over_.

Oppgaven din er å innføre _game over_ ved å stoppe spillklokka dersom en av de nevnte tilstandene inntreffer. Spillet skal stoppe som en _reaksjon_ på at slangen har beveget seg, og ikke som en del av `moveSnake`.

For å stoppe tikkingen, har vi trukket ut en funksjon `stopTicking` som du kan bruke.

#### Hint: Hjelpefunksjoner

I `utils.js` finner man de nyttige funksjonene `isInsideBoard` og `isSnakeEatingItself`.

#### Hint: Reaktivitet

Husk reaktivitet og if-setninger, `$: if (x) { … }`, og hvordan man nesten ordrett kan oversette spill-logikk til slike.

Hvis vi skulle formulert reglene for game over muntlig, hadde vi sagt noe slikt som:

- «Hvis slangehodet er utenfor brettet eller inni slangen selv, er det game over»
- «Hvis spillet er slutt, stopper tikkingen.»

### Oppgave 3.5: Bare reager på vinkelrette tastetrykk

Idet du har fått game over til å virke, kommer du kanskje til å oppdage et problem: Slangen dør når man trykker tasten som går i motsatt retning av der slangen beveger seg for øyeblikket, fordi den spiser sin egen hals. Dette kan også skje når man er litt rask idet man prøver å ta en U-sving. I denne og den neste oppgaven skal vi prøve å unngå dette.

Oppgaven din er å sørge for at slangen kun reagerer på tastetrykk som er vinkelrette på slangens nåværende retning. Hvis slangen går nordover, skal spillet bare registrere tastetrykk på venstre og høyre piltast. Som med mange andre oppgaver, finnes det en funksjon som kan hjelpe deg i `utils.js`.

### Oppgave 3.6: Bruk en kø til å holde styr på fremtidige bevegelser

**Dette er en utfordringsoppgave som har mer å gjøre med programmering enn Svelte i seg selv. Du kan hoppe til neste oppgave hvis du ønsker.**

I løsningen på oppgave 3.5 som man finner i `task-3.5-end`, kan man fortsatt fremprovosere at slangen spiser seg selv hvis man er rask: Hvis slangen for eksempel beveger seg nordover og spilleren raskt trykker ⬅️ fulgt av ⬇️, ender spillet opp med å registrere ⬇️ som neste bevegelse.

Vi kan unngå problemet ved å bruke en _kø_ til å ta vare på retningene som slangen skal bevege seg i. Når slangen skal bevege seg, henter vi neste planlagte retning og beveger slangen i den. Dette gjør det mulig å trykke inn avanserte bevegelser raskt uten å tenke på timing.

Vi har laget variabelen `headDirectionQueue`, et array som holder styr på retningene brukeren har planlagt at slangen skal bevege seg i. I stedet for å legge neste planlagte retning rett i `headDirection`, skal du legge retningen sist i `headDirectionQueue`. Når tiden for at slangen skal bevege seg er inne, skal programmet bruke _den første vinkelrette retningen_ i køen som ny verdi for `headDirection`. Med andre ord: Fjern alle ikke-vinkelrette bevegelser fra starten av køen frem til du finner en vinkelrett bevegelse. Bruk denne som neste `headDirection` og la påfølgende bevegelser bli liggende i køen som de er.

Gjør de endringene som trengs i `moveSnake` og `handleKeydown`.

## Del 4: Animasjon

Når du er ferdig med denne delen, skal spillet ha en animert slange, hodeskalle og epler.

### Opplæring: Kontroll-blokker

- [if-blokker](https://svelte.dev/tutorial/if-blocks)
- [else-blokker](https://svelte.dev/tutorial/else-blocks)
- [key-blokker](https://svelte.dev/tutorial/key-blocks)

### Opplæring: Hvordan overganger fungerer

I Svelte følger modulen `svelte/transition` med. Den gjør at man kan animere et element som dukker opp i eller forsvinner fra dokumentet.

- [transition-attributtet](https://svelte.dev/tutorial/transition)
- [Hvordan man kan legge parametere på overganger](https://svelte.dev/tutorial/adding-parameters-to-transitions)
- [Forskjellige overganger for inn og ut](https://svelte.dev/tutorial/in-and-out)

### Oppgave 4.1: Animer eplet

Oppgaven din er å få det nye eplet til å sprette opp på plassen sin når slangen spiser det forrige eplet.

For å få til dette skal du importere overgangen `scale` fra `svelte/transition` og legge den på riktig element. For å begrense animasjonen til når eplet dukker opp, skal du bruke `in:` i stedet for `transition:`. (Du kan også prøve [andre overganger](https://svelte.dev/docs#svelte_transition).)

### Hint: Bruk en egnet blokk

Vanligvis pleier Svelte bare å animere elementer når de dukker opp i eller forsvinner fra dokumentet. Man kan fortelle Svelte at elementet skal animeres på nytt når en verdi endrer seg ved å bruke en key-blokk: `{#key <verdi>}<innhold>{/key}`. Da vil Svelte animere `innhold` på nytt når `verdi` endrer seg.

### Oppgave 4.2: Legg på en hodeskalle når slangen dør

I stylingen finnes det en klasse `skull`. Oppgaven din er å få en `<div/>` med klassen `skull` til å dukke opp når slangen dør. Den skal ha samme koordinat som slangehodet.

For å animere hodeskallen, legg på en `transition:scale` med en forsinkelse på 300 ms.

### Oppgave 4.3: Animer slangehodet

I style-blokken finnes det en klasse `head`. Denne sørger for styling og animasjon av slangehodet så lenge man legger den på et element med klassen `body-part`. Oppgaven din er å legge inn et animert slangehode ved hjelp av denne klassen.

Du trenger ikke å bruke noen `transition:…` her. Stylingen tar seg av animasjonen så lenge du legger riktig klasse på rett sted.

### Oppgave 4.4: Animer slangehalen

Oppgaven din er å animere halen. Det finnes en klasse, `tail`, som man kan legge på et element for å få den samme gli-animasjonen som for hodet, men uten å forstørre kroppsdelen.

Legg til en animert hale på slangen.

**Advarsel**: Halen kommer til å blinke litt i alle nettlesere utenom Firefox (deriblant Chrome og Safari) på grunn av en bug i layout-motoren. Du kan regne oppgaven som ferdig når du har en animert hale som blinker av og til. Fasiten inneholder et triks som fjerner blinkingen. Vi kan dessverre ikke fortelle hva trikset er, fordi det ville avslørt løsningen på hovedoppgaven.

## Del 5: Komponenter og nettverk

Når du er ferdig med denne delen, skal spillet ha en game-over-skjerm med toppliste hentet fra en tjener. På skjermen skal man også kunne registrere navnet sitt og sende det til tjeneren sammen med siste poengsum.

### Opplæring: Komponenter

Gjør følgende oppgaver fra Svelte-opplæringen:

- [Nøstede komponenter](https://svelte.dev/tutorial/nested-components)
- [Å erklære props](https://svelte.dev/tutorial/declaring-props)

### Oppgave 5.1: Lag en komponent som dukker opp ved spillslutt

Filen `GameOver.svelte` ligger klar i samme mappe som `App.svelte`. Oppgaven din er å sørge for at komponenten vises på skjermen når spillet er over og at den viser poengsummen som spilleren fikk.

Det er litt knotete å få komponenten til å vises på skjermen på en elegant måte. Derfor har vi lagt inn noen div-er nederst i template-delen av `App.svelte` der man kan montere `<GameOver>`-komponenten.

### Advarsel: Resten av del 5 er vanskelig

Resten av oppgavene i del 5 er for folk som har erfaring med nettverkskall, løfter (_promises_) og lignende i Javascript. Om du synes oppgavene blir for vanskelige å løse, kan du hoppe til del 6.

### Opplæring: Await-blokker

Man bruker Javascript-løfter (_promises_ på engelsk) til handlinger som kan ta tid og muligens kan mislykkes, ofte nettverksforespørsler. Svelte har en egen blokk for å ta seg av løfter, og denne heter await-blokken.

Løs [oppgaven om await-blokker fra Svelte-opplæringen](https://svelte.dev/tutorial/await-blocks) før du går videre.

### Oppgave 5.2: Hent topplista fra API-et

SvelteKit-prosessen som kjøres under utvikling inneholder en liten i-minne-database som holder styr på en toppliste som man kan hente ut tidligere poengsummer fra og poste sin siste poengsum til.

Funksjonen `fetchScores` fra `api.js` henter topplista. Oppgaven din er å importere denne funksjonen og vise topplista i «Game Over»-komponenten du har laget.

Dersom du ønsker å holde deg til samme visuelle tema som i resten av spillet, kan du sjekke [dokumentasjonen for stilarket Nes.css](https://nostalgic-css.github.io/NES.css/) (eller fasiten).

Advarsel: Akkurat når man jobber med løfter, kan navngitte funksjoner (de som er definert med nøkkelordet `function`) oppføre seg rart. For å unngå bugs, bruk pilfunksjoner (altså `const foo = () => {…}`).

### Opplæring: Binde variabler til input-felter

Løs [oppgaven om tekst-input og binding](https://svelte.dev/tutorial/text-inputs) før du går videre.

### Oppgave 5.3: Legg til et felt der folk kan fylle inn navnet sitt

Oppgaven din er å lage et felt der folk kan fylle inn navnet sitt. Lag også en knapp som folk kan trykke på for å sende inn navn og poengsum på formatet `{ name: string, score: number }`. Du kan bruke funksjonen `postScore` fra `api.js` til dette.

Når poengsummen er sendt inn, skal komponenten hente den oppdaterte topplisten.

Merk: Fordi databasen ikke lagres til noe permanent minne, vil alt man har lagt til i den forsvinne når man starter utviklingstjeneren på nytt. Hvis du ødelegger databasen ved å sende inn feilformatert data, kan du starte utviklingstjeneren på nytt for å starte med blanke ark.

## Del 6: Game Over?

Gratulerer! **Du var veldig flink som leste gjennom oppgavesettet før du begynte!** Eller kanskje du faktisk har gjort alle oppgavene? Wooooaaahh!!!!!1

![Et bilde av game over-skjermen i kabal][solitaire-win-png]

Del 6 er en sandkasse der du kan gjøre omtrent hva du vil.

### Oppgave 6.1: Forbedre spillet

Det finnes fortsatt noen mulige forbedringer av spillet:

#### Oppgaver uten løsning i main-branchen

Følgende funksjoner har vi ikke selv prøvd å lage (ennå), men vi tror de er både løsbare – og gøyale:

- **Hull i kantene**: Hull i brettets kanter som gjør at man kan komme ut av et tilsvarende hull på den andre siden, som i Pacman.
- **Hindre**: Visse områder midt på brettet er umulige å gå gjennom – kall dem vegger, øyer eller hva som helst. De er som kanten av brettet: Slangen dør når den treffer et slikt område.
- **Gullepler**: Få gullepler til å dukke opp i ny og ne i tillegg til det vanlige eplet. Disse gir 5 ekstra poeng hvis man spiser dem innen en viss tid.
- **Lydeffekter**: Legg på lyder når slangen spiser eplet, når den dør og lignende. Husk å bruke hodetelefoner dersom du deler arbeidslokale med andre.

Hvis du ikke føler deg klar for å jobbe uten fasit ennå, kan du prøve deg på en oppgave du finner løsningen på i main-branchen.

#### Oppgaver med løsning i main-branchen

Spillet som ligger i main-branchen har noen funksjoner som det ikke er laget oppgaver for:

- Pause
- Startskjerm
- Omstart-knapp på game-over-skjermen

Start med repoets tilstand slik det er i fasiten på oppgave 5.3 og prøv å lage disse funksjonene uten å kikke på fasit.

### Oppgave 6.2: Alternative spill

Kanskje du kan lage et av følgende spill:

- [Whac-a-Mole](https://en.wikipedia.org/wiki/Whac-A-Mole) – [vi har allerede gjort et forsøk](https://mos.knowit.no/)
- [Breakout](<https://en.wikipedia.org/wiki/Breakout_(video_game)>)

### Oppgave 6.3: Etter dette kurset

Om man synes Svelte er gøy og vil lære mer, har vi følgende anbefalinger:

- Gjør [hele Svelte-opplæringen](https://svelte.dev/tutorial/)
  - Sjekk ut [dokumentasjonen](https://svelte.dev/docs) etterpå. Man kan nesten alt som står der etter opplæringen.
- Prøv ut [SvelteKit](https://kit.svelte.dev/), Sveltes motsvar til for eksempel Next.js og Nuxt.js.
  - Ditt første prosjekt kan for eksempel være en hjemmeside fylt av alle spillene dine. Legg den ut i påvente av at «flash-spill» kommer på moten igjen.

### Avsluttende ord

Da gjenstår det kun å si at vi håper du har kost deg med kurset vårt. Game over!

[apple-near-middle-of-board-png]: ../../assets/task_1.1_end.png
[axes-png]: ../../assets/axes.png
[gameplay-png]: ../../assets/gameplay.png
[solitaire-win-png]: ../../assets/solitaire_win.png
[source-code-size-png]: ../../assets/source_code_size.png
[task-1-2-end-png]: ../../assets/task_1.2_end.png
[tasks-eng]: ../../TASKS.md
[tasks-nob]: .
[transfer-size-png]: ../../assets/transfer_size.png