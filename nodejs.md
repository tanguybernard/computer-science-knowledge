# NodeJS

## Event loop

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
