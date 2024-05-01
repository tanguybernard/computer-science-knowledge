# Functional

## Monad

Monad is a pattern in functional programming !


## Pure Functions


En FP, les fonctions doivent être pures. Une fonction pure présente les caractéristiques suivantes :
- Son résultat ne dépend que de son entrée
- Elle ne mute aucune variable en dehors de son corps
- Elle ne modifie pas ses arguments
- Elle ne lance jamais d'erreur

## Currying

 Une fonction qui retourne une autre fonction, ce type de fonction est appelé fonction curry (curried function).

 Avec une fonction curry, le code qui manipule d'autres fonctions sait à quoi s'attendre. Une fonction a toujours besoin d'un seul argument pour s'exécuter.

## Monoid

Le terme monoïde provient de la théorie des catégories.

Un monoid est un __magma__ avec l'opération binaire qui est associative et qui possède un élément neutre.

En résumé: 

#### Combinaison

L'opération doit combiner deux valeurs de l'ensemble en une troisième valeur du même ensemble. Si a et b font partie de l'ensemble, alors concat(a, b) doit également faire partie de l'ensemble. En théorie des catégories, on appelle cela un _magma_.

#### Associativité

_concat(x, concat(y, z))_ doit être identique à _concat(concat(x, y), z)_ où x, y et z sont des valeurs quelconques de l'ensemble. 

#### Element Neutre

L'ensemble doit posséder un élément neutre par rapport à l'opération. Si cet élément neutre est combiné avec une autre valeur, il ne doit pas la modifier. concat(élément, neutre) == concat(neutre, élément) == élément



Chaque fois que vous devez composer un nombre arbitraire d'éléments (par exemple lors de l'aplatissement d'une hiérarchie d'objets, ou lors de la mise en œuvre d'un flux d'opérations asynchrones), pensez à un monoïde !

### Monoid Example

https://marmelab.com/blog/2018/04/18/functional-programming-2-monoid.html

    const fetchTodo = async (a:number) => fetch(`https://jsonplaceholder.typicode.com/todos/${a}`);
    
    const toJson = async (response:any) => response.json();
    const getTitle = (json:any) => json.title;
    
    console.log("Solution 1")
    const getTodo = async (n:number) => getTitle(await toJson(await fetchTodo(n)))
    getTodo(1).then(console.log); 


    // the getJoke() function is a pain to write. Let's use composition to make it easier
    const asyncCompose = (func1:any, func2:any) => async (x:any) => func1(await func2(x));

    // asyncCompose() is associative
    asyncCompose(getTitle, asyncCompose(toJson, fetchTodo))(23).then(console.log);
    
    asyncCompose(asyncCompose(getTitle, toJson), fetchTodo)(23).then(console.log);

    
    //----------- BETTER ------------
    
    const flow = (func1:any, func2:any) => async (x:any) => func2(await func1(x));
    // func1 is executed before func2
    //const flowArray = (functions:any) => functions.reduce(flow, (x:any) => x);
    // let's make it a function that takes an arbitrary number of arguments instead
    const flowArgs = (...args: any) => args.reduce(flow, (x:any) => x);
    console.log("Solution 2")
    
    // now, writing getTodo2() becomes much easier
    const getTodo2 = flowArgs(fetchTodo, toJson, getTitle);
    getTodo2(2).then(res => console.log(res));


