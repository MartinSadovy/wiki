## SOLID

### S - Single-Responsibility Principle
- jedena třída/modul má mít jednu odpovědnost ke SVÉ změně
- A module should be responsible to one, and only one, actor.

## O - Open-Closed Principle
> Objects or entities should be open for extension but closed for modification.

původní definice: můžeme rozšířit o nové fieldy, ale na venek se musí chovat konzistentně

nově: 
- interface, dědičnost
- extension function
- delegation

## L - Liskov substitution Principle

- vychází z 

> Let q(x) be a property provable about objects of x of type T. Then q(y) should be provable for objects y of type S where S is a subtype of T.

> Nechť q(x) je vlastnost prokazatelná pro objekty x typu T. Pak by q(y) měla být prokazatelná pro objekty y typu S, kde S je podtyp T.

Anglicky tldr: Subsclasses should be substitutable for their base classes.

Obecně na OOP: potomek předka (base/interface) je zaměnitelný. ALE!

Jde o mnoho pravidel:
- method argument typech (signaturách funkcí - argument, return type) 
- invariantech stavu třídy (property rules)
- že potomek nemá možnost ovlivnit stav předka, pokud to předek předtím neuměl (history constraint)
- preconditions, postconditions (method rules)

Příklad na zamyšlenou
> Objekt Čtverec dědí z obdélníku, je to přeci speciální případ že? Obdélník má však dvě vlastnosti: X,Y.  Co když na čtverci změníme Y (např. metoda changeY), to nám však z pohledu zastupotelnosti neříká že měníme X.


## I - Interface segregation principle
- prostě nedělat příliš velké rozhraní ale vyseparovat rozhraní na menší
- dynamicky typové jazyky toto neřeší díky duck duck

## D - Dependency Inversion Principle

> 1.  High-level modules should not import from low-level modules. Both should depend on abstractions.
> 2.  Abstractions should not depend on details. Details should depend on abstractions.

špatné příklady: máme singleton knihovnu (e.g. CSV parser, načtení z db) v kodu aniž bychom použili DI


tzn:
1) extrahujeme z high lvl do low lvl, a ty pomocí abstrakce (interfaců) použijeme


O - goal
S, D - codin strategy
