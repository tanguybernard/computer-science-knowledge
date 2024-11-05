# NodeJS

## nvm install

https://dev.to/kasuken/install-node-version-manager-nvm-without-admin-rights-194f

nvm proxy http://mon-proxy:3131

nvm install v18.18.0



## Event loop

L’event loop permet de lire chaque ligne de code, de l’interpréter, et d’en créer un événement à faire exécuter par le thread. 

L'opération est placé dans la "call stack", la boucle d'évenement vient lire l'opération et l'execute. L'opération alors executé dans le pool de thread, le resultat (le callback) est alors placé dans la "callback queue" qui sera lu par l'event loop est lu pour retourner un resultat ou alors traiter de nouveau une opération asynchrone avec un nouveau callback.

https://dev.to/nodedoctors/an-animated-guide-to-nodejs-event-loop-3g62

https://www.jsv9000.app/?code=c2V0VGltZW91dChmdW5jdGlvbiBhKCkgeyBjb25zb2xlLmxvZygnTWFjcm8gVGFzaycpIH0sIDApOwoKUHJvbWlzZS5yZXNvbHZlKCkKLnRoZW4oZnVuY3Rpb24gYigpIHsgY29uc29sZS5sb2coJ01pY3JvIHRhc2snKSB9KTsKCmNvbnNvbGUubG9nKCdZbycpOw%3D%3D


## Streaming example


    import { pipeline } from 'node:stream/promises';
    import fs from 'node:fs';
    
    // URL du fichier à télécharger
    const fileUrl = 'https://placehold.co/600x400/000000/FFFFFF/png';
    
    // Nom du fichier de destination
    const destinationFilePath = 'image.png';
    
    fetch(fileUrl)
      .then(
        res =>
          new Promise(async (resolve, reject) => {
            for await (const chunk of res.body) {
              console.log("chunk")
              console.log(chunk)
            }
            const dest = fs.createWriteStream(destinationFilePath);
            pipeline(res.body, dest)
          })
      )
      .then(x => console.log(x));
