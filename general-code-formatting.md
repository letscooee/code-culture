# General Code Formatting

This is a general code formatting we follow at [Wiz Panda](https://wizpanda.com/).

## Indentation

Use 4 space (not tabs) to indent any sort of file. For example, TypeScript, JavaScript, Java, Groovy, HTML etc. The default formatting
provided by IntelliJ IDEA uses the 4 spaces.

## Spacing

These spacing rules are applicable to all code like TypeScript, Java or Groovy.

```javascript
// Wrong
if("foo" !== "bar"){
}

// Right
if ("foo" !== "bar") {
}
```

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

## Variable declaration priority

As a general standard, private constants & static variables should come first in a class.




