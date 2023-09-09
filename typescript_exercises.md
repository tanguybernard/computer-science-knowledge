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




  
## Credits


https://blog.logrocket.com/typescript-mapped-types/

https://dev.to/logrocket/mastering-mapped-types-in-typescript-344g
