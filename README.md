# Docker Setup for Laravel/Lumen projects

## Local dev guide (Linux)

1. Clone the repo:
    ```.sh
    git clone https://github.com/TOA-Anakin/lumen-docker-dev.git
    ```
2. Rename the cloned repo as desired: 
    ```.sh
    mv lumen-docker-dev your_project_name
    ```
3. Check your user ID using the `id -u` command and update the `.docker/.env` file accordingly.
4. `cd` into the `.docker` directory and build the Docker containers:
    ```.sh
    cd your_project_name/.docker
    docker compose up -d --build
    ```
    Before the end of the process you should see a list of newly created (now running) containers:
    ```.sh
    [+] Running 2/2
    ✔ Network lumen_docker_app      Created      0.1s 
    ✔ Container lumen_docker-api-1  Started      0.1s
    ```
5. Open the terminal of the PHP container (mine is named `lumen_docker-php-1`) and create a Lumen project using `composer`:
    ```.sh
    docker exec -it lumen_docker-php-1 bash
    composer create-project --prefer-dist laravel/lumen tmpdir
    ```
    Move the contents of `temp_dir` into the project root:
    ```.sh
    mv tmpdir/* . && mv tmpdir/.[!.]* . && rmdir tmpdir
    ```
6. Access your Lumen web app at http://localhost