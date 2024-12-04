# Mongo

## Command

### Connection

    mongo --username mongo --password mongo --authenticationDatabase adminDb

### List all databases

    show dbs

### Select DB

    use <tableName>
    
### Show tables

    show collections

### Checking if a field contains a string

    db.notifications.findOne({"title" : {$regex : ".*Riz.*"}});
    
### Count

    db.collection.count({"organizationCode": "TEST"})


### Display some fields :

Data :

    [
    ...
        {
            _id: UUID('a2816acb-7635-4129-b17d-96fa0aa3eab8'),
            num: '1938ccb188c',
            offers: [
              {
                _id: 1,
                type: 'standard',
                excludingTaxPriceByTiwatt: 83.33,
                percentTax: 20,
              }
          ]
        }
    ]

Command :

    db.orders.find({}, { "offers.excludingTaxPriceByTiwatt": 1, _id: 1 });

Reponse :

    [ 
      {
        _id: UUID('52614702-f874-4887-9bcd-afe4259c3861'),
        offers: [ { excludingTaxPriceByTiwatt: 83.33 } ]
      },
      {
        _id: UUID('b148cb27-cac7-499b-83a5-2d40a9a07579'),
        offers: [ { excludingTaxPriceByTiwatt: 83.33 } ]
      },
      ...
    ]


### Give me all "num" of orders if offers.excludingTaxPriceByTiwatt exists

    db.orders.find( { "offers.excludingTaxPriceByTiwatt": { $exists: false }}, {num: 1} )

### Insert

    db.samlDocument.insertOne({active: true,organizationCode: "TEST", registrationId: "test", metadataLocation:"url", entityId:"test", idpWebSsoUrl:null});


### Update

    db.Employee.update({"Employeeid" : 1},{$set: { "EmployeeName" : "NewMartin"}});
    
    db.documentDocument.update({"organizationCode" : "TEST", "code": "93896"},{$set: { "effectiveDate" : new ISODate("2020-09-08T00:00:00Z")}})
    
