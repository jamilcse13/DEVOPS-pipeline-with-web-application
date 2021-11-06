- Setup virtual environment inside project
- listed required installation packages inside requirements.txt file and run:
    - pip install -r requirements.txt
- used jsdelivr semantics-ui css and js
- used 'db.create_all()' above app.run() for creating related database

## Our Using Packages and Libraries:

### ngrok:
- Ngrok exposes local servers behind NATs and firewalls to the public internet over secure tunnels.
- ngrok allows you to expose a web server running on your local machine to the internet. Just tell ngrok what port your web server is listening on.
    - ngrok http 80
- Installation procedure:
    - pip install flask-ngrok
- add those lines in our py file:
    - from flask_ngrok import run_with_ngrok
    - run_with_ngrok(app)
- We have to remove debug=True from app.run()
- Here i have faced an error: Permission denied: '/tmp/ngrok/ngrok'
- Solution: We can fix it manualy by changing [project/lib/flask_ngrok.py line 29 os.chmod(executable, 777) into os.chmod(executable, 755)

## Setting CI/CD using Github Actions

### here we use different versions of pythons
- go to github repository->Actions->python-package
- then setup the python-package.yml file
    ```
    # This workflow will install Python dependencies, run tests and lint with a variety of Python versions
    # For more information see: https://help.github.com/actions/language-and-framework-guides/using-python-with-github-actions

    name: Python package

    on:
    push:
        branches: [ master ]

    jobs:
    build:

        runs-on: ubuntu-latest
        strategy:
        matrix:
            python-version: [3.7, 3.8, 3.9]

        steps:
        - uses: actions/checkout@v2
        - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v2
        with:
            python-version: ${{ matrix.python-version }}
        - name: Install dependencies
        run: |
            python -m pip install --upgrade pip
            if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
        - name: Test with pytest
        run: |
            pytest test.py
    ```

## here we use different versions of OS
- go to github repository->Actions->python-package
- then setup the python-package.yml file
    ```
    # This workflow will install Python dependencies, run tests and lint with a variety of Python versions
    # For more information see: https://help.github.com/actions/language-and-framework-guides/using-python-with-github-actions

    name: Python package

    on:
    push:
        branches: [ master ]

    jobs:
    build:

        strategy:
        matrix:
            platform: [ubuntu-latest, macos-latest, windows-latest]
            python-version: [3.7, 3.8, 3.9]
        runs-on: ${{ matrix.platform }}

        steps:
        - uses: actions/checkout@v2
        - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v2
        with:
            python-version: ${{ matrix.python-version }}
        - name: Install dependencies
        run: |
            python -m pip install --upgrade pip
            then pip install -r requirements.txt
        - name: Test with pytest
        run: |
            pytest test.py
    ```

# Docker
- It is a container software
- It is designed to make deployment easier and run applications anywhere using containers
- It is opensource, reusable
- Alternative of docker: rkt, podman, container
## Docker Image and Container:
- Docker image packs up the application and environment required by the application to run
- Containers are runnable instance of an image

# Kubernetes
- to manage multiple docker container

## Minikube
- sets up a local Kubernetes cluster
- Minikube is an open source tool that allows you to set up a single-node Kubernetes cluster on your local machine.
- The cluster is run inside a virtual machine and includes Docker, allowing you to run containers inside the node.
- This is an excellent way to test in a Kubernetes environment locally, without using up too much resources.
- installation process:
    - https://www.linuxtechi.com/how-to-install-minikube-on-ubuntu/
    - https://phoenixnap.com/kb/install-minikube-on-ubuntu
- pod:
    - we can wrap up our container/containers within pod
    - pods can communicate with each other
    - a pod is executed with all its elements
    - it better to use small number of container inside a pod