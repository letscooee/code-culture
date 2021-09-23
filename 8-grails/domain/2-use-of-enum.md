# Best Practice 2: Use of Enums

## Use of plain Enums

`Enum` should be used whenever some values are fixed and constant. A very simple example is the gender of a user. It can have three
 values, `MALE`, `FEMALE` & `OTHER` (with utmost respect). 

So let's use enum in our previous example (removing some fields from the previous example for simplicity).

```groovy
package com.letscooee.foo.user

import grails.compiler.GrailsCompileStatic
import groovy.transform.CompileStatic
import groovy.transform.ToString

/**
 * A Grails domain entity which holds the basic information about a user who is
 * going to use the portal by logging in.
 *
 * @author Shashank Agrawal
 */
@ToString(includes = ["id", "email", "mobile"], includeNames = true, includePackage = false, cache = true)
@GrailsCompileStatic
class User {

    static constraints = {
        fullName blank: false, maxSize: 50, minSize: 2
        mobile blank: false, size: 10..10, unique: true
        email email: true, maxSize: 50, unique: true
        gender nullable: true
    }

    boolean enabled = true

    String email
    String mobile
    String fullName

    Gender gender
}

@CompileStatic
enum Gender {

    FEMALE,
    MALE,
    OTHER
}
```

This will be mapped as-

```mysql based
mysql> desc user;
+--------------+--------------+------+-----+---------+----------------+
| Field        | Type         | Null | Key | Default | Extra          |
+--------------+--------------+------+-----+---------+----------------+
| id           | bigint(20)   | NO   | PRI | NULL    | auto_increment |
| version      | bigint(20)   | NO   |     | NULL    |                |
| gender       | varchar(255) | YES  |     | NULL    |                |
| mobile       | varchar(10)  | NO   | UNI | NULL    |                |
| first_name   | varchar(50)  | NO   |     | NULL    |                |
| password     | varchar(100) | NO   |     | NULL    |                |
| enabled      | bit(1)       | NO   |     | NULL    |                |
| email        | varchar(50)  | NO   | UNI | NULL    |                |
+--------------+--------------+------+-----+---------+----------------+
```

1. We added an enum right there in the same domain class. This can also go in `src/main/groovy/com/letscooee/foo/user` 
   as a separate class.
2. `@CompileStatic` **MUST** be added for performance reason (read about the annotation).
3. We added the field in the domain.

Now when you run your application, you will see that Grails will create a column `gender` in `user` table which will be a `varchar(255)`
of MySQL. But the maximum characters required to store a gender is 6 (for `FEMALE`). So do this, we can add a `mapping` like- 

```groovy
    static mapping = {
        gender length: 6
    }
```

And the Grails will change the mapping to `varchar(6)` for `gender` column.

## Use of ids in Enum

In the above example, we achieve the enum and made it a string of 6 characters (for the database). But a string comparision/matching is
 always expensive (in terms of CPU & memory) so we should user numbers.

Grails/Hibernate can map an Enum to use a `id` if a field `id` is avaialble in the enum. So we can change our enum to-

```groovy
@CompileStatic
enum Gender {

    FEMALE((Byte) 1),
    MALE((Byte) 2),
    OTHER((Byte) 3)

    final Byte id

    Gender(Byte id) {
        this.id = id
    }
}
```

And add the following in mapping-

```groovy
    static mapping = {
        gender enumType: "identity"       // This will tell Hibernate to use the "id" attribute
    }
```

We are using `Byte` because we don't need more than 127 values (maximum value of `Byte`). This helps in following two ways-
 
1. Using reduced memory in JVM as we don't need a `Integer` when `Byte` is sufficient.
2. Small data type in Mysql. So Grails will map this as `tinyint` in MySQL. Read the mapping between Java data types to MySQL types here https://www.tutorialspoint.com/hibernate/hibernate_mapping_types.htm

Now when you will see it in DB-

```mysql based
mysql> desc user;
+--------------+--------------+------+-----+---------+----------------+
| Field        | Type         | Null | Key | Default | Extra          |
+--------------+--------------+------+-----+---------+----------------+
| id           | bigint(20)   | NO   | PRI | NULL    | auto_increment |
| version      | bigint(20)   | NO   |     | NULL    |                |
| gender       | tinyint(4)   | YES  |     | NULL    |                |
| mobile       | varchar(10)  | NO   | UNI | NULL    |                |
| first_name   | varchar(50)  | NO   |     | NULL    |                |
| password     | varchar(100) | NO   |     | NULL    |                |
| enabled      | bit(1)       | NO   |     | NULL    |                |
| email        | varchar(50)  | NO   | UNI | NULL    |                |
+--------------+--------------+------+-----+---------+----------------+
```
