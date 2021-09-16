# General Code Formatting

These are some general code formatting that is applicable for all code, languages or frameworks.

## Indentation

Use 4 space (not tabs) to indent any sort of file. For example, TypeScript, JavaScript, Java, Groovy, HTML etc. The 
default formatting provided by IntelliJ IDEA uses the 4 spaces.

Exceptions-

1. Dart files

Configure your IDE and `.editorconfig` (if present) to use 4 space indentation.

## Negating the nested if conditions

```groovy
// Avoid/wrong
Device addDevice(JSONObject deviceJson, App app, User user) {
    if (deviceJson) {
        if (deviceJson.name) {
            Device device = new Device(deviceJson)
            device.app = app
            device.user = user
            device.os = deviceJson.os == OperatingSystem.ANDROID.toString() ? OperatingSystem.ANDROID : OperatingSystem.IOS
            device.save(flush: true, failOnError: true)
       } else {
            log.debug "Name is unavailable"
       }
    }
}
```

The above approach reduces the readability.

```groovy
// Write approach
Device addDevice(JSONObject deviceJson, App app, User user) {
    if (!deviceJson) {
        log.debug "Device data is not available"
        return null
    }

    if (!deviceJson.name) {
        log.debug "Name is unavailable"
        return null
    }

    Device device = new Device(deviceJson)
    device.app = app
    device.user = user
    device.os = deviceJson.os == OperatingSystem.ANDROID.toString() ? OperatingSystem.ANDROID : OperatingSystem.IOS
    device.save(failOnError: true)
    return device
}
```

## Using any local references

Your code must not use any text that is local to user's system. For example,

```diff
-File tempDirectory = new File("/user/john/.tmp")
-sdk.dir=/Applications/Unity/Hub/Editor/2019.4.29f1/PlaybackEngines/AndroidPlayer/SDK
-dbConnection = db.connect('localhost:2345/prod_db')
```

## Extra empty lines

Your code must not have empty lines. Make sure to use maximum of one empty line.

```diff

[slot=fixed] {
    width: 100%;
    height: 100%;
}
+
+
+
+
+ion-segment-button {
```