# Best Practices for Groovy

## Avoid `def`

Avoid using `def` because it breaks the readability and usability of the code. For example: 

```groovy
def addUserProperties(JSONObject userPropertiesJson, App app, User user) {
    // some code
}
```

We can't say that what is being returned from here.
So adding return type to all the functions where return type is known or pre defined

## Passing the input parameters to closures

Passing the variable to closure explicitly so as to increase readability.

```groovy
userPropertiesJson.each { String key, String value -> 
    UserProperty userProperty = new UserProperty()
    userProperty.name = name
    userProperty.value = value
}
```

## Use of as operator

We can use the as operator to invoke the conversion.
eg:- 

```groovy
enum MyColors{
  BLUE(0), RED(1), WHITE(2)
}
String color = "BLUE"
// Now if you want it to convert to enum 


MyColor newColor = color as MyColor
```

