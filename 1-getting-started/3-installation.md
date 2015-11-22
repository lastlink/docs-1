# Installation
* Check that your server meets the requirements above
* Download and unzip the Directus package from [here](https://github.com/RNGR/directus6/tree/build)
* Create a database and MySQL user (with access and modify privileges) for Directus on your web server
* Upload the files to a specific folder or the root of your web-server
* Run the Directus installation script by accessing the URL where you uploaded the files.

**Once you have completed the install, make sure to delete install folder for security purposes.**

### Troubleshooting

#### Server error occured!
In case you find this error the first time you tried to login, it means you missconfigured Apache2. You might need to add *overrideAllow All* in your virtualHost.
