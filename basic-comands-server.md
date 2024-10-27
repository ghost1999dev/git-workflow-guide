## Start a project in NodeJS

```
npm init -y

```
## Required modules

```
npm i express morgan swagger-jsdoc swagger-ui-express cors mongoose mongoose-pagination multer moment validator bcrypt-nodejs jwt-simple 

```
## Start with typescript 

```

npm i -D typescript ts-node nodemon @types/cors @types/express @types/morgan @types/swagger-jsdoc @types/swagger-ui-express

npx tsc --init 

outDir
rootDir

```

## Create a nodemon field

```
    nodemon.json
    {
        "watch":[
            "src"
        ],
        "ext":"ts,json"
        "exec": "ts node ./src/index.ts"
    }

```

## Run the project 

```
 "build":"tsc",
 "start":"node build/index.js",
 "dev":"nodemon"

```

## app.ts

``` 

const app = express()
app.set('port', process.env.PORT || 3000)
app.use(cors())
app.use(morgan('dev'))
app.use(express.json())


export default app

```

## index.ts

```
import app from './app'
app.listen(app.get('port'))
console.log('Server listening in port ')

```
