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

https://marmelab.com/blog/2018/04/18/functional-programming-2-monoid.html

    const fetchTodo = async (a:number) => fetch(`https://jsonplaceholder.typicode.com/todos/${a}`);
    
    
    const toJson = async (response:any) => response.json();
    const getTitle = (json:any) => json.title;
    
    const flow = (func1:any, func2:any) => async (x:any) => func2(await func1(x));
    // func1 is executed before func2
    const flowArray = (functions:any) => functions.reduce(flow, (x:any) => x);
    // let's make it a function that takes an arbitrary number of arguments instead
    const flowArgs = (...args: any) => args.reduce(flow, (x:any) => x);
    
    // now, writing getJoke() becomes much easier
    const getTodo2 = flowArgs(fetchTodo, toJson, getTitle);
    getTodo2(2).then(res => console.log(res));
