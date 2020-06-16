# Best Practices for Groovy

## Avoid `def`

Avoid using `def` because it breaks the readability and usability of the code. For example: 

```groovy
def addUserProperties(JSONObject userPropertiesJson, App app, User user) {
    // some code
}
```

We can't say that what is being returned from here.
