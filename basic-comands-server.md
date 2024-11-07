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
## Create an user

```
npm install @types/bcrypt --save-dev
```
```
async userRegister(req:Request,res:Response){
        try {
            const {
                name,
                surname,
                password,
                email
            }=req.body

            let newUser={
                name,
                surname,
                password,
                email
            }
            
            const userData=await User.findOne({
                name:newUser.name,
                email:newUser.email
            })
            if (userData) {
                res.status(200).send({
                    message:"The user was registered"
                })
            }
            const hashes=bcrypt.hashSync(newUser.password,10)
            newUser.password=hashes

            const dataResponse = new User(newUser)
            await dataResponse.save()
            
            res.send({
                status:200,
                message:"User registerd succesfull",
                dataResponse
            })
        } catch (error) {
            res.send({
                status:400,
                message:"Process failed",
                
            })
        }        
     }
```
## Create token

```
import jwt from "jwt-simple";
import moment from "moment"

const SECRET_KEY = "SPUTNIK_DEVELOPER"
export interface UserToken {
    _id:string,
    name:string,
    surname:string,
    email:string,
    role:string,
    image:string,
    iat?:number,
    ex?:number
}
const createToken =(user:UserToken)=>{
    const payload ={
        id:user._id,
        name:user.name,
        surname:user.surname,
    
        email:user.email,
        role:user.role,
        image:user.image,
        iat:moment().unix(),
        ex:moment().add(30,"days").unix
    }
    return jwt.encode(payload,SECRET_KEY)
}
export default{
    createToken,
    
}

```
## Create login

```
async userLogin(req:Request,res:Response){
        try {
            const{
                name
            }=req.body

            const userData=await User.findOne({name:name})
            if (!userData) {
                res.send({
                    status:false,
                    message:"User not found"
                })
                return
            }
            const userDataToken: UserToken={
                _id:userData.id,
                name:userData.name,
                surname:userData.surname,
                email:userData.email,
                role:userData.role,
                image:userData.image,
                
            }
            
            const jwtData=jwt.createToken(userDataToken)
            res.send({
                status:true,
                success:"succesfull",
                user:userData,
                token:jwtData
            })
        } catch (error) {
            res.status(400).send({
                status:false,
                message:"Error ",
                error
            })
        }
     }
     ```


