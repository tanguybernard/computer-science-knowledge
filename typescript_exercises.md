# Typescript

## Some exercises

https://typescript-exercises.github.io/#exercise=10&file=%2Findex.ts

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

## Mapped Type

Supposons que notre programme garde une trace des appareils électroniques, de leurs fabricants et de leurs prix. Nous pourrions avoir un type comme celui-ci pour représenter chaque appareil :

  type Device = {
    manufacturer: string;
    price: number;
  };


Créons un type qui permet de créer un setter pour chaque clé du Device :

    type DeviceFormatter = {
        [Key in keyof Device as `format${Capitalize<Key>}`]: (value: Device[Key]) => string;
    };


    /*
    Resultat
    type DeviceFormatter = {
      formatManufacturer: (value: string) => string;
      formatPrice: (value: number) => string;
    };
     */


    const deviceFormatter: DeviceFormatter
    = {
      formatManufacturer: (value: string) => value,
      formatPrice: (value: number) => value.toFixed(2),
    };


  
    class SamsungGalaxyBook implements DeviceFormatter {
    
      public formatPrice (value: number) {
        return value.toFixed(2);
      }
    
      public formatManufacturer (value: string) {
        return value;
      }
    
    }

## Branding & Flavoring

Exemple du problème auquel nous pouvons faire face.

    type PostId = number;
    type CommentId = number;
    
    const postId: PostId = post.id;
    const commentId: CommentId = postId; // OK

Branding

Voici notre même exemple utilisant le type branding :

    type PostId = number & { __brand: 'PostId' };
    type CommentId = number & { __brand: 'CommentId' };
    
    const value = 1 as PostId;
    
    const postId: PostId = value; // OK
    const commentId: CommentId = value; // Erreur

De manière générique

    type Brand<T, U> = T & { __brand: U };
    
    type PostId = Brand<number, 'PostId'>;
    type CommentId = Brand<number, 'CommentId'>;


Limitations
Le changement d'un type en un type brandé requiert de le caster manuellement ;
  
Il est possible de lire la propriété __brand ;
  
Il n'y a pas de conversion implicite possible, par exemple :
  
    type Post = Brand<{ author: string; content: string; }, 'Post'>;
    const createPost = (post: Post) => { ... };
    createPost({ author: 'matthieu', content: 'Hello world!' }); // Erreur


Flavoring

Le flavoring est similaire en tout point au branding, au détail près que la propriété __brand est rendue optionnelle. Cette technique nous permet d'avoir une conversion implicite pour les types et les objets :

    type Flavor<T, U> = T & { __flavor?: U };
    
    type Post = Flavor<{ author: string; content: string; }, 'Post'>;
    type PostComment = Flavor<{ author: string; content: string; }, 'PostComment'>;
    
    const createPost = (post: Post) => { ... };
    createPost({ author: 'matthieu', content: 'Hello world!' }); // OK
    
    const comment: PostComment = { author: 'matthieu', content: 'Hello world!' };
    createPost(comment); // Erreur

S'il est communément admis qu'il est préférable d'utiliser le branding pour les types primitifs, le flavoring peut être préférable pour les objets afin de tirer bénéfice de la conversion implicite. On peut utiliser un type conditionnel pour faire ce travail à notre place :

    type Brand<T, U> = T & { __brand: U };
    type Flavor<T, U> = T & { __flavor?: U };
    
    type Nominal<T, U> = T extends object ? Flavor<T, U> : Brand<T, U>;


https://galadrim.fr/blog/type-branding-and-flavoring-rendez-votre-code-typescript-plus-lisible-et-robuste

## Safe optional values, errors represented as data  (WIP)

A partir de cette interface qui represente une donnée provenant d'une api, nous devrons convertir ces données en un objet du domaine.

    interface ElementDto {
        opacity: number;
        color: string;
        label: string | null;
    }

La couleur de domaine est celle-ci:

  type Color = 'lightcyan' | 'darkorchid';



    import { Maybe } from 'true-myth';
    
    
    type Element = {
        opacity: number;
        color: Color;
        label: Maybe<string>;
    }
    
    const dtoToDomain: Record<string, Color | undefined> = {
      clr_light: 'lightcyan',
      clr_dark: 'darkorchid',
    };
    
    const mapDtoToValues = (dtoColor: string): Color | never => {
      const domainColor = dtoToDomain[dtoColor];
    
      if (typeof domainColor !== 'undefined') {
        return domainColor!;
      }
    
      throw new Error(`Could not map the value "${dtoColor}" to a domain value of type Color`);
    };
    
    
    
    
    const element: ElementDto = {
      opacity: 0.5,
      color: 'clr_light',
      label: null,
    };
    
    const mapElementDtoToElement = ({ opacity, color, label }: ElementDto): Element => ({
      opacity,
      color: mapDtoToValues(color),
      label: Maybe.of(label),
    });
    
    const mappedElement = mapElementDtoToElement(element);
    
    console.log(mappedElement.label.toString());//Nothing
    
    console.log(mappedElement.label.mapOr('No label', r => r));//No label



//https://softwaremill.com/translating-api-responses-into-type-safe-interfaces-with-typescript/


## Exercice Type Réponse APi exemple avec Tableau server (WIP: continue exo avec la requete: body data... et l'erreur, si resposne erreur: {errors: [ {id: 34, message: "lallala"}]} ) donc reponse = ReponseApiUser | ReponseError


La reponse Api contient toujours une clé correspondant a la ressource

    type ResourceApi = 'site' | 'user';
    
    type ResponseApi<T extends  ResourceApi> = {
        [key in T]: {
            id: string;
            name: string;
        }
    }

Ensuite on etend pour le user avec mail
    
    type ResponseApiUser<T extends ResourceApi> = ResponseApi<T> & {[key in T]: {email: string}};
    
    
    const responseApiUser: ResponseApiUser<'site'> = {
      site: {
        id: '1',
        name: 'Site',
        email: '<EMAIL>',
      },
    
    };
    
    
    console.log(responseApiUser.site.email);

https://stackoverflow.com/questions/56419558/typescript-how-to-use-a-generic-parameter-as-object-key
  
## Credits


https://blog.logrocket.com/typescript-mapped-types/

https://dev.to/logrocket/mastering-mapped-types-in-typescript-344g
