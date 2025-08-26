## Del 1 CPU, Memory, I/O
Datamaskin arkitektur er bygget opp av en CPU (med en Control unit CU, Arithmetic Logic Unit (ALU) og registere), minne og I/O.

Det kan være von Neumann arkitektur hvis instruksjoner og data deler busser og minne. 
Eller Harvard/modified Harvard arkitektur hvis det er egne busser for data og instruksjoner.

CPU-en har en intern klokke som sier når den skal "gjøre" noe. Denne sender ut puls hvert nano-sekund.

**CPU**:  Central processing unit, hoved prosessoren. Hjernen til datamaskinen, og komponenten som er ansvarlig for å utføre maskin instruksjoner.
- **MMU**: Memory Management Unit, viktig komponent som lar hvert kjørende program få sitt eget minne område. 
- **CU**: Control unit, kontrollerer dataflyt og og gjør alt forarbeid slik at ALU kan utføre instruksjoner.
- **ALU**: Arithmetic Logic Unit, får data fra CU. Utfører aritmetiske og logiske instruksjoner på binære tall.
- **Registrere**: Minste og raskeste lagringen på datamaskinen, typisk mellom 8 og 64 blir lagret i registrene.
	- **AX, BX, CX, DX, SP, BP, SI, DI**: Data registere som lagrer variabler, argumenter, return verdier ol.
	- **IP/PC**: Instruction pointer og Program counter. Inneholder address til neste instruksjon som skal lastes fra minne og utføres.
	- **IR**: Instruction register. inneholder instruksjonen som vil utføres av ALU.
	- **SP**: Stack pointer. Inneholder adressen til toppen av stack-en.
	- **BP**: Base pointer/Frame Pointer. Base pointer inneholder adressen til bunnen av stack rammen. En stack  er delt i stack rammer (stack frames), den blir lagd når du kaller en funksjon og slettet når du return-ere noe fra en funksjon.
	- **FLAG/PSW**: holder kontroll/status på informasjon. Eks: om resultatet på en sammenlikning.
	  
- **Memory/RAM**: Random Access Memory. Program blir lastet inn i minne, og de inneholder instruksjoner og data. Alt blir lagret i bit, (8 bit = 1 byte).  En byte er det minste man kan laste fra minne. Hver minne adresse går til en byte, og ikke en bit.
  
- **I/O-devices**: I/O er koblet til datamaskinens sentral buss, og blir brukt av CPU-en for å få informasjon inn og ut av datamaskinen. Disse enhetene har er "mindre datamaskiner", med en prosessor, noe minne, noe software (firmware) og noe interaces (dens egne registere som CPU kan lese og skrive til). SSD har en kontroller som CPU kan snakke med og egne lagring bak kontrolleren.
  

### Registere
Registere kan være 8, 16 eller 64 bit versjoner.  

Hvis det registere starter med **r** er det 64 bit versjonen (rax, rip, rsp).
Hvis det registere starter med **e** er det 32 bit versjonen (eax, eip, esp).

16 og 8 bit er sjeldne idag.

### ISA
Instruction set architecture:
- naive data types and instructions
- registers
- addressing mode
- memory architecture
- interrupt and exception handling
- external I/O

Hver ISA har et spesifikt set instruksjoner den kan utføre. Disse kan varriere fra arkitektur til akritektur (intel, amd x86.). Assemly er symbolsk representasjon av maskin instuksjoner. 


**Vanlig instruksjoner**:
- Move/copy data - mov
- Math functions - add, sub
- Function related - call, ret
- Jumping - jmp, je (if equal), jne (junp if not equal)
- Comparing - cmp
- Stack - push, pop


## Del 2 Minne Stack
Med uten interrupts
![[Pasted image 20250825121203.png]]

Med interrupts
![[Pasted image 20250825121344.png]]
### Registere vs fysisk minne
Registrene sitt innhold tilhører det programmet som kjører og operativ systemet. 

De kan være flere programmer lastet i minne samtidig (multiprogramming). Men bare en lastet per CPU kjerne (to kan være lastet hvis man har Hyperthreading/SMT er tilgjengelig).


### Program i minne
![[Pasted image 20250825122401.png]]


