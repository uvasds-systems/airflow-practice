# Lab - Airflow Practice

Get hands-on experience with Apache Airflow.

## Pre-requisites:

1. Docker Desktop
2. Install the `astro` CLI from Astronomer.io. Follow [these instructions](https://www.astronomer.io/docs/astro/cli/install-cli/) for your platform.

## Run Airflow Locally

1. Fork this project, clone it, open it locally and navigate to the `learning-airflow` project subdirectory.

2. Start Airflow for that project on your local machine by running `astro dev start` from within that directory.

    This command will spin up 4 Docker containers on your machine, each for a different Airflow component:

    - Postgres: Airflow's Metadata Database
    - Webserver: The Airflow component responsible for rendering the Airflow UI
    - Scheduler: The Airflow component responsible for monitoring and triggering tasks
    - Triggerer: The Airflow component responsible for triggering deferred tasks

3. Verify that all 4 Docker containers were created by running `docker ps`.

    Note: Running `astro dev start` will start your project with the Airflow Webserver exposed at port 8080 and Postgres exposed at port 5432. If you already have either of those ports allocated, you can either [stop your existing Docker containers or change the port](https://docs.astronomer.io/astro/test-and-troubleshoot-locally#ports-are-not-available).

4. Access the Airflow UI for your local Airflow project. To do so, go to `http://localhost:8080/` and log in with `admin` for both your Username and Password.

You should also be able to access your Postgres Database at `localhost:5432/postgres`.

## Add a new DAG

1. Within the Airflow UI, go to the `Admin -> Variables` from the top navigation menu.
2. Create one variable entry (key-value pair):
    - MONGOPASS - assigned the value given to you in the instruction page (same as Lab 9).
3. Add a new file `simple.py` within the `dags` subdirectory of the project. Paste in the code found here https://gist.github.com/nmagee/1ef0216ca71079aa3078ff46aefd325d
4. Update the database name in the code on line 18 to your UVA computing ID.
5. Save the file and return to the Airflow UI. Refresh the page or wait a couple of minutes for your DAG to appear. It should be in a paused state.
6. Unpause your DAG and run it once by hand.
8. You can use `MONGO-ATLAS` from Lab 9 to review the values your code inserted into the database. Be sure to select the correct database.
9. Take a screenshot of the inserted documents in MongoDB and submit it for the lab.
10. Answer this question: How many documents were inserted into your collection?

### Bonus!

- Explore the other DAG in your Airflow UI ("example_astronauts")
- Cd into the `etl` folder and start Airflow from within that folder to explore how those DAGs work. (You must shut down one Airflow environment before you can spin up another.)

## Cleaning Up

When done, issue the command `astro dev stop` to turn off the Docker stack.
