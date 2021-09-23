# Best Practice 3: Use of version field

You must have noticed in the simple example table that there is a `version` column in the mapped `user` table. 

```mysql based
mysql> desc user;
+--------------+--------------+------+-----+---------+----------------+
| Field        | Type         | Null | Key | Default | Extra          |
+--------------+--------------+------+-----+---------+----------------+
| id           | bigint(20)   | NO   | PRI | NULL    | auto_increment |
| version      | bigint(20)   | NO   |     | NULL    |                |
| first_name   | varchar(50)  | NO   |     | NULL    |                |
| email        | varchar(50)  | NO   | UNI | NULL    |                |
+--------------+--------------+------+-----+---------+----------------+
```

This is the concept of [Optimistic Locking](http://gorm.grails.org/7.0.x/hibernate/manual/#_optimistic_locking). To read-

> By default, GORM classes are configured for optimistic locking. Optimistic locking is a feature of Hibernate which involves storing a
> version value in a special version column in the database that is incremented after each update.

> The version column gets read into a version property that contains the current versioned state of persistent instance which you can
> access.

Hibernate automatically bumps this version every time you save your domain instance and this is useful as it allows a certain level of
 atomicity.

Although, we do not require this `version` property sometimes in our domain classes. A possible scenarios:

1. When the domain classes will never update. For example,
    1. `UserEvent` which is logged only once.
    2. `BankTransaction` which will never be updated.
    3. `Category` of a ecommerce product which will never be updated.
2. When we decide not to keep that version field because that is not needed in a particular table of a particular field. For example,
    1. We do not care that how many times a `User` profile was updated.
    2. We do not care that how many times a `Category` record was updated.
    
In these scenarios, we should turn off the `version` field which can save one column in the database. To do that, add the following-

```groovy
static mapping = {
    version false
}
```

**PLEASE NOTE:** This is totally a decision based practice which can be decided by the team if version is required or not. 
