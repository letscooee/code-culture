# Best Practices for Grails Domain Classes

## Flushing the session

It is not recommended to use `flush: true` while saving or updating a domain instance. For example: `userInstance.save(flush: true
)`. One should use the `flush: true` after understanding the consequences of it.

The major problem with using `flush: true` is that 
