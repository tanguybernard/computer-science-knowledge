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

### Insert

    db.samlDocument.insertOne({active: true,organizationCode: "TEST", registrationId: "test", metadataLocation:"url", entityId:"test", idpWebSsoUrl:null});


### Update

    db.Employee.update({"Employeeid" : 1},{$set: { "EmployeeName" : "NewMartin"}});
    
    db.documentDocument.update({"organizationCode" : "TEST", "code": "93896"},{$set: { "effectiveDate" : new ISODate("2020-09-08T00:00:00Z")}})
    
