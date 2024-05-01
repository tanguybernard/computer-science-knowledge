# Functional


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
