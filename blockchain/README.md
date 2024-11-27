# Blockhain Information

## Bloc

Un bloc est un enregistrement dans la blockchain qui contient et confirme plusieurs transactions en attente. Toutes les 10 minutes, en moyenne, un nouveau bloc contenant des transactions est ajouté à la chaine de blocs par le minage.

## Hash

Un hash est un nombre souvent hexadécimal calculé à partir d’une donnée. Il représente en quelque sorte une empreinte digitale servant à identifier rapidement la donnée initiale.

## Transaction Hash

Un ID de transaction (TxID), ou hash de transaction, est une chaîne de caractères unique attribuée à chaque transaction qui est vérifiée et ajoutée à la blockchain. En d'autres termes, un TxID est un numéro d'identification de chaque transaction sur la blockchain.


## Ancrage

Le terme utilisé pour décrire l’enregistrement d’une donnée sur la Blockchain est l’Ancrage (anchoring). Une donnée ancrée est repérée par un identifiant indiquant le numéro du bloc (dans la chaine) dans lequel elle se situe. L'Ancrage permet une vérification de la Preuve de façon autonome.

## Consensus

Le mécanisme de consensus d'une blockchain permet au réseau de se mettre d'accord sur une version unique de l'histoire. 
L'historique dans le cas d'une blockchain de type cryptomonnaie est l'ordre dans lequel les transactions ont eu lieu 
sur le réseau.

### Proof of Work : Compétition pour trouver un hash
### Proof of Stake

La preuve d'enjeu, preuve de participation ou preuve d’intérêt (en anglais : proof of stake, PoS) est une méthode par laquelle une chaîne de blocs d'une crypto-monnaie vise à atteindre un consensus distribué.  La preuve d'enjeu demande à l'utilisateur de prouver la possession d'une certaine quantité de crypto-monnaie (leur « participation » dans la crypto-monnaie) pour prétendre à pouvoir valider des blocs supplémentaires dans la chaîne de bloc et de pouvoir toucher la récompense, s'il y en a une, à l'addition de ces blocs. 

### Proof of Authority

Le Proof of Authority (PoA) est un algorithme de consensus basé sur la réputation.

Il y a un nombre limité de validateurs de blocs.




### Notes

Ethereum 2.0

Le changement de consensus à venir sur Ethereum va profondément modifier son mode de fonctionnement. 
Actuellement en Proof-of-Work, le protocole va évoluer vers du Proof-of-Stake et ainsi envoyer au tapis les mineurs. 
Petit coup de projecteur sur l’avenir des mineurs d’Ethereum !

## Halving

Un halving, également connu sous le nom de réduction de moitié, est un événement qui se produit tous les 210 000 blocs (environ tous les 4 ans) pour la blockchain Bitcoin (BTC). Lors d'un halving, la récompense en BTC décernée lors du minage de chaque bloc est divisée par 2.

L'objectif principal de cette réduction de moitié est de maintenir l'inflation sous contrôle en réduisant la quantité de bitcoins qui sont créés au fil du temps. Cet événement étant périodique et connu, il ne relève en rien de l'aléatoire.
## Smart Contract 

## Abi

### Initialisation

L’ABI d’un contrat Ethereum, « Application Binary Interface », Interface Binaire d’Application, est une représentation au format JSON de toutes les fonctions d’un Smart Contract. 

Cela permet notamment à web3.js, de faire communiquer une page web avec la blockchain Ethereum.

Smart Contract:

  pragma solidity 0.5;

  contract message {

      string lemessage;

      constructor() public {
      }

      function definirMessage(string memory  _nouveaumessage) public {
         lemessage = _nouveaumessage;
      }

      function voirMessage() public view returns (string memory  ){  
          return lemessage;
      }
  }


Après compilation, l'abi :

    [
        {
            "constant": false,
            "inputs": [
                {
                    "name": "_nouveaumessage",
                    "type": "string"
                }
            ],
            "name": "definirMessage",
            "outputs": [],
            "payable": false,
            "stateMutability": "nonpayable",
            "type": "function"
        },
        {
            "inputs": [],
            "payable": false,
            "stateMutability": "nonpayable",
            "type": "constructor"
        },
        {
            "constant": true,
            "inputs": [],
            "name": "voirMessage",
            "outputs": [
                {
                    "name": "",
                    "type": "string"
                }
            ],
            "payable": false,
            "stateMutability": "view",
            "type": "function"
        }
    ]

https://www.une-blockchain.fr/retrouver-labi-dun-contrat-ethereum/


### Utilisation

    //déclaration du provider 
    let web3 = new Web3(new Web3.providers.WebsocketProvider("myProvider"));

    let messageABI = //json;
    let web3js = new Web3(web3.currentProvider);
    let MessagesContract = web3.eth.contract(messageABI);
    let Message = MessagesContract.at("0x72c17c6e483febf50fd9099ea0f48532128ffc38");

    Message.voirMessage(function(error, result){
     if(!error){
       console.log(result);
       }
    else
      console.error(error);
    });
  
  https://www.une-blockchain.fr/une-page-web-qui-communique-avec-ethereum-grace-a-web3-js/
  
  
  ## Solidity
  
  ### Type
  
  uint8 c'est entre 0 et 255
  
  Déclarer une variable public, accessible en lecture seule aux autres contracts.
      
      public uint maVariable = 16;
 
 ## Blockchain Privé
 
 ### Hyperledger
 
Hyperledger est une blockchain privée (ou de consortium) open source soutenue par la Fondation Linux.



## Info

Bitcoin peut-il être à la fois sécurisé et scalable ? Le CTO de Ledger nous réponds !

https://www.youtube.com/watch?v=uZpsX3LCRi8&t=1583s


Layer 2

https://ethereum.org/fr/layer-2/



Protocole

https://www.quantmetry.com/blog/blockchain-fonctionnement-du-protocole/


Nonce :

https://www.investopedia.com/terms/n/nonce.asp


Proof of work

https://coincentral.com/what-is-a-nonce-proof-of-work/
