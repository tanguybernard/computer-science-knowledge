# Phantom Type

    export interface Query<A> {
        sql: string;
        params?: any;
    }
    
    export const execute = <A>(query: Query<A>): A[] => {
      const t:A = {
        foo: 'bar',
        bar: 'baz'
      } as unknown as A;
      return [t];
    };
    
    const getData: Query<Baz> = {
      sql: 'Select foo, bar from baz'
    };
    
    export interface Baz {
        foo: string;
        bar: string;
    }
    
    const bazes: Baz[] = execute(getData);
    
    console.log(bazes);


## Credits

https://medium.com/@reidev275/creating-a-more-descriptive-query-model-with-phantom-types-93d8a5c2d5d9

https://www.bussieck.com/typescript-types-with-complex-properties/
