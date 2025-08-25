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


## Del 2


## Del 3


## Del 4


## Del 5
