# lecc-be
Projeto LECC - Localizador para Empresas em Caso de Catástrofe

## Install required software

- Git
    - Make sure you can run 'git' command from any cli window
    - Set Git for Windows to check in line breaks in Unix format, and check ou as is
- Docker
    - It requires WSL to be installed and updated
       - On a command line, do:
           - wsl.exe --install
           - wsl.exe --update
    - Make sure the Docker Engine is up and running, after getting WSL worked out.
- OSGeo4W : https://trac.osgeo.org/osgeo4w/
    - Make sure to install it under C:\OSGeo4W
    - Select 'Express' install and GDAL option
        - It will take some time to download
    - after install, run setup-osgeo4w.bat to set it up on Windows
        - Make sure you started the terminal (or IDE with terminal inside) as Administrator
    - Reference: https://docs.djangoproject.com/en/5.2/ref/contrib/gis/install/#windows
- Python
    - Install Python 3.12 for windows
    - https://www.python.org/downloads/release/python-31211/

## Set up the project virtual environment

- Go into the folder where you cloned the project
- Inside the folder, run:
    - create-venv.bat

## Activate the virtual env and install required libs

- Every time when you start the project, make sure you are in the virtual env
- To activate the virtual env, do:
    - cd .ven
    - cd Scripts
    - activate
- This can be automated in your IDE to avoid this every time
    - On vscode, install the Python extension from Microsoft
- To install all the necessary Python libraries for the project, run:
    - pip install -r requirements.txt
    - this will install django, psycopg and other libs listed in requirements.txt

## Start the database

- For the Django project to run, you need to have the database up and running. 
- Call the file start-db.bat
    - this file will start all the containers defined in the docker-compose.yml file.

## Run Migrations (create the database tables)

- You need to run the migrations that will setup the basic database tables
- The databse container should be running
- command: python manage.py migrate

## Start the Django development server

- To start the development server, run:
- python manage.py runserver
- accesse the dev server for the first time using the URL:
    - http://127.0.0.1:8000/

## Next steps

- Code using the Django web framework:
    - https://docs.djangoproject.com/en/5.2/

- Create a model (db table) to store de equipments locations
    - Columns: equipament id, lat/lon, datetime
    - use the geospatial column for lat/lon

- Create an API for:
    - POST: to receive the equipments location info
       - Payload: equipment id + lat/lon
    - GET: to retrieve the equipments location info
       - Input as url arguments: equipment id + time range
       - Output as geojson of a path or a point 
