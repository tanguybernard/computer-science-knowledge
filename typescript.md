# Typescript

## Type validators

    type Units = 'px' | 'rem' | '%';
    
    type IsValidCSS<T> = T extends `${number}${Units}` ? true : false;
    
    type StringNumber<T extends number> = `${T}`;
    
    type IsAllowedNumber<T> = 
      T extends `${infer Num}${Units}` 
      ? Num extends StringNumber<99> 
      ? false 
      : true 
      : false;
    
    type Validator<T extends boolean> = 
      T extends true 
      ? [] 
      : ['Dear developer, please use valid CSS values'];
    
    const foo = <T extends string>
      (
        arg: T,
        ...validation: [...Validator<IsValidCSS<T>>, ...Validator<IsAllowedNumber<T>>]
      ) => { }
    
    foo('100px'); // ok
    foo('99px'); // expected error

https://catchts.com/validators)https://catchts.com/validators


## Credits

https://catchts.com/
