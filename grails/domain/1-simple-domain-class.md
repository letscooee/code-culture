# Best Practice 1: A Simple Domain Class

```groovy
package com.letscooee.foo.user

import grails.compiler.GrailsCompileStatic
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
        // Plain password will be encrypted so keeping higher maxSize
        password blank: false, maxSize: 100
    }

    boolean enabled = true

    String email
    String mobile
    String fullName
    String password
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
| mobile       | varchar(10)  | NO   | UNI | NULL    |                |
| first_name   | varchar(50)  | NO   |     | NULL    |                |
| password     | varchar(100) | NO   |     | NULL    |                |
| enabled      | bit(1)       | NO   |     | NULL    |                |
| email        | varchar(50)  | NO   | UNI | NULL    |                |
+--------------+--------------+------+-----+---------+----------------+
```

The following are the explanation line by line:

1. Every domain classes must be in a good package to start. They should start with `com.letscooee.app-name`. For example, a user related
 domain should be in a package `com.letscooee.foo.user`.
2. Domain classes must have Javadoc to explain the usage of the domain entity.
3. Every domain class must have a `@ToString` annotation which must print the `id` and any other required field. If you do not add
 `@ToString` or do not override the `String toString()` method, those gets printed something like this: `com.letscooee.foo.user.User(id: 11)`.
4. Every domain classes must have `@GrailsCompileStatic` (unless explicitly discussed to skip). This helps in performance.
5. The `constraints`, `mapping` & `belongsTo` should come before the declaration of fields.
6. The constraints need to think & applied for every single field. For example,
    1. The name of a user can't be blank and must be minimum of 2 characters and can't go beyond 50 characters (by default MySQL maps a
     `String` field with 255 characters which is a waste of memory in DB).
    2. The mobile number (especially in India) needs to be exact 10 characters, and it must be unique.
    3. The email of a user can't go beyond 50 characters, and it can't be duplicated.
    4. Since the password will be hashed/encrypted, it's size must be at least 100 characters.
7. All the fields must follow the camelCase character and shouldn't use shortcut names. For example, `fullName` instead of `fn`.
