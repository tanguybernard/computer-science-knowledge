# NodeJS

## Event loop

L’event loop permet de lire chaque ligne de code, de l’interpréter, et d’en créer un événement à faire exécuter par le thread. 

L'opération est placé dans la "call stack", la boucle d'évenement vient lire l'opération et l'execute. L'opération si synchrone est executé, le resultat est retourné directement (ex: console.log). Si c'est asynchrone, le pool de thread vient traiter l'evenement est le resultat (le callback) est placé dans un "callback queue" qui sera lu par l'event loop est executé a son tour pour retourner un resultat ou alors traiter de nouveau une opération asynchrone avec un nouveau callback.

https://dev.to/nodedoctors/an-animated-guide-to-nodejs-event-loop-3g62


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
