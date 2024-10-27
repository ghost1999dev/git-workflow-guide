
## Database diagram

```
Table user{
  id integer
  name string
  nick string
  password string 
  role string
  image string
  created_at string
}


Table publication{
  id integer
  text string
  file string
  created_at string
  user string
}

Table follows {
  id integer
  user integer
  followed integer
  created_at string
}

Ref: user.id < publication.user
Ref: user.id < follows.user
Ref: user.id < follows.followed

```

## Mongoose model

```

const {Schema, model}= require("mongoose")

const UserSchema = Schema({
  name:{
    type:String,
    required:true
  },
  surname:{
    type:String
  },
  nick:{
    type:String,
    required:true
  },
  email:{
    type:String,
    required:true
  },
  role:{
    type:String,
    default:"role_user"
  },
  image:{
    type:String,
    default:"default.png"
  },
  created_at:{
    type:Date,
    default:Date.now
  }
})

module.exports = model("User", UserSchema, "users")

```