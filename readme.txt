API CONNECTION AND AIRFLOW DAG INTIALIZATION
- first we create a python enviroment and activate it
- then we initilize apache-airflow in this enviroment --- pip install apache-airflow ---
- we create a dags folder and then create a file named kafka_stream.py where we'll write our airflow dag
- while creating the dag we loaded some json file and tested the results locally before running it on airflow
- after the tests has been completed and everything is okay, we create a function called get_data, which will actuallly get data from our api
- then we'll format our data the way we want it from the data gotten from the get_data function.
- lastly our stream_data will return these formated results as a test before we add kafka and other components to our build


DOCKER COMPOSE FILE FOR OUR KAFKA INTEGRATION (zookeeper, kafka, schema-registry, controller)
- we could check the documentation for their respective docker compose configurations or we could just use ai.
    - specify everything you want to run in your docker-compose and let the ai do the rest
- we'll run the docker compose just to make sure that the enviroment is ready for anything and fix any errors that pop up
- we can check the control center via the port on our localhost:9092
- now we'll test our kafka queue by loading data into it
    - to do that we'll first install kafka-python in our env --- pip install kafka-python ---
    - then we set up the kafka producer, and push messages just to make sure that everything is functioning as it should

DOCKER COMPOSE FILE FOR OUR AIRFLOW INTEGRATION (webserver, postgres, scheduler): we also developed our requirements file etc.
- next we set up our airflow with postgres so we can use it to push data to our kafka system
- now we'll create a directory called scripts for our entry point
- then we create a file called entrypoint.sh
    - in this file we'll writee the sequence of commands that airflow would have to follow when it wants to initialize the webserver or scheduler etc.
- we also create a requirements.txt file which would contain all the packages we've installed on our env to run our docker-compose
    - we create this requirements.txt file by running --- pip freeze > requirements.txt ---
- next we make our producer run on the dags, so we can test it on our airflow webserver
    - for this we just completed our dag setup. we used a while loop and added some try and except commands to make our code more robust
- note: we fixed dependency issues by making sure all our airflow versions are pegged to our env python version


DOCKER COMPOSE FILE FOR OUR SPARK/cassandra INTEGRATION (sparkmaster, sparkworker, cassandradb)
- we add our sparkmaster to our docker compose
- then we add our sparkworker to it: to add several workers we can just copy and paste the work setup but change the name (e.g worker 2)
- we also add cassandra to our compose: we'll add the volumes if we need to mount cassandra in our dir and get data into cassandra
- once spark and cassandra is up and running we'll create a new file in our project folder called spark_stream.py
- now that all our dependencies are working, we'll install cassandra and spark packages in our virtual env
            ---
            pip install cassandra-driver # so we can communicate with cassandra
            pip install spark, pyspark
            ---

then we write our spark_stream code:
    - we'll create a spark connection funtion
        - in the config we'll setup some java packages that will connect our spark to other packages: we go to mvnrepository.com: there we'll search for spark cassandra connector:
            - we'll add the scala version and then the version i.e scala:version: this will setup our spark connection to cassandra
            - then we'll find another connector. this time a spark sql kafka connector. we'll download it and use it.: this will connect our spark to our kafka broker
        - then we'll setup our config for our cassandra host

    - next we create our cassandra connection:
        - ...

note: we could just search spark kafka example online or whatever we want to know about or code. google will direct you to examples that you'll find useful for your projects
- we also need to download the jar files from mvnrepository and paste them in in virtual env


- after setting up everything, we run our docker-compose again, then we run our spark stream via python
- then we open cassandra with this --- docker exec -it cassandra cqlsh -u cassandra -p cassandra localhost 9042 ---
- then we describe the table we created --- describe spark_streams.created_users; ---
- --- select * from spark_streams.created_users; ---
- now that we've verified that everything is working: when we're streaming data from kafka, we'll push them to cassandra for storage

- to run everything, we'll start up the docker compose again
- we confirm that our spark sever is running on it's port
- then we submit our spark stream: --- spark-submit --master spark://localhost:7077 spark_stream.py ---
- then we can run our dags and check that it's been pushed to cassandra.