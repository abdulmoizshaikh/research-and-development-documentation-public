# Postman

## how to do inherit auth from parent postman

Inheriting Auth Details | Postman Level Up

https://www.youtube.com/watch?v=WFiYsfSkyXE&ab_channel=Postman

**setting env variable automatically after login response**

add this below code in test tab in postman

```jsx showLineNumbers
var jsonData = JSON.parse(responseBody);
postman.setEnvironmentVariable(""tokenDev"", `Bearer ${jsonData.data.token}`);
console.log(""new tokenDev"",pm.environment.get(""tokenDev"")) "
```

**how to export all collection from postman**

Data export requested
they will send you exported data link in email
You will be notified via email when the export is ready for download.

https://stackoverflow.com/questions/57747235/export-all-collections-in-postman

**How to set a postman environment variable's value to another variable's?**

"VARIABLE | INITIAL VALUE | CURRENT VALUE
Red | | #ff0000
Default | | {{Red}}"

https://stackoverflow.com/questions/63996859/how-to-set-a-postman-environment-variables-value-to-another-variables
