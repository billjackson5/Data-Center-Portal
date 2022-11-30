## Data Center Portal System Deployment Manual
------


### Introduction
------

This document is a guide to the installation, configuration and operation of the BSN Spartan Network Data Center Portal System. This system connects to the Data Center Management System [v1.1.0](https://github.com/BSN-Spartan/Data-Center-System/blob/main/Data%20Center%20System%20Upgrade%20Manual.md) and later version.

### Hardware Requirements
------

Minimum Requirements:
- 1 CPU
- Memory: 2GB

Recommended Requirements:
- 2 CPU
- Memory: 4GB

### System Installation
------

#### 1. Prerequisites

##### 1.1 NodeJS

Node.js should be locally installed. Download from [official website](https://nodejs.org/) and install it. The version of Node.js should be 14 or later.

##### 1.2 PM2 Management Tool1
After installing node.js, install pm2:

```
npm install pm2@latest -g
```
Check whether pm2 is successfully installed:

```
pm2 -v
```


#### 2. Download the Data Center Portal Deployment Package

Download the data center portal deployment package to a local directory:

```
git clone https://github.com/BSN-Spartan/.git
```



#### 3. Configure the Data Center Portal and Management System

##### 3.1 Configure the Port Number of Data Center Portal

Configure the port number in `Data-Center-Portal/package.json` file:

```
"scripts": {
    "start": "next start -p 3000"
  },
```

##### 3.2 Configure the URL of Data Center Management System

Configure the URL in `Data-Center-Portal/next.config.js` file:

```
const baseURL = "date center url";
```

*Note: After changing the the port number of data center portal or the URL of data center management system, you must run the command below to rebuild the project.*

Rebuild the project:
```
npm run build
```

#### 4. Start the Data Center Portal System

Go to the directory where the deployment package is located

##### 4.1 Install Dependencies

```
npm install
```

##### 4.2 Start/Stop the Project

4.2.1 Start the Project

```
npm run build
npm run start
```

4.2.2 Stop the Project

```
 ctrl+C
```

##### 4.3 Permanent Start/Stop the Project

4.3.1 Permanent Start

```
npm run build
pm2 start server.js
```

4.3.2 Permanent Stop

```
pm2 stop server.js
```

#### 5. User Manual Deployment

After deployed the portal, you need to customize the default user manual to meet the actual business requirements.

We have provided the user manual in both word and markdown formats, which can be obtained through `Data-Center-Portal/public/static/` directory.

When using the user manual in markdown format, please ensure that you have installed gitbook locally. Here we take Windows system as an example to introduce how to install and use it:

1. Download and install Node.js from [Offical Website](https://nodejs.org/download/release/v10.12.0/), you need to use a lower version of Node.js to install gitbook.

2. Open command prompt and check the version：
   `node -v`   
   v12.12.0  
   `npm -v` 
   6.11.3

3. Install gitbook by command prompt：
   `npm install gitbook-cli -g`
   Run command below to check the version：
   `gitbook --version`
      CLI version: 2.3.2
      GitBook version: 3.2.3

4. Create a folder and run command below to check whether gitbook has been successfully installed:
    `gitbook init`
    
    If installed, the following message will be returned:
    ```
    warn: no summary file in this book
    info: create README.md
    info: create SUMMARY.md
    info: initialization is finished
    ```
5. Copy the user manual in word format and `user-manual` folder to this folder. The user manual in markdown format is saved in in `user-manual` folder.

    <img src='image/usermanual.png' style='width:600px;' alt='getChainAccessInformation' title='getChainAccessInformation'>


    You can edit the word document and then export it to the pdf version and store that file in the same path. 

    Please keep the name consistent among different user manual formats. 

6. Edit markdown documents. You can open `user-manual` folder through Visual Studio Code to edit the markdown document.

- Click SUMMARY.md to change the directory. Please note that the directory structure is consistent with the word document.

  <img src='image/summary.png' style='width:600px;' alt='summary' title='summary'>

- Click README.md, edit the name, version and revision date of the user manual. If you do not need to provide the pdf version, you can delete the last row of data.

  <img src='image/readme.png' style='width:600px;' alt='readme' title='readme'>

- Configure the logo and copyright information of your online user manual in book.json.

  <img src='image/bookjson.png' style='width:600px;' alt='bookjson' title='bookjsaon'>

- The default user manual creates folders according to chapters. The contents of each chapter are stored in the corresponding folder as markdown documents. You can edit them directly.

  <img src='image/edit.png' style='width:600px;' alt='edit' title='edit'>

- After editing the markdown documents, you can check the user manual by typing `gitbook serve` command to generate html file. You can also directly type `gitbook build` command to generate the user manual in the terminal, and the generated manual will be stored in `_ Book` folder. After saving the file, press `Ctrl+C` to terminate the command.

  <img src='image/build.png' style='width:600px;' alt='build' title='buid'>

- Enable global search, replace `<a href="./">` with `<a href="./index. html">`, replace`< A href="../">` with `<a href="../index. html">`. 
Then, find `index.html file` in `_book` folder and replace `../` with `./`.

  <img src='image/search.png' style='width:600px;' alt='search' title='search'>

- After the above operations are completed, replace the files in the `Data-Center-Portal/public/static/user-manual` folder in the server with the files in `_book` folder.

#### 6. Terms of Service Deployment

After completing the deployment, the portal system uses the default Terms of Service. You need to customize the Terms of Service to meet the actual business requirements.

1. Edit the Terms of Service. The path of the Terms of Service is:

<u>data-center-portal/public/static/Terms Of Service.doc</u>

2. After edited, you can save it as a PDF file and replace the default Terms of Service:

<u>data-center-portal/public/static/Terms Of Service.pdf</u>

3. If you would like to change the name of Terms of Serivce, customize it in the following path:

<u>data-center-portal/components/CustomHeader/index.tsx</u>

```
export const TermsOfService = "/static/newName.pdf";
```
