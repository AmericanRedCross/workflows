# ODK 2.0

There are five mobile tools used to create customizable mobile data management applications. The five ODK mobile ‘apps’ that comprise the framework are Services, Survey, Tables, Scan, Sensors, and Submit.

There are currently two options for Cloud Endpoints to communicate with ODK 2 tools (Mobile and Desktop Apps).

1. [ODK Sync Endpoints](http://opendatakit-dev.cs.washington.edu/2_0_tools/release/218/cloud_endpoints#1-Sync-Endpoint) - Supports the full ODK 2.0 REST Protocol
2. [ODK Aggregate 1.4.15 Tables Extension](http://opendatakit-dev.cs.washington.edu/2_0_tools/release/218/cloud_endpoints#2-Aggregate) - Supports the majority of the ODK 2.0 REST Protocol; however, is missing group permission filtering support.

We use the first opetion because it has the group permission filtering support.

## ODK Sync Endpoint

ODK Sync Endpoint is a Docker container that implements the ODK 2.0 sync protocol. 

ODK Sync Endpoint does not store user information in its own database, instead it integrates with a LDAP directory or an Active Directory. That directory is then used to authenticate users and obtain user roles.

**NOTE**: As a consequence of the integration, Basic Authentication is the only supported authentication method.
**PREREQUISITES**: You must have **Docker 17.06.1** or newer, and be running in **Swarm Mode**.



## ODK Sync Endpoint - Setup overview

1. Setup Docker >= 17.06.1 and Run Docker in Swarm Mode
2. Clone `sync-endpoint-default-setup` repository
3. Pull and build the `sync-endpoint-containers` using docker
4. Pull and build the `sync-endpoint-web-ui` using docker
5. Go to cloned directory `sync-endpoint-default-setup` and build db-bootstrap, openldap, phpldapadmin on docker.
6. Create new default group on ldap using phpldapadmin and create user
7. Assing roles to the user based on the available group on the ldap

## ODK Sync Endpoint - Setup in Detail

### Preparing the host (AWS EC2 Instance)
We use AWS EC2 service to create the cloud host and setup our ODK 2.0 Sync Endpoint.
Create EC2 instance of type t2.small or higher. In our case we use Ubuntu EC2 instance of type t2.large
- Login to AWS Console
- Click on Launch instance
- Select `Ubuntu Server 16.04 LTS (HVM), SSD Volume Type`
- Select Type: t2.large (CUPs:2 and Memory: 8 GiB)
- Click on Review and Launch

### 1. Install Docker
#### Set up the repository
Update the apt package index:
```
$ sudo apt-get update
```
Install packages to allow apt to use a repository over HTTPS:
```
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
```
Add Docker’s official GPG key:
```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

```

Verify that you now have the key with the fingerprint 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88, by searching for the last 8 characters of the fingerprint.
```
$ sudo apt-key fingerprint 0EBFCD88

pub   4096R/0EBFCD88 2017-02-22
      Key fingerprint = 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid                  Docker Release (CE deb) <docker@docker.com>
sub   4096R/F273FCD8 2017-02-22
```

se the following command to set up the stable repository.

```
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

```
#### Install Docker CE

Update the apt package index.
```
$ sudo apt-get update
```
Install the latest version of Docker CE, or go to the next step to install a specific version. Any existing installation of Docker is replaced.
```
$ sudo apt-get install docker-ce
```

#### Run Docker in Swarm Mode
```
#docker swarm init --advertise-addr <MANAGER-IP> //IP of the localhost, in this case Elastic IP (Public IP)
```






### 2. Clone 
sdlksjdf

### 3. Pull and build the packages
sdfsdllsdj

### 



```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/rajsingh8220/Test/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
