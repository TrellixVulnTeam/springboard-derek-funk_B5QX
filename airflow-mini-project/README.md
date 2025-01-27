# Airflow Mini-Project
This project sets up an Airflow workflow that emails you the daily 1-minute interval stock price data for Apple and Tesla, every weekday at 6pm local time.

The infrastructure involves a Docker container per component of the Airflow application: web server, scheduler, worker, executor, and metadata stores. Although a Celery (parallel) executor is used, only 1 worker is used effectively reducing the processing to a Sequential (linear) executor.

# How you can replicate this project
* download docker and docker-compose
* start docker engine
* download this repository
* if you would like Airflow to send you emails, create a new gmail account with the *Less secure app access* feature ON
* in *airflow/airflow.cfg*, change:
    * *smtp_user* and *smtp_mail_from* to the full email address
    * *smtp_password* to the email password
* in the repository, open a command line shell and build the containers: `$ docker-compose up -d --build`
* to view the status of the containers: `$ docker ps`
* to see the contents of a container: `$ docker exec -it <CONTAINER ID> bash`
* open the web scheduler in a browser at http://localhost:8080/
* find the DAG *marketvol* and toggle it ON
* You should now receive an email every weekday at 6pm with Apple and Tesla stock price data as attachments. It will look like this: ![This is a alt text.](images/image_emailAttachments.png "image_emailAttachments.png")
* if the DAG run is unsuccessful, you will receive an email for each task failure with a link to the web server in order to diagnose
* you can shutdown the app at anytime: `$ docker-compose down`

# Manual DAG Run
* you can manually trigger the DAG in the web scheduler UI
* a successful run looks like this: ![This is a alt text.](images/image_successfulRun.png "image_successfulRun.png")
* If it is a weekend day, there will be no stock file. In this case, in *airflow/dags/marketvol.py* you can temporarily change *start_date* to a weekday, then rebuild the containers and trigger the DAG.

# Sources
* https://towardsdatascience.com/deploy-apache-airflow-in-multiple-docker-containers-7f17b8b3de58
