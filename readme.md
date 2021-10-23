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
