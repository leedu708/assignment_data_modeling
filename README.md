# assignment_data_modeling
Mmmmm.... dataaaaa....

*Include your ERM modeling "pseudocode" in the space below*

Basic

1.  You are building a free online learning platform which will be used by students who are exclusively online (but don't need to be logged in or kept track of). You offer many different courses, each with a title and description, and each course has multiple lessons which can be displayed. Lesson content consists of a title and body text. What are the Goals? Entities? Attributes, types and constraints? Relationships? Design the data model for this web app.

  - Goal:  allow students to find out course information and lesson plan for courses
  - Entities: courses, lessons
  - Attributes:
    - course:
      1. name, String 3-40 chars
      2. description, String 500chars max
    - lesson:
      1. title, String 3-40 chars
      2. body, String, no limit
      3. course ID, foreign key
  - Relationship: one course to many lessons, one-to-many

  - Course Table:
    1. ID, int
    2. name, string, 3-40 chars
    3. description, string, 500 chars max
    4. created_at, DateTime
    5. updated_at, DateTime

  - Lesson Table:
    1. ID, int
    2. title, string 3-40 chars
    3. body, string, no limit(>0 chars)
    4. created_at, DateTime
    5. updated_at, DateTime
    6. course_id, int

2.  You are building the profile page for a new User on your login site. You are already storing your User's username and email, but now you want to collect demographic information like City, State, Country, Age and Gender. Think -- how many profiles should a User have? How would you relate this to the User model? Design the data model for this web app.

  - Goal:  collect demographic information from users
  - Entities: user with only one profile, location
  - Atrributes:
    - User:
      1. username, String 3-15 chars
      2. email, String 5-50 chars
      3. age, int max 3 chars
      4. gender, 1 char (M or F)
      5. location
    - Location:
      1. city, String
      2. state, String
      3. country, String
      4. zip code, int, optional

  - Relationship:  many users to one location, one-to-many

  - User Table:
    1. ID, int
    2. username, String 3-15 chars
    3. email, String 5-50 chars
    4. age, int 1-3 chars
    5. gender, 1 char (M or F)
    6. location ID, int, foreign key
    7. created_at, DateTime
    8. updated_at, DateTime

  - Location Table:
    1. location ID, int
    2. city, String 3-30 chars
    3. state, String 3-30 chars
    4. country, string 3-30 chars
    5. zip code, int
    6. created_at, DateTime
    7. updated_at, DateTime


Intermediate

1. You want to build a message board like Hacker News. Users can post links. Other users can comment on these submissions or comment on the comments. How would you make sure a comment knows where in the hierarchy it lives? Design the data model for this web app.

  - Goal: build a message board where users can make posts, comment on posts, and comment on comments
  - Entities: user, post, comment
  Attributes:
    - Users:
      1. username
      2. email
    - Posts:
      1. title
      2. link to article
      3. comments
    - Comments:
      1. author
      2. body
      3. parent post ID
      4. parent comment ID

  - Relationships:
    - one user to many posts
    - one user to many comments
    - one post to many comments
    - one comment to many comments

  - User Table:
    1. username, String 3-15 chars, primary key
    2. email, string 5-50 chars
    3. created_at, DateTime
    4. updated_at, DateTime

  - Post Table:
    1. post ID, int, primary key
    2. title, string 1-50 chars
    3. link to article, string 1-100 chars
    4. username, string, foreign key
    5. created_at, DateTime
    6. updated_at, DateTime

  - Comment Table:
    1. author, string, foreign key
    2. created_at, DateTime
    3. updated_at, DateTime
    4. body, string < 750 chars
    5. post ID, foreign key
    6. parent comment ID, foreign key
    7. comment ID, primary key for other comments



Advanced

You want to build an e-commerce site like a very simplified Amazon.com. You'll need to keep track of products, users, orders, shipments and all the bits and pieces necessary to glue them all together. Design the data model for this web app.

  - Goal:  keep track of products, users, orders, shipments and create a model to glue them all together
  - Entities: user, product, order, shipment, credit card, address
  - Attributes:

    - User:
      1. username
      2. email
      3. credit card

    - Address:
      1. city
      2. state
      3. country
      4. zip code
      5. street number
      6. street
      7. apartment number if necessary

    - Credit card:
      1. credit card number
      2. name on card
      3. expiration date
      4. ccv
      5. billing address

    - Product:
      1. name
      2. price
      3. product ID

    Order:
      1. order number
      2. shipping address

    Shipping:
      1. order number
      2. pack date
      3. ship date
      4. delivery date

  - Relationships:

    User to Address:  many to many (different family members at same address)

    Credit Card to Address: one address to many credit cards

    User to Credit card: one user to many credit cards

    Product to Order:  many to many

    Shipping to Order:  one order to one shipment

    Order to Address:  one address to many orders

    Order to User:  one user to many orders

    Order to credit card:  one credit card to many orders

  - User Table:
    1. username, string 3-15 chars, primary key
    2. email, string 5-50 chars

  - Address Table: 
    1. city, string 3-30 chars
    2. state, string 2-30 chars
    3. country, string 3-30 chars
    4. zip code, int
    5. street number, int
    6. street name, string, up to 30 chars
    7. apt number, string (e.g. 3A) max 5 chars
    8. Address ID, int, primary key

      - User to Address Table:
        1. username, string, foreign key
        2. address ID, foreign key

  - CC Table:
    1. cc ID, int, primary key
    2. cc number, int
    3. name on card, String 5-50 chars
    4. expiration date, DATE(MM/YY)
    5. ccv, int 3-4 digits
    6. address ID, foreign key

  - Product Table:
    1. name, string 5-50 chars
    2. price, float
    3. product ID, primary key

  - Order Table
    1. order number, int, primary key
    2. cc number, int foreign key
    3. username, string, foreign key
    4. address ID, int, foreign key

      - Order to Products Table:
          1. order number, int, foreign key
          2. product ID, int, foreign key

  - Shipment Table:
    1. order number, int, foreign key
    2. pack date, DateTime
    3. ship date, DateTime
    4. delivery date, DateTime