# Phantom Type


## C'est quoi ?

Un type fantôme est un type dont la déclaration comporte un paramètre de type qui n'est pas réellement utilisé par les constructeurs ou les champs de ce type.

Un type fantôme est un type générique qui n'est jamais utilisé à l'intérieur d'un objet. Pourquoi existe-t-il alors ? Sécurité des types.

##  Pourquoi ?


Avec les types fantômes, vous pouvez ajouter des informations supplémentaires à vos types et les utiliser pour restreindre le code afin de rendre impossibles les situations non valides. Plus il y a de restrictions, moins il y a de place pour les erreurs de programmation, mieux le code est auto-documenté et moins il y a de tests. 

source: https://kean.blog/post/phantom-types

## Example :

https://oleb.net/blog/2016/08/measurements-and-units-with-phantom-types/




### Kotlin 1

L'idée est d'empêcher les objets d'avoir un état illégal ou d'interdire les opérations illégales au moment de la compilation.

    sealed class DoorState
    object Open: DoorState()
    object Closed: DoorState()
    
    class Door(val state: DoorState) {
        fun open() = Door(Open)
        fun close() = Door(Closed)
    
    }
    
    fun open(): Door {
        val state = Open
        return if (state == Open) throw IllegalStateException() else Door(Open)
    }
    
    val success1 = Door(Open).open()
    
    var failed1 = Door(Closed).open()
    
    class DoorPhantom<out T: DoorState>(val state: T)
    
    fun DoorPhantom<Closed>.open() = DoorPhantom(Open)
    fun DoorPhantom<Open>.close() = DoorPhantom(Closed)
    
    
    val success = DoorPhantom(Open).close()
    
    var failed = DoorPhantom(Open).open()//error


### Kotlin 2

The Kotlin equivalent would be next. Let’s pretend that you have code:

    data class User(val id: String)
    data class Address(val id: String)
    
    val me = User(id = "test id")
    val home = Address(id = "test id")
    
    if (me.id == home.id) {
      assert("Wrong! Person can not be address")
    }

Isuru Rajapakse came with the next improvement:

    @JvmInline value class UserId(val value: String)
    @JvmInline value class AddressId(val value: String)
    
    data class User(val id: UserId)
    data class Address(val id: AddressId)
    
    val me = User(id = UserId("test id"))
    val home = Address(id = AddressId("test id"))
    
    if (me.id == home.id) {} // This will not compile

That has minimum performance penalty but still require some boilerplate code writing.

//

Then Ivan Canet proposed an improvement that will require also minimum boilerplate and will be 100% equivalent to the swift code:

    @JvmInline value class Id<out T>(val value: String)
    
    data class User(val id: Id<User>)
    data class Address(val id: Id<Address>)
    
    val me = User(id = Id("test id"))
    val home = Address(id = Id("test id"))
    
    if (me.id == home.id) {} // This will not compile also

source: https://emartynov.medium.com/kotlin-ddd-phantom-type-ae5ab1da0a35
### Typescript (should be improved)


    type Open = {_type: 'Open'};
    type Close = {_type: 'Close'};
    
    type DoorState<T, D =never> = {value: never} & T;
    
    type InitDoorClosed = (a: string) => DoorState<Close>;
    type CloseDoor = (a: DoorState<Open>) => DoorState<Close>;
    type OpenDoor = (a: DoorState<Close>) => DoorState<Open>;
    
    
    const initDoorClosed: InitDoorClosed = value => {
      return { value } as DoorState<Close>;
    };
    export const openReally: OpenDoor = value => {
      return { value } as DoorState<Open>;
    };
    
    export const closeReally: CloseDoor = value => {
      return { value } as DoorState<Close>;
    };
    
    const initialData = initDoorClosed('open');
    
    const openedDoor = openReally(initialData);
    const closedDoor = closeReally(openedDoor);//ferme une porte ouverte
    
    const closeADoorAlreadyClose = closeReally(closedDoor); //ferme une porte deja ferme BOOM ca pete, normal

### TS 2

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


### TS 3


    //Problem
    
    function submitCommentAaargh(
      user: any,
      comment: string
    ) {
      console.log(comment);
    
    }
    function onSubmitAaaargh() {
    
      const user = { age: 20, name: 'toto', hasPermission: (p:string) => true };
    
      if (!user.hasPermission('writeComment')) {
        console.log({
          message: 'Sorry you can\'t post comments!',
        });
      }
      submitCommentAaargh(user, 'My super comment');
    }
    
    //Solution
    
    type User = {
        // this is the only relevant property for our system
        permissions: number
        // with any other user-related property
        // you can think of
        name: string
        age: number
    }
    
    
    declare const phantom: unique symbol;
    
    const writeComment = { writeComment: true } as const;
    type WriteComment = typeof writeComment
    const readComment = { readComment: true } as const;
    type ReadComment = typeof readComment
    type Permissions = WriteComment & ReadComment
    type SomePermissions = Partial<Permissions> // writeComment | readComment
    
    
    type AuthorizedUser<T extends SomePermissions> = User & {
        address: string
        [phantom]: T
    }
    
    
    type PermissionResult<T extends SomePermissions> =
        | { type: 'ok', user: AuthorizedUser<T> }
        | { type: 'fail', reason: string }
    
    function authorize<T extends Permissions>(
      user: User,
      permission: T
    ): PermissionResult<T> {
      if (user.age>18 && permission.writeComment) {
        return { type: 'ok', user: user as AuthorizedUser<T> };
      } else {
        return { type: 'fail', reason: 'User does not stan loona' };
      }
    }
    
    function hasPermission<T extends SomePermissions>(user: User, p: T): user is AuthorizedUser<T>;
    function hasPermission<T extends Permissions>(
      user: User,
      permission: T
    ): user is AuthorizedUser<T> {
      return authorize(user, permission).type === 'ok';
    }
    
    
    function submitComment(
      user: AuthorizedUser<WriteComment>,
      comment: string
    ) {
      console.log(comment);
    
    }
    
    
    
    function onSubmit() {
      //const result = authorize(user, writeComment);
      //if (result.type === 'fail') {
      const user: User = { age: 20, name: 'toto', permissions: 0 };
      //if (!hasPermission(user, {...writeComment, ...readComment})) {
      if (!hasPermission(user, writeComment)) {
        // user has type User here
        console.log('You are not authorized to write comments');
        return 'You are not authorized to write comments';//comment and see error message
      }
      // user has type User here
      submitComment(user, 'My super comment');
    }
    
    onSubmit();

