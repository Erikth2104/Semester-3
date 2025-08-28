Tree: en graf uten sykler

Terminologi:
Node (child, parent)
Kant: koblinger mellom noder
Sti: kantene man må gjennom for å nå en node
Root ("toppen" av treet)

Kun en sti mellom alle noder (også via rota), eller er det en graf
Over - under
Parent - child - sibling - barnebarn besteforeldre 
Interne node - node med minst et blad
Terminal/blad node - noder uten barn, nederst på en sti
Grad - Antall barn hver node har, (treets grad er graden til noden med høyest grad)
Nivå - rot er på nivå 1 eller 0
Dybde - antall kanter fra rota og til en gitt node
Høyde: antall kanter fra en node og ned til dens fjerneste bladnode
Sti-lengde - summen av alle stiene fra rota og til enhver node
Ikke-sortert - verdien til hver node spiller ikke rolle
Ordnet/sortert - hver node på venstre side har lavere "verdi" enn nodene på venstre side
![[Tree.png]]


Subtre
![[SubTree.png]]


Skog: 




Multiveis tre: hver node har opptil N bran, evt fylle ut med bladnode(r)

Binært tre: alle interne noder har eksakt to barn (men treet trenger ikke å være balansert av den grunn).

Komplett binært tre: Alle bladnodene slutter på samme nivå, unntatt evt, det aller nederste, men det er fylt opp med noder fra venstre mot høyre


Binært søketre: sortert tre

B-tre:

Balansert tre:


2-3-4 tre: 

Red-Black tre:



### Egenskaper av tre
1. Eksakt en sti (via rota?) mellom to noder i et tre
2. N noder har N-1 kanter (fordi all med en link opp til mor, unntatt rota)
3. Binært tre: N noder har N+1 tomme "barn"/nullptr
4. Fullt balansert binært tre: høde er ca $log_2(N)$ (avrundet til nørmeste heltall)


### Traversering av trær

**Preorder**
1. Visit seg selv
2. Traverser venstre 
3. Traverser høyre


**Inorder**
1. Traverser venstre 
2. Visit seg selv
3. Traverser høyre


**Postorder**
1. Traverser venstre 
2. Traverser høyre
3. Visit seg selv


**LevelOrder**
Visit alle på ett og ett nivå, fra venstre mot høyre, ovenfra og nedover





















