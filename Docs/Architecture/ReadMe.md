# Clean Architecture

Se va a implementar una arquitectura por capas siguiendo la terminología de la *clean architecture* propuesta por Robert Martin.

## Diagrama resumen
WIP.

## Correspondencia con MV*
Esta tabla asocia dicha terminología con patrones arquitectónicos MV*:

| Clean   |      MV*      |  Observaciones |
|:-------:|:-------------:|:--------------:|
| Controller |  Vista de entrada | Como hemos visto que era originalmente en SmallTalk |
| Interactor |    Controlador   |   Se definen a partir de los casos de uso |
| Entity | Modelo |    Como en Entity-Control-Boundary de Ivar Jacobson |
| Presenter | ¿Presentador? |    Puente entre controlador (Interactor) y vistas |
| View | Vista tonta |    Solo recibe modelos de datos que usa para cambiar el estado de la vista |
    
Los principios en los que se basa son los que pueden resumir a cualquier arquitectura multitier:
- El flujo de dependencias es unidireccional.
    - La dirección va de menos abstracción (mayor dependencia con tecnologías) a más abstracción.
- El flujo de control hace un viaje de ida y vuelta, siguiendo primero el flujo de dependencias y después el sentido contrario.

## Capas recomendadas

Las capas que propone por defecto la Clean Architecture son:

| Capa   |      Contiene      |  Conoce a | 
|:-------:|:-------------:|:--------------:|
| Domain |  Entities | Ninguna otra capa, ya que es la de mayor abstracción |
| Application |    Interactors/UseCases y Boundaries de entrada/salida   |   Domain |
| Adapters | Controllers, Presenters, implementación de Gateways... |    Application y tal vez Domain |
| Frameworks | Databases, UI... |    Adapters |

Las capas son maleables y pueden añadirse, trocearse o combinarse de la forma que mejor convenga al proyecto.

## Capas mínimas
Sin embargo, como mínimo debe existir la noción de estas dos grandes capas:

| Capa   |      Contiene      |  Conoce a | 
|:-------:|:-------------:|:--------------:|
| Domain |  Domain + Application | Ninguna otra capa, ya que es la de mayor abstracción |
| Infrastructure |  Adapters + Frameworks  |   Domain |
El nombre de Domain en este caso se extiende y es quizá desafortunado por su ambigüedad,
pero al final se trata de diferenciar, simplemente, entre abstracciones y detalles de implementación.

## Capas cohesivas
Estas organizaciones en capas, sin embargo, violan en mayor o menor medida uno de los seis principios de arquitectura que hemos visto, propuestos también por Robert Martin.  
Se trata del *Reuse/Release Equivalence Principle*, que dice que los componentes (paquetes) deben poder desplegarse de forma independiente sin afectar al resto.  
Es decir, que los componentes de un sistema sean cohesivos.

Para ello habría que trocear las capas más exteriores, ya que por ejemplo la de adaptadores incluye tanto controladores como presentadores, que no tienen cohesión entre sí.  
Este troceo se ejemplifica comparando las tres siguientes imágenes, donde:
- la primera define la arquitectura propuesta en general;
- la segunda muestra el flujo de dependencias según abstracción;
- la tercera la trocea para aumentar la cohesión de componentes;


![](CleanArchitecture.jpg)
![](CleanArchitecture-OneSlice.jpg)
![](CleanArchitecture-Sliced.png)



