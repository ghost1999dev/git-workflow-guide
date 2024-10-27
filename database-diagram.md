
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