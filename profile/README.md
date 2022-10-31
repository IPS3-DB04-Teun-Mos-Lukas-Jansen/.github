# Welcome to the MonkoDash organization.

![monkey-happy](https://user-images.githubusercontent.com/81776357/194836855-56efc80b-a942-4cbd-a415-e3c55c0ee3e6.gif)

## About us
We are [Teun Mos](https://github.com/TeunMos) and [Lukas Jansen](https://github.com/LukasJansen100), both at the time of building this project, studying ICT at Fontys university of aplied sciences. We are currently in our third semester, studying software engineering, and working together on this project.

## Our Idea
Our project idea is to create a "Dashboard" for people, to make it easier to navigate through all your digital services. The point of the dashboard is to centralize a lot of services that people use, so they don't need to spend a lot of time going from one to the other.

We want to make the dashboard as customizable as possible. The user should be able to choose which services they would like to enable, and which not. Our dashboard will try to have as many integrations with popular apps, websites, and more.

The dashboard will collect some data from services (where it's allowed!) and use it to create an easy environment where you can find information about your activities/history.

Since the idea for this dashboard is very broad, we can always choose to implement and integrate new services into the dashboard.

## The project
If you are interested in our project and want to learn more, here is a [click here for documentation](https://github.com/IPS3-DB04-Teun-Mos-Lukas-Jansen/Documentation).

## Running the project
To run the project you need to install Docker and Docker Compose, or install Docker Desktop.
[For further instructions, view this page.](https://docs.docker.com/compose/install/)

This is the docker compose file, it contains all the information docker compose needs to start up all the docker containers.
``` yaml
name: dashboard
services:
 
  dashboard-frontend:
    container_name: frontend
    restart: unless-stopped
    image: teunlukas/dashboard-frontend:main
    ports:
      - 3000:3000
    env_file:
    - ./.env
    
  user-preferences-db:
    container_name: user-preferences-db
    restart: unless-stopped
    image: mongo
    ports:
        - 27017:27017
        
  user-preferences-api:
    container_name: user-preferences-api
    restart: unless-stopped
    image: teunlukas/dashboard-user-preferences-api:main
    ports:
        - 8000:8000
    env_file:
    - ./.env
    links:
     - user-preferences-db
```

In the docker compose file there are a few enviroment variables.
To start up this project you will need your own Client ID and CLient Secret.
You can find more information on how to get these [here](https://developers.google.com/identity/sign-in/web/sign-in).
```
REACT_APP_CLIENT_ID = ...
REACT_APP_CLIENT_SECRET = ...
REACT_APP_REDIRECT_URI = http://localhost:3000
REACT_APP_USER_PREFRERENCES_URL = http://localhost:8000
USER_PREF_DB_URL ='mongodb://user-preferences-db:27017/'
```

Save the docker compose in a folder as "docker-compose.yml".
Then save the enviroment variables as ".env" in the same folder as the docker compose file.

Then run "docker compose up --build" in the command prompt to start the project.
