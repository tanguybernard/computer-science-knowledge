# Railway (Railroad) Programming / Result operation Pattern / Either



## Intro

- Gestion structurée des erreurs
- Réduction de l'encombrement des erreurs
- Composition facile des fonctions
- programmation pure
- 




## Example



    interface Success<a> {
        kind: 'success'
        value: a
    }
    interface Failure<e> {
        kind: 'failure'
        error: e
    }
    type Result<a, e> = Success<a> | Failure<e>
    
    
    const unit = <a>(a:a): Success<a> => ({kind: 'success', value: a})
    const failed = <e>(e:e): Failure<e> => ({kind: 'failure', error: e})
    
    
    const getUser = () => ({firstname: "John", lastname: "doe"})

    const renderUser = (): Result<string, 'no-user'| 'no-name'> => {
        const user = getUser()
        if (user == null) return fail('no-user')
        if (user.firstname && user.lastname) return unit(`${user.firstname} ${user.lastname}`)
        if (user.firstname) return unit(user.firstname)
        if (user.lastname) return unit(user.lastname)
        return fail('no-name')
    }
    
    type User = {firstname: string, lastname?: string}
    
    const getUserResult = ():Result<User, 'no-user'> => unit(({firstname: "John"})) //fail('no-user')
    const formatName = (u: User): Result<string, 'no-name'> => {
        if (u.firstname && u.lastname) return unit(`${u.firstname} ${u.lastname}`)
        if(u.firstname) return unit(u.firstname)
        if(u.lastname) return unit(u.lastname)
        return failed('no-name')
    }
    
    const toUpper = (u: string): Result<string, 'Strange issue'> => {
        return unit(u.toUpperCase())
    }
    
    interface fun<a, l> {
        (a: a): l
    }

    const applicate = <a,b,c,d>(f:fun<a, Result<c, d>>) => (r: Result<a,b>) => r.kind === "success" ? f(r.value) : r
    
    
    
    const railRoad = <succ1, errors>(r: Result<succ1, errors>) => ({
        get: () => r,
        then: <succ2, errors2>(f:fun<succ1, Result<succ2, errors2>>) => railRoad(applicate(f)(r))
    })
    const formatName2 = (u: User): Result<string, 'no-name'> => {
        return failed('no-name')
    }
    console.log(railRoad(getUserResult()).then(formatName2).then(toUpper).get())


## Credits

    https://talesfrom.dev/blog/many-faces-of-ddd-aggregates-in-fsharp


https://imhoff.blog/posts/using-results-in-typescript
