# Using the DocumentationConfiguration Object

SitecoreDXG supports being passed a `DocumentationConfiguration` object as a property of the JSON object stored in the [`OPTIONS_FILE_PATH`](./) passed to the middleman. This object allows users to add extra information to the documentation that they plan to generate. 

By default, this object supports the following properties:

1. `DocumentationTitle`
2. `CommitAuthor`
3. `CommitHash`
4. `CommitLink`
5. `DeployLink`
6. `ProjectName`
7. `EnvironmentName`

An example `DocumenationConfiguration` object is shown below:

```javascript
{
    "DocumentationConfiguration": {
        "DocumentationTitle": "Foo Corp Sitecore Solution Documentation",
        "ProjectName": "Foo Corp .COM",
        "EnvironmentName": "UAT",
        "CommitAuthor": "Zachary Kniebel",
        "CommitHash": "0FE1D344",
        "CommitLink": "http://mygit.com/repo/myrepo/commits/0FE1D344",
        "DeployLink": "http://mydocs.com/foo/bar"
    }
}
```

