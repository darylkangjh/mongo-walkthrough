<img src="https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png" style="margin: 0;">

Welcome darylkangjh,

This is the Code Institute student template for Gitpod. We have preinstalled all of the tools you need to get started. You can safely delete this README.md file, or change it for your own project.

## Gitpod Reminders

To run a frontend (HTML, CSS, Javascript only) application in Gitpod, in the terminal, type:

`python3 -m http.server`

A blue button should appear to click: *Make Public*,

Another blue button should appear to click: *Open Browser*.

To run a backend Python file, type `python3 app.py`, if your Python file is named `app.py` of course.

A blue button should appear to click: *Make Public*,

Another blue button should appear to click: *Open Browser*.

In Gitpod you have superuser security privileges by default. Therefore you do not need to use the `sudo` (superuser do) command in the bash terminal in any of the backend lessons.

## Updates Since The Instructional Video

We continually tweak and adjust this template to help give you the best experience. Here are the updates since the original video was made:

**April 16 2020:** The template now automatically installs MySQL instead of relying on the Gitpod MySQL image. The message about a Python linter not being installed has been dealt with, and the set-up files are now hidden in the Gitpod file explorer.

**April 13 2020:** Added the _Prettier_ code beautifier extension instead of the code formatter built-in to Gitpod.

**February 2020:** The initialisation files now _do not_ auto-delete. They will remain in your project. You can safely ignore them. They just make sure that your workspace is configured correctly each time you open it. It will also prevent the Gitpod configuration popup from appearing.

**December 2019:** Added Eventyret's Bootstrap 4 extension. Type `!bscdn` in a HTML file to add the Bootstrap boilerplate. Check out the <a href="https://github.com/Eventyret/vscode-bcdn" target="_blank">README.md file at the official repo</a> for more options.

--------

Happy coding!
# Important things to do when starting MONGODB

## 1. In console: type 'show databases'
## 2. In console: type 'use sample_airbnb
## 3. In console: type 'show collections'



## find by multipel criteria 

add the new criteria to the first argument to the `find` function 

To find listings with2 beds and 2 bedrooms: 

first object is criteria, second is projection 

db.listingsAndReviews.find({
    'beds':2,
    'bedrooms':2
}, {
    'name':1,
    'beds':1,
    'bedrooms':1
}).pretty().limits(10)




## find by a range or inequality 
we can use `$gt` or `$lt` to represent greather than or less than.

find listing with more than 3 beds

db.listingsAndReviews.find({
    'beds':{
        '$gt':3
    }
},{
    'name':1,
    'beds':1
}).pretty().limit(10)
---------------------------------------------
find listing with less than 3 beds

db.listingsAndReviews.find({
    'beds':{
        '$lt':3
    }
},{
    'name':1,
    'beds':1
}).pretty().limit(10)

---------------------------------------------

`$gte` is greater than or equal and `$lte` is lesser than or equal

db.listingsAndReviews.find({
    'beds':{
        '$gte':4
        '$lte'=8
    }
},{
    'beds':1,
    'name':1
}).pretty().limit(10)

let critera = {   
    'beds':{
        '$gte':4
        '$lte':6
    }, 
}

let projection = {
    'beds':1,
    'name':1,
    'bedrooms':1
}

db.listingsAndReviews.find(criteria,projection)



db.listingsAndReviews.find({
    'amenities':{
        '$all':['Washer','Dryer']
    }
}, 
{
    'name': 1,
    'ammneities': 1
}).pretty().limit(5)

## find listing that include 1 of the specific element in an array

db.listingsAndReviews.find({
    'amenities':{
        '$in':['TV','Cable TV']
    }
}, 
{
    'name': 1,
    'amenities': 1
}).pretty().limit(5)

## find all listings that are either in Canada or Brazil 
```
db.listingsAndReviews.find({
    'address.country':{
        '$in':['Brazil','Canada']
    }
}, {
    'name':1,
    'address.country':1
}).pretty()
```

## find all listings which have reviewed by Bart 
db.listingsAndReviews.find({
    'reviews':{
        '$elemMatch': {
            'reviewer_name':'Bart'
        }
    }
},{
    'name':1,
    'reviews':1
}).pretty().limit(5)

## Match by string 
something like `select * from customers where customerName like 

'$options':'i' means that it makes the query not case sensitive.

db.listingsAndReviews.find({
    'name':{
        '$regex':'Spacious', '$options':'i'
    }
},{
    'name':1
})

## count how many listings there are in total 

db.listingsAndReviews.find().count()

## show all listings that >= 15 amenitites
db.listingsAndReviews.find({
    'amenities.6':{
        '$exists':true
    }
},{
    'name':1, 'ammenities':1
}).pretty()

## compounds 'AND' or 'OR' or 'NOT' 

find all the listings in Brazil OR listings from canada that has more than 5 bedrooms 
db.listingsAndReviews.find({

    '$or':[
        {
            'address.country':'Brazil'
        },
        {
            'address.country':'Canada',
        }
    ]


},{

    'name':1,
    'bedrooms':1,
    'address.country':1

}).pretty()