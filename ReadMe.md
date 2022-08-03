## GitHub Action

Github Action is a useful tool for CI (Continuous Integration /Continuos Deployment). Github Action is written in yml file. 

### An example of main domain and staging domain of GitHub Action workflow file 

```
Local Git Change --> Push to GitHub --> on branch specific GitHub action start to Deploy --> Cpanel with ftp server name, username & password --> website update & deployment
```

* A yml workflow for main branch to main domain deployment

```
name: 🚀 Deploy to website by git push on main branch

on: 
  push: 
    branches:
      - main

jobs:
  web-deploy:
    name: 🎉 Deploy
    runs-on: ubuntu-latest

    steps:
    - name: 🚚 Get latest code
      uses: actions/checkout@v2
    
    - name: 📂 Sync files
      uses: SamKirkland/FTP-Deploy-Action@4.0.0
      with:
        server: servername.com
        username: ${{ secrets.FTP_USERNAME }}
        password: ${{ secrets.FTP_PASSWORD }}
        server-dir: /public_html/
```
* A yml workflow for staging branch to staging subdomain deployment

```
name: 🚀 Deploy to website by git push on staging branch

on: 
  push: 
    branches:
      - staging

jobs:
  web-deploy:
    name: 🎉 Deploy
    runs-on: ubuntu-latest

    steps:
    - name: 🚚 Get latest code
      uses: actions/checkout@v2
    
    - name: 📂 Sync files
      uses: SamKirkland/FTP-Deploy-Action@4.0.0
      with:
        server: servername.com
        username: ${{ secrets.FTP_USERNAME }}
        password: ${{ secrets.FTP_PASSWORD }}
        server-dir: /staging.name.com/
```

