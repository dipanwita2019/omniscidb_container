# omniscidb_container

This is a guide to run omniscidb as a docker container in local computer and access the tables using console.

# Introduction to omniscidb and omniscidb sql

Install and login to the docker. 

Open a terminal and run the following commands:

docker pull omnisci/core-os-cpu 

$ docker run -d --name omnisci  -p 6274:6274 -v /Users/dmallick/omnisci-storage:/omnisci-storage omnisci/core-os-cpu

#this generates a long list of characters - the first 12 represents the container ID for the omniscidb instance.

docker exec -it <container id> bash #c6484edd75af(my id) password needed : HyperInteractive

docker exec -it c6484edd75af ./insert_sample_data #pick the number of the data table you want to insert

docker exec -it c6484edd75af  /omnisci/bin/omnisql

SELECT origin_city AS "Origin", dest_city AS "Destination", AVG(airtime) AS "Average Airtime" FROM flights_2008_10k WHERE distance < 175 GROUP BY origin_city, dest_city; #Use any query to explore data

# Loading CSV into omniscidb as a table  
copying the csv file in to the container : 
                    docker cp /Users/your_name/test_omni.csv c6484edd75af:/omnisci/sample_datasets
create a table schema by logging into the database similar to the csv file.
                    
create table test1 (

..> name TEXT ENCODING DICT(32),

..> Phone INTEGER,

..> Address TEXT ENCODING DICT(32));

Then copy the csv file data into the created table(i.e, test1)

                   \copy ./small_datasets/test.csv test
Start querying using SQL.
# Important resouces:
https://docs.omnisci.com/latest/3_omnisql.html
https://docs.omnisci.com/latest/5_tables.html  

https://docs.omnisci.com/latest/4_docker_cpu_os_recipe.html

https://docs.omnisci.com/v4.1.3/1_loading_data.html
