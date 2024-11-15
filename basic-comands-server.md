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

## Create authentication

```
//Import modules
import jwt from "jwt-simple";
import moment from "moment"
import { Request,Response,NextFunction } from "express";
//Import secret key
import jwtService from "../services/jwt";
import { SECRET_KEY } from "../services/jwt";

//Authentication function
const auth=(req:Request & {user?:any},res:Response,next:NextFunction)=>{
    if (!req.headers.authorization) {
        res.status(403).send({
            status:false,
            message:"The request haven't the authentication header"
        })
        return
    }  
    try {
        let token = req.headers.authorization.replace(/['"]+/g, '')
        let payload = jwt.decode(token,SECRET_KEY)
        if (payload.ex <= moment().unix()) {
            res.status(401).send({
                status:false,
                message:"Token expired"
            })
            return
        }
        req.user=payload
        next()

    } catch (error) {
        res.status(404).send({
            status:false,
            message:"Invailable token",
            error
        })
    }

}
export default{
    auth
}
```
### Create getUserById , getAllUser, updateUser

```async getUserById(req:AuthenticateRequest,res:Response){
        try {
            const{id}=req.params
            const data = await User.findById(id)
            .select('-password -created_at -__v')
            res.send({
                status:true,
                message:"Private test",
                data
               
            })
        } catch (error) {
            res.status(404).send({
                status:false,
                message:"Error",
                error
            })
        }
     }
     async userList(req:Request,res:Response){
        try {
            const page =Number(req.params.page) || 1
            const limit =Number(req.params.limit) || 4
            const skip = (page - 1) * limit
            const data = await User.find().skip(skip).limit(limit).select('-password -created_at -__v')
            const totalDocuments = await User.countDocuments()
            //Division 
            const totalPages = Math.ceil(totalDocuments / limit)
            res.send({
                status:true,
                data,
                currentPage:page,
                totalPage:totalPages,
                totalDocuments:totalDocuments
            })
        } catch (error) {
            res.status(404).send({
                status:false,
                message:"Error",
                error
            })
        }
     }

     async updateUser(req:AuthenticateRequest,res:Response){
        try {
            const userIdentity = req.user
            const userBody = req.body  
            let condition = false
            const findData = await User.find({
                name:userBody.name,
                email:userBody.email
            })
            
            findData.forEach((element:any)=>{
                if (element._id !=userIdentity.id) {
                    condition=true 
                }
                
            })

            if (condition) {
                res.send({
                    status:true,
                    message:"The user already exist"
                })
                return
            }

            //Encrypt the password
            //Update user
            
            
            res.send({
                findData
            })
        } catch (error) {
            
        }
     }
     ```


