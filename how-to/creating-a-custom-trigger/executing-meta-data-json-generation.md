# Executing Meta-Data JSON Generation

SitecoreDXG uses the same third-party libraries as StarUML - the UML IDE that SitecoreUML integrates with - for documentation generation. As part of the documentation generation process, SitecoreDXG first generates a new Meta-Data JSON file \(.MDJ extension\), which is effectively a project file for StarUML. However, sometimes you may want just the MDJ file and not the HTML documentation, especially considering that the MDJ file may only take a few seconds to generate for a very complex solution, whereas the HTML documentation may take several minutes. For this reason, SitecoreDXG includes the abiltiy to execute the MDJ file generation independently of the HTML documentation generation.

In order to generate just the Meta-Data JSON file, you need to call the `generateMetaDataJson` function of the `generation` module.

The function has the following syntax:

```text
generation.generateMetaDataJson(
  Object data,        // the parsed JSON data response received from the serializer
  Fn successCallback, // callback to be executed on successful generation
  Fn errorCallback,   // callback to be executed on generation error
);
```

Following this syntax, the below can be used to execute the Meta-Data JSON file generation:

```javascript
generation.generateMetaDataJson(
  data,
  function function (mdjPath, targetFileName, targetFolderPath, targetFilePath) {
    ...your logic to run on success...
  },
  function (error) {
    ...your logic to run on error...
  }
);
```

