# Typescript


## Index signatures in TypeScript

Ecrire un type User, qui comportera un "name" et des preferences non connu à l'avance, les preferences ont une clé de type string et une valeur de type string :

  type User = {
    name: string;
    preferences: {
      [key: string]: string;
    }
  };
  
  const currentUser: User = {
    name: 'Foo Bar',
    preferences: {
      lang: 'en',
    },
  };
  const currentLang = currentUser.preferences.lang;


  
## Credits


  https://blog.logrocket.com/typescript-mapped-types/
