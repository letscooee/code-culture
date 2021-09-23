# General HTML Standard

## 1. No inline styles

```diff
- <p style="position: absolute; bottom: 0;right:16px">
+ <p class="foo">

+ .foo {
+   position: absolute;
+   bottom: 0;
+   right: 16px
+}
```
