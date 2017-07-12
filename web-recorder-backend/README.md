# Web Recorder Backend
Backend represents all the logic behind the scenes. It is responsible for test running and scheduling. Backend's API can be accessed from http://snf-7503980.vm.okeanos.grnet.gr:4000 or can be installed locally to your PC. You can see documentation's API [here][documentation].

[documentation]: http://snf-750380.vm.okeanos.grnet.gr:8080/documentation

## Installation
### Docker Installation

### Manual Installation
For manual installation you have to install these packages:
#### Selenium Wedriver using npm
```
$ npm install selenium-webdriver
```
#### MongoDB

 First we have to import the key for the official MongoDB repository.
```
$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
```

Issue the following command to create a list file for MongoDB.
```
$ echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
```

After adding the repository details, we need to update the packages list.
```
$ sudo apt-get update
```

Now we can install the MongoDB package itself.
```
$ sudo apt-get install -y mongodb-org
```

We'll create a unit file to manage the MongoDB service. Create a configuration file named mongodb.service in the /etc/systemd/system directory using nano or your favorite text editor.
```
$ sudo nano /etc/systemd/system/mongodb.service
```

Paste in the following contents, then save and close the file.
```
[Unit]
Description=High-performance, schema-free document-oriented database
After=network.target

[Service]
User=mongodb
ExecStart=/usr/bin/mongod --quiet --config /etc/mongod.conf

[Install]
WantedBy=multi-user.target
```

Next, start the newly created service with `systemctl`.
```
$ sudo systemctl start mongodb
```

While there is no output to this command, you can also use `systemctl` to check that the service has started properly.
```
$ sudo systemctl status mongodb
```

Output
```
● mongodb.service - High-performance, schema-free document-oriented database
   Loaded: loaded (/etc/systemd/system/mongodb.service; enabled; vendor preset: enabled)
   Active: active (running) since Mon 2016-04-25 14:57:20 EDT; 1min 30s ago
 Main PID: 4093 (mongod)
    Tasks: 16 (limit: 512)
   Memory: 47.1M
      CPU: 1.224s
   CGroup: /system.slice/mongodb.service
           └─4093 /usr/bin/mongod --quiet --config /etc/mongod.conf
```

The last step is to enable automatically starting MongoDB when the system starts.
```
$ sudo systemctl enable mongodb
```

#### Install Packages
After selenium and MongoDB installation you have to run `$ npm install` in backend folder in order to install all the required packages.

### Running
Now you can run Web Recorder's API after having installed all required packages. In order to run API type this command:
```
$ node server.js
```
You can run `server.js` using also [nodemon][nodemon] or [forever][forever].

[nodemon]: https://github.com/remy/nodemon
[forever]: https://www.npmjs.com/package/forever