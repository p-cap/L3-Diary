# Revisit My ExpressJS Endpoint 

## Generate sample data 
```>>> mongo localhost:27017/appdb data.js ```

### Data.js
```
// Connect to MongoDB
conn = new Mongo();
// Create a database instance
db = conn.getDB("appdb");

db.apps.insertMany([
{"AppName":"Mat Lam Tam","FileName":"ElementumPellentesqueQuisque.mp3","Sha1":"b3a51cecd0187e8575e762c65bd058ae6b4386f1"},
{"AppName":"Tresom","FileName":"LiberoNonMattis.mp3","Sha1":"8c679f8aed2700f5c01e86a7fa94a3984fa2758a"},
{"AppName":"It","FileName":"Aliquam.txt","Sha1":"55c2a6e0bed1d3165f9538ef413c262d35a9ce21"},
{"AppName":"Stringtough","FileName":"CumSociisNatoque.gif","Sha1":"f655ce0eb4edf875b39045a56d71a7fd972c86ba"},
{"AppName":"Konklux","FileName":"SapienVarius.mp3","Sha1":"7475c403d77dfd7f34938951d09f20c6a80c2655"},
{"AppName":"Tin","FileName":"AtTurpisA.tiff","Sha1":"9e161975c44eebe78cd891a421cf123326b3bcee"},
{"AppName":"Solarbreeze","FileName":"PellentesqueUltricesPhasellus.xls","Sha1":"09f998d8a26b54250dab75afe0022e2928facf85"},
{"AppName":"Stronghold","FileName":"DictumstMorbiVestibulum.ppt","Sha1":"92fb957f605e31bc9e5bf2ced6eee123f9a9374e"},
{"AppName":"Aerified","FileName":"DuisBibendumFelis.tiff","Sha1":"d29b6bc34135da382c11c12f86903dcc3dd5d126"},
{"AppName":"Subin","FileName":"OdioElementum.mov","Sha1":"e2e4eee7cc642a41186e6de9ed75dda11f886d25"}
])
```

NOTE: Even if the database does not exits, the script will generate the DB.  

## Model => Apps.js ... made some changes to the Schema 
```
const mongoose = require('mongoose')
const Schema = mongoose.Schema

const AppsSchema = new Schema ({
    AppName: {
        type: String,
        required: true
    },
    FileName: {
        type: String,
        required: true
    },
    Sha1: {
        type: String,
        required: true
    }
})

// 'app' is the name of the collection 
const Apps = mongoose.model('app', AppsSchema)

module.exports = Apps
```
## Routes => routes.js
```
const AppsController = require('../controllers/AppsController')

module.exports = (app) => {
    app.get('/', AppsController.greeting)

    app.get('/apps', AppsController.read)

    app.post('/add', AppsController.create)

    app.put('/update/:appName', AppsController.edit)

    app.delete('/delete/:appName', AppsController.delete)

}
```

## AppsController => made major changes to the app controller
```
const Apps = require('../models/Apps')

module.exports = {
    greeting(req, res) {
        res.send("Welcome to Pcap's World")
    },

    read(req, res, next) {
        Apps.find()
        .then(Apps => res.send(Apps))
        .catch(next)
    },

    create(req, res, next) {
        const AppsProps = req.body

        Apps.create(AppsProps)
        .then(Apps => res.send(Apps))
        .catch(next)
     },

     edit(req, res, next) {
         const AppsName = req.params.appName
         const AppsProps = { 
             FileName: req.body.FileName,
             Sha1: req.body.Sha1
         }

         Apps.updateMany({ AppName: AppsName }, 
            { FileName: AppsProps.FileName, Sha1: AppsProps.Sha1 })
         .then( Apps => res.send(Apps))
         .catch(next)
        },

     delete(req, res, next) {
        const AppsName = req.params.appName

        Apps.deleteMany( { AppName : AppsName } ) 
        .then(Apps => res.status(204).send(`${Apps.appName} was successfull deleted`))
     }     
}
```

## App.js => Contained the connection to the mongodb server, middleware for parsing http body requests and error handling
```
const express = require('express')
const routes = require('./routes/routes')
const app = express()
const mongoose = require('mongoose')
const bodyParser = require('body-parser')
// var cors = require('cors')


// connect to mongodb database
mongoose.Promise = global.Promise
mongoose.connect('mongodb://localhost/appdb', {
    useNewUrlParser: true,  
    useUnifiedTopology: true, 
    useUnifiedTopology: true 
})

// app.use(cors)
app.use(bodyParser.json())
routes(app)

// creating our middleware that catches mostly the errors
app.use((err, req, res, next) => {
    res.status(422).send({ error: err.message })
})

module.exports = app
```

## Make sure I use the command below to start server
``` npm run pcap ```

# Curl commands for testing
```
# GET Request
curl -G http://localhost:5555/apps 

# POST Request
curl -d '{"AppName":"test","FileName":"test.mp3","Sha1":"test"}' -H 'Content-Type: application/json' http://localhost:5555/add

# PUT Request
curl -X PUT -d '{"FileName":"pcap","Sha1":"pcap Success"}'  -H 'Content-Type: application/json' http://localhost:5555/update/test

# DELETE Request
curl -X "DELETE" http://localhost:5555/delete/test
```
### Note: I will make this more extensible so I can apply optional paramaters