- **Text**: Det faktiske programmet, maskin instrukser. Text fordi det er program text.  
- **Data/heap**: Vokser oppover og er delt i Data, BSS (Black started by symbol) and heap. Dette inneholder globale variabler, lokale statiske variabler og dynamiske allokerte variabler.  
- **Libraries**: Biblioteker som flere programmer bruker vil ligger her. "Load the library" betyr egentlig "point to the library". Man trenger ikke lagre samme biblotek flere ganger.
- **Stack**: call stack/ user space stack. Område som vokser nedover . En stack er en data struktur som likner en bøtte. Det siste man legger i bøtten vil ligge på toppen. Stacken er delt i *stack frames*. Verdien av *base pointer register* (EBP/RBP) peker til bunnen av den øverste stack framen.  *Stack pointer register* (EBP/RBP) peker alltid til toppen av stacken (topen av den øverste stack framen). 
  
  Når koden din går inn i en funksjon blir en ny stack frame lagd, og den blir fjernet når du går ut av funksjonen. Her blir automatiske variabler, return addresser og i noen tilfeller funksojn argumenter blir lagret. 

## Del 3 Assembly
Når du kompilerer kode får man instruksjoner (assembly) dette er not portable, til andre arkitekturer.
 
### gcc
gcc er en kompiler som vil gi assembly kode med -S

gcc -fno-asynchronous-unwind-tables -S tmp.c
-fno-asynchronous-unwind-tables fjerner .cfi-lines

### 32 vs 64 bit
Instructions
- q for 64 bit, pushq
- l for 32 bit, pushl

Register
- r for 64 bit, rbp
- e for 32 bit, ebp

### Syntax
![[Pasted image 20250825131118.png]]
Direktiver starter med . og labels slutter med(:). 

- instructions/opcode is called a mnemonic
- mnemonic suffix b(byte), word (2 byte), long (32 bit), q( quadword 64 bit)
- % is a register
- $ is a constant
- Address calculation: movl -4(%ebp), %eax, her betyr () sted i minne
  Hent det som er i addresse(%ebp-4) last det til %eax



## Del 4 CPU Hyperthreading

### Pipeline
![[Pasted image 20250825182611.png]]

Man laster enn, når den er ferdig laster man neste,(a). Dette går løpende slik at man ikke venter.

(b) er en super scalar cpu, hvor man har flere spesialiserte pipelines samtidig.

Speculative execution er branch speculation hvor cpu-en prøver å "gjette" resultatet av en jump instruksjon. Når cpu-en har hentet jump instruksjonen, så gjetter den basert på resultatet av tidligere jump instruksjoner og starter å hente instruksjoner, isteden for å vente på kondisjonen. Når kondisjonen har blitt prosessert så sjekker cpu-en om den hadde rett. Hvis den tok rett så går alt som normalt, hvis ikke så må den laste de andre instruksjonene.


### Hyper threading
![[Pasted image 20250825183514.png]]
Hvis en CPU har hyperthreading vil den visse seg som 2 cpu-er for OS-en. Dette er fordi den kan kjøre to programmer samtidig. Her er representerer det gule og røde programmer.
I effekt har en hyper thread cpu dobbelt opp av alt en cpu har, registere, CU og MMU. MEN det har bare en ALU. 

Med hyper threading har man evnen til å laste 2 programmer fra minne til cpu, men det hjelper ikke med antall operasjoner man kan gjøre pr/s. Det hjelper ved at man kan bytte raskere mellom to programmer.

## Del 5 Cache

CPU har cache mellom seg og minne.

CPU spør cache etter noe, cache har det ikke. Cache spør minne om det har noe, det har det, så lagres det i cache. Nå når cpu spør vil det få det fra cache.

Cache funker fordi vi gjenbruker data i rommet (spatial locality) og tid (temporal locality). Den misnte biten data man kan hente fra minne er 1 byte, men vi cacher alldri 1 byte, man cacher en cache linje (64 byte) 


### Write policy

Write-Through: write to cache line and immediately to memory
Write-Back: Write to cache line and mark cache line as dirty.

Med **write-back** blir data bare skrevet til minne når cache linjen skal bli over-skrevet av en annen eller i tilfeller som context switch. 
For å gjøre dette må man sjekke om cache linjen man vil skrive er dirty (data som ikke er blitt skrevet til neste nivå minne). Dette gjelder for både read og write operasjoner.

**Write-Through** er den enkleste og tryggeste, (fordi de vil alltid finnes en kopi av data-en et annet sted). Men siden man skriver til minne med en gang, vil man ha lavere ytelse.