## TS 4



    declare const phantom: unique symbol;
    
    type Mile = {[phantom]: "Mile"};
    type Kilometer = {[phantom]: "Kilometer"};
    
    type Distance<T, D = never> = {value: never} & T;
    
    type DistanceMile = (a: number) => Distance<Mile>;
    type DistanceKm = (a: number) => Distance<Kilometer>;
    
    export const createDistanceMile: DistanceMile = value => {
        return { value } as Distance<Mile>;
    };
    
    export const createDistanceKm: DistanceKm = value => {
        return { value } as Distance<Kilometer>;
    };
    const tenKm = createDistanceKm(10)
    const tenMiles = createDistanceMile(10)
    
    type addDistance = <T,E, C>( a: Distance<T> )=> ((b:Distance<E>)=> Distance<C>) ;
    
    const add = <T> (a: Distance<T>) => b => a.value+b.value as T
    const addKilometersToMiles  = (a: Distance<Kilometer>) => (b:Distance<Mile>) => a.value + (b.value*0.621371)
    
    //const result = add(20)(twentyMiles)//issue car doit etre distance valide
    const result = addKilometersToMiles(tenKm)(tenMiles);
    
    console.log(result)


https://www.stevenleiva.com/posts/phantom_types


## TS5: Exemple Groupe Sanguin

    declare const phantom: unique symbol;
    
    //Phantom declaration
    type OPositive = {[phantom]: 'O+'}
    type ONegative = {[phantom]: 'O-'}
    type APositive = {[phantom]: 'A+'}
    type BPositive = {[phantom]: 'B+'}
    type ABPositive = {[phantom]: 'AB+'}
        
    //Sang, une valeur et un Phantom Type
    type Blood<Type> = {value: never} & Type
    // Signature pour créer un donneur OPositif
    type BloodOPositive = (value: string) => Blood<OPositive>
    type BloodAPositive = (value: string) => Blood<APositive>
    type BloodABPositive = (value: string) => Blood<ABPositive>
    type BloodONeg = (value: string) => Blood<ONegative>

    //Implémentation
    const createOPositive : BloodOPositive = (value) =>  {
      return {value} as Blood<OPositive>;
    };
    
    const createAPositive : BloodAPositive = (value) =>  {
      return {value} as Blood<APositive>;
    };
    
    const createABPositive : BloodABPositive = (value) =>  {
      return {value} as Blood<ABPositive>;
    };
    const createONegative : BloodONeg = (value) =>  {
      return {value} as Blood<ONegative>;
    };

    //Type de receveur De OPositve
    type ROP = (ABPositive|APositive|BPositive|OPositive)
    //TODO Tous enfin presque, il manque Les negatif
    type ALL = (APositive|BPositive|ABPositive|OPositive|ONegative)

    //Les combinaison
    function GiveBlood( a: Blood<ABPositive> ,b:Blood<ABPositive>) : string ;
    function GiveBlood( a: Blood<APositive> ,b:Blood<APositive|ABPositive>) : string ;
    function GiveBlood( a: Blood<OPositive> ,b:Blood<ROP>) : string ;
    
    function GiveBlood(a: Blood<ALL>, b:Blood<ALL>) {
      return a.value+' '+b.value;
    }
    
    const userOPositive = createOPositive('O Rh');
    const userOnegative = createONegative('O');
    const userAPositive = createAPositive('A Rh');
    const userAbPositive =createABPositive('AB Rh');
    
    
    
    const a = GiveBlood(userOPositive, userAPositive);
    console.log(a);

### Kotlin

    data class BloodSample<T>(val value: String) {
        
         operator fun plus(other: BloodSample<T>): BloodSample<T> =
                BloodSample(value + other.value)
       
    }
    
    
    object OP
    object ON
    
    
    fun main() {
        
        var t = BloodSample<OP>("toto")
        var i = BloodSample<ON>("toto")
        
        print(t + i)//Error
        
    }

## Credits

https://medium.com/@reidev275/creating-a-more-descriptive-query-model-with-phantom-types-93d8a5c2d5d9

https://www.bussieck.com/typescript-types-with-complex-properties/

https://stackblitz.com/edit/typescript-isbn-type-constraints?file=index.ts

https://proandroiddev.com/phantom-types-in-kotlin-afd3f59fde10

https://davesquared.net/2019/01/phantom-types.html

https://www.hackingwithswift.com/plus/advanced-swift/how-to-use-phantom-types-in-swift

https://sporto.github.io/elm-patterns/advanced/phantom-types.html
