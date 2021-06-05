# MovieRecommender
This project is a web app for movie websites like Netflix where a user is allowed to create an account and watch movies. This web app has mainly focused on the quality of recommendations we make to the user. From the various forms of recommendations we have used some of the most appropriate ones. The user can view the already watched and rated movies in the dashboard. But before that when the user opens the web app he is prompted to login the website if not registered we can as well register. The web app has a nice GUI with every button and field labeled with their respective role. So, the user will not face any difficulty in using the web app.


# Installation Guide
You must have Python 3.6+ installed in your system. Since this is upgraded version of the project. You can prefer older version of this project 
###### Download the latest version of Apache Spark form the official site. I'll recommend you to use the same version which I am using for painless journey.  
```
wget -q https://downloads.apache.org/spark/spark-3.0.1/spark-3.0.1-bin-hadoop2.7.tgz
```
###### Extarct this folder and move it to the Home directory. 

Clone this repository:
If you don't have installed pip, use pip3 for installation 
```
sudo apt-get install python3-pip
```
Set up a virtual environment and activate it to avoid dependency issues.
```
virtualenv venv
source venv/bin/activate
```
Install default-libmysqlclient-dev for flask-mysqldb:
```
sudo apt install default-libmysqlclient-dev
```
Install the required dependencies using the following command
```
pip3 install -r requirements.txt
```
MySql database setup:
```
mysql -u root;

mysql> CREATE DATABASE flaskapp;
mysql> USE mysql;
mysql> UPDATE user SET plugin='mysql_native_password' WHERE User='root';
mysql> FLUSH PRIVILEGES;

mysql> USE flaskapp;
mysql> CREATE TABLE `users` (
  `ID` int(20) NOT NULL,
  `Password` char(60) DEFAULT NULL,
  `Name` varchar(40) DEFAULT NULL,
  `Genre1` varchar(40) DEFAULT NULL,
  `Genre2` varchar(40) DEFAULT NULL,
  PRIMARY KEY (`ID`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;
mysql> exit;

mysql -u root;
```
###### Make Sure your MySql server keep running. 

# Data Set
Download the dataset by running `download_dataset.sh`.
###### Move item_based_features folder to `/datasets/ml-latest`.
For the convenience I have replaced `/datasets/ml-latest/ratings.csv` by `/datasets/ml-latest-small/ratings.csv` to run locally.

# Instructions to run Application
  - Make sure Folder `[spark-3.0.1-bin-hadoop2.7]` in in home directory. 
  - Go to the Network settigs: Find the IPv4 Address.
  - Go to `home/<username>/spark-3.0.1-bin-hadoop2.7/conf` and make a copy of `spark-env.sh.template` file and rename it to `spark-env.sh`
  - Add `SPARK_MASTER_PORT=5435` ,`SPARK_MASTER_HOST=<Your IPv4 Address>` in `spark-env.sh` file.
  - Go to the project folder and find `server.py` file and update `'server.socket_host': '<Your IPv4 Address>'`.
  - The file `server/server.py` starts a [CherryPy](http://www.cherrypy.org/) server running a [Flask](http://flask.pocoo.org/) `app.py` to start a RESTful web server wrapping a Spark-based `engine.py` context. Through its API we can perform on-line movie recommendations.  
