**Author**: [@shiryz](https://github.com/shiryz)  

**Maintainer**: [@shiryz](https://github.com/shiryz)  

## Databases morning challenge

The purpose of this challenge is to construct complicated queries, learn about joins and use some subqueries.

#### 5-minute setup:
- Clone / fork this repo.
- cd into the repo in your command line `$ cd db-morning-challenge`
- Install dependencies with `$ npm install`
- Create an app on Heroku `heroku create app-name-here --region eu` (If you haven't yet installed Heroku CLI see [here](https://devcenter.heroku.com/articles/heroku-cli)
- Push to Heroku `git push heroku master`
- Create a new database on Heroku: `heroku addons:create heroku-postgresql:hobby-dev`
(You can also create the database with as alias `heroku addons:create heroku-postgresql:hobby-dev --as USERS_DB`)
- Find the database url, either on the heroku dashboard for your project, under settings (click reveal config vars), or by using `heroku config -s | grep USERS_DB`
- Back in your command line, create a config.env file with the url of your new database. You can do that like this
  `$ echo "export DB_URL = {YOUR_COPIED_DATABASE_URL}" >> "config.env"`
- Build your database by running: `$ node database/db_build.js`

You're done!

#### Using Heroku databases

Access your database from the command line with `psql {YOUR_COPIED_DATABASE_URL}`

For each of the challenges below, write and test your queries in the command line and save them in a text editor when you're happy with them, so you can refer back to them later.

#### Challenge 1

One of the tables you have created is a books table that looks like this:

| book_id | book_name | year | max_reservation_time | library |
| ------- | --------- | ---- | -------------------- | ------- |

your challenge is to construct a query that returns the following columns:
* `book_id`,
* `book_name`,
* `max_reservation_time`

**AND** to return only the books that can be reserved for a time greater than the **average** reservation time for all books at the library *this* book is in.

*Hint: try using sub queries*

You should expect to see this:

| book_id | book_name                                | max_reservation_time |
|---------|------------------------------------------|----------------------|
| 1       | Javascript: The Good Parts               | 21                   |
| 5       | Pride and Prejudice                      | 21                   |


#### Challenge 2:

Your database contains 3 more tables:

**Mentors**
For storing details of FAC mentors.

| name | location |
| ---- |--------- |

**Posts**
For things that have been posted by mentors:

| num | mentor_name |
| --- |------------ |

**Likes**
For the likes posts have received, and the *person who liked it*

| mentor_name | post_num |
| ----------- |--------- |

**The challenge:**
- Construct a query that returns the names of mentors and the number of likes each mentor got, in total, for all their posts.

  You should expect to see this:

| mentor_name | count |
|-------------|-------|
| Shireen     | 9     |
| Tom         | 4     |
| Steve       | 4     |

- Construct a query that returns the location and the post number, for posts that
  have been liked by a mentor from that location.

  You should expect to see this:

| location | post_num |
|----------|----------|
| Nazareth | 20       |
| Nazareth | 44       |
| Nazareth | 19       |
| Nazareth | 57       |
| Nazareth | 32       |
| Nazareth | 20       |
| Nazareth | 19       |
| Nazareth | 44       |
| Nazareth | 20       |
| Nazareth | 19       |
| London   | 19       |
| London   | 57       |
| London   | 32       |
| London   | 44       |
| London   | 32       |
| London   | 44       |
| London   | 20       |

#### Challenge 3 (bonus, you can try this one at home!)

Building on the queries you wrote in level 2, construct another query that returns the **average number of likes per post** in each location.

You should expect to see this:

| location | avg |
|----------|-----|
| Location | 4   |
| Nazareth | 3   |
