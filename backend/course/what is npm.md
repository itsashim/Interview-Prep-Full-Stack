Npm is default package manage for Javascript and typescript, It consists of vast online registry containing millions of reusable code and packages and CLI that allows developers to easily update, delete, install and manage the dependicies of their projects.


`npm init`
creates package.json, which is the configuration file of our project where all kinds of data about the current project is stored.

`npm outdated`
list all the outdated packages in your project

`npm install <package_name>@versionnumber`
installs that specific version of packages !if that you have the existing package with another varialbe it replaces it with new installed version

# Two types of packages that can be installed
- simple dependencies
- development dependencies :- our code doesn't need them we simply need them to develop our applications like: webpack, testing library etc, In production we don't need them. inorder to use the development dependencies we have to use the package by specifing the run script inside the scripts: {} in package.json and run in like: npm run <dependency_name>
   : npm install <package_name> --save-dev
- global installs: It will be installed globally in your system so that i can be used in any other project in your system.
: npm install <package_name> --global


# versioning, updating, deleting packages in npm

## versioning: major.minor.patch (1.1.11)  
    - patch number is at the end of the verisioning and is used by the developer to track and update bugs fixes
    - minor version number: This version introduces new features to the package but doesn't include breaking changes
    - major version number: For huge new release that can have breaking changes that our current version of our code might not work as well.

# versioning symbols

`^` : accept all the patch and minor releases
`~` : only accept patch releases
`*` : includes all the version, like patch, minor, major when we update, that can sometimes break our code 

## updating packages
- npm update <package_name>
    updates wated package version according the config symbols in the versioning, you can check the wanted version by : npm outdated 


## delete packages
- npm uninstall <package_name>
delete the package from the node_modules and also from package.json


# Node modules folder
- always ignore this folder because it's already tracked with package.json, 
- `npm i` will install node_modules


# package-lock.json
- we get all the version of our packages that includes dependencies of dependencies

always share package-lock.json and package.json file with your collegeus