# Datebase-HW8-NoSQL-MongoDB

***Name: Thanathip Suwannakhot Student ID: 6310545981***

### 5) Create MongoDB database with following information
![image](https://user-images.githubusercontent.com/78087668/159250886-bbda62cf-b732-4a91-b202-4a2456f1ef23.png)
#### Create a Database
```js
use Database-HW8
```
#### Create a collection named Users 
![image](https://user-images.githubusercontent.com/78087668/159250307-a380f443-c752-4d98-ba11-da9c653b8cae.png)
```js
db.createCollection("Users")
```
![image](https://user-images.githubusercontent.com/78087668/159251184-89b92556-9e91-47be-958c-885bf8878ffe.png)
#### Insert data to Users collection
```js
db.Users.insertMany(
    [
        {"name":"Ramesh","subject":"maths","marks":87},
        {"name":"Ramesh","subject":"english","marks":59},
        {"name":"Ramesh","subject":"science","marks":77},
        {"name":"Rav","subject":"maths","marks":62},
        {"name":"Rav","subject":"english","marks":83},
        {"name":"Rav","subject":"science","marks":71},
        {"name":"Alison","subject":"maths","marks":84},
        {"name":"Alison","subject":"english","marks":82},
        {"name":"Alison","subject":"science","marks":86},
        {"name":"Steve","subject":"maths","marks":81},
        {"name":"Steve","subject":"english","marks":89},
        {"name":"Steve","subject":"science","marks":77},
        {"name":"Jan","subject":"english","marks":0,"reason":"absent"}
    ]
)
```
![image](https://user-images.githubusercontent.com/78087668/159254030-2573f891-c75c-415b-950a-60cd77720930.png)
-----
### Find the total marks for each student across all subjects.
```js
db.User.aggregate(
    [
        {
            $group: {
              _id: "$name",
              totalMark: {
                  $sum: "$marks"
              }
            }
        }
    ]
)
```
![image](https://user-images.githubusercontent.com/78087668/159254245-08fec31c-994b-4d43-ba88-c90a275ebbcd.png)

### Find the maximum marks scored in each subject.
```js
db.User.aggregate(
    [
        {
            $group: {
              _id: "$subject",
              maxMark: {
                  $max: "$marks"
              }
            }
        }
    ]
)
```
![image](https://user-images.githubusercontent.com/78087668/159254791-d9ed31e5-a66b-42c2-a623-e47def1b233b.png)

### Find the minimum marks scored by each student.
```js
db.User.aggregate(
    [
        {
            $group: {
              _id: "$name",
              minMark: {
                  $min: "$marks"
              }
            }
        }
    ]
)
```
![image](https://user-images.githubusercontent.com/78087668/159254893-7664062d-084a-4209-a293-7399f73b2f71.png)

### Find the top two subjects based on average marks.
```js
db.User.aggregate(
    [
        {
            $group: {
              _id: "$subject",
              averageMark: {
                  $avg: "$marks"
              }
            }
        },
        {
            $sort: {
                averageMark: -1
            }
        },
        {
            $limit: 2
        }
    ]
)
```
![image](https://user-images.githubusercontent.com/78087668/159255002-70b2288a-28d1-4cfc-a034-62b9d716deb0.png)

