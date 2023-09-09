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

  
## Credits


https://blog.logrocket.com/typescript-mapped-types/

https://dev.to/logrocket/mastering-mapped-types-in-typescript-344g
