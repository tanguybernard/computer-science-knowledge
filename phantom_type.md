# Phantom Type


## C'est quoi ?

Un type fantôme est un type dont la déclaration comporte un paramètre de type qui n'est pas réellement utilisé par les constructeurs ou les champs de ce type.

## Kotlin

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

## Typescript (should be improved)


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

## Exemple 1

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


## Exemple 2


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

## Exemple 3 



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


## Credits

https://medium.com/@reidev275/creating-a-more-descriptive-query-model-with-phantom-types-93d8a5c2d5d9

https://www.bussieck.com/typescript-types-with-complex-properties/

https://stackblitz.com/edit/typescript-isbn-type-constraints?file=index.ts

https://proandroiddev.com/phantom-types-in-kotlin-afd3f59fde10

https://davesquared.net/2019/01/phantom-types.html
