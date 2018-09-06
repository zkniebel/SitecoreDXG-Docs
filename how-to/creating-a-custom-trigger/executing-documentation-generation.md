# Executing Documentation Generation

In order to generate documentation, you need to call the `generateDocumentation` function of the `generation` module.

The function has the following syntax:

```
generation.generateDocumentation(
  Object data,        // the parsed JSON data response received from the serializer
  Fn successCallback, // callback to be executed on successful generation
  Fn errorCallback,   // callback to be executed on generation error
);
```

Following this syntax, the below can be used to execute documentation generation:

```js
generation.generateDocumentation(
  data,
  function (targetArchiveFilePath, targetArchiveFileName, targetFolderPath, targetHtmlDocFolderPath, targetMdjFilePath) {
    ...your logic to run on success...
  },
  function (error) {
    ...your logic to run on error...
  }
);
```



