# Package.json | Terminal

**How to pass params from terminal to package.json**

https://stackoverflow.com/questions/11580961/sending-command-line-arguments-to-npm-script

For example, in your "scripts" JSON value, include--

```bash showLineNumbers
start: "node ./script.js server $PORT"
And then from the command-line:

$ PORT=8080 npm start
or
"create_migration": "sequelize migration:create --name=$name", name="add_experience_columns_in_employees" npm run create_migration
```

### project skeliton

1 use yarn as a package manager rather than npm

## Package.json / npm

1. Uninstalling packages and dependencies
   run this below command if you want to remove package from both node_modules and package.json
   don't forget to add --save flag at last

   ```bash showLineNumbers
   npm uninstall <package-name> --save
   e.g
   npm uninstall react-router-dom --save
   ```

   https://youtu.be/Z-BpYj6cSoQ
   https://docs.npmjs.com/uninstalling-packages-and-dependencies

2. npm check and update package if needed
   npm outdated
   npm update
3. command to update package to lastest wanted verison
   npm update <pacakge_name>
4. command to get outdated npm packages
   npm outdated
   https://www.carlrippon.com/upgrading-npm-dependencies/

## Yarn

use yarn over npm beacuse yarn is stable than npm (sometimes npm do problem in installing dependencies but yarn is champ)

How to Install Yarn on Ubuntu 20.04

https://linuxize.com/post/how-to-install-yarn-on-ubuntu-20-04/
