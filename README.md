# Integrate MySQL with Grafana Dashboard Visualization
## Pre-requisite
 - Create Linux EC2 instance in AWS
 - change the security group inbound rule to allow all traffic
 - connect EC2, then exec commands: 
   - ec2-user
   - sudo su
   - sudo yum update -y
 - install docker:
   - yum install docker
   - systemctl start docker
   - systemctl enable docker
 - make assured no images existed:
   - docker images
   - docker ps -a 
 - to make docker and grafana both are up and running, exec commands:
   - docker run -d --name=grafana -p 3001:3000 -v grafana_config:/etc/grafana -v grafana_data:/var/lib/grafana -v grafana_logs:/var/log/grafana grafana/grafana 
 - copy ip address from ec2 instance then open a new browser and enter ipaddress:3001 
    - exec password admin:admin then replace with a new password 

## Install MySQL
 - docker run -d --name mysqldb -p 3306:3306 -v db_data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=password mysql:latest
 - docker exec -it mysqldb bash
 - mysql -u root -p password
## Now inside the Database
 - show databases;
 - create a database, here I given name is team;
 - USE team;  (Database changed to team )
 - show tables;  (table is empty now)
## Create Table
 - CREATE TABLE person ( person_id INT NOT NULL PRIMARY KEY, fname VARCHAR(30) NULL, lname VARCHAR(30) NULL, age INT NOT NULL, created TIMESTAMP ); 
 - show tables; (person table is created)
 - select * from person;  (empty now)
 - copy then insert the following query
  INSERT INTO person(person_id, fname, lname, age) VALUES(1,'Troy','Williams', 42);
  INSERT INTO person(person_id, fname, lname, age) VALUES(2,'Jennifer','Williams', 32);
  INSERT INTO person(person_id, fname, lname, age) VALUES(3,'Chelsea','Williams', 10);
 - select * from person;  (see 3 rows, 5 columns)

 ## Create MySQL Connection
  - Add DataSource in Grafana 
  - Add MYSQL DB
  - fill up Host with your EC2 public IP Address:3306 , database is team , User is root , Password is password 
  - Save & test
  ## Database Connection OK !!

  # Create your first Dashboard
  - Add visualization 
  - select 'code' at right corner
  - write query: 
  - SELECT * FROM team.person;  (Table view now available)
  - go to the panel option on the right side, and change the panel title with whatever you like! Here, I have used the 'Employee Data' title
  - Apply and save it.
  ## Thank YOU !!
