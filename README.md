Tutorial adpated from here: https://devcenter.heroku.com/articles/getting-started-with-python#define-config-vars

1. Create a free Heroku account
2. Have Postgres installed locally/ via docker/ via RDS
3. Install the Heroku Command Line Interface (https://devcenter.heroku.com/articles/getting-started-with-python#set-up)
4. Use the `heroku login` command to log in and authentificate the Heroku CLI
5. Clone a simple Flask app from this repository
6. Create an app on Heroku with `heroku create <my-app-name>`. This will create another git remote called `heroku` that you can use to update the app. 

    - You can allready visit your app in the browser by visitng https://<my-app-name>.herokuapp.com/ or by typing `heroku open -a <my-app-name>` into the command line
    
7. Now push the flask code to heroku: `git push heroku master`
8. Visit logs via `heroku logs --tail`
9. Create a `Procfile` that defines the command that should be executed to start the web app

```bash
 web: gunicorn gettingstarted.wsgi --log-file -
```

10. with `heroku ps -a <my-app-name>` you can check you rate limits and how many dynos are currently running

    - you can scale the number of dynos by `heroku ps:scale - a <my-app-name> web=0`. For a free account you can only have one dyno running. Free dynos sleep after halg hour of inactivity
    
11. add a `requirements.txt` to your app so heroku knows which packages it has to install when setting up the dyno
12. to run the app localy type `heroku local web` or on windows `heroku local web -f Procfile.windows`
13. add the `requests` module to the `requirements.txt` and add a new route to your app: 

```python
def index(request):
    r = requests.get('http://httpbin.org/status/418')
    print(r.text)
    return HttpResponse('<pre>' + r.text + '</pre>')
```
14. test the changes locally and then deploy them with `git add .`, `git commit -m "demo"` and `git push heroku master`, see if it worked by reloading your app `heroku open`

## Config Variables

- Access environment variables via the `os.environ.get`  function
- Environment variables are set based on the content of the `.env` file in the local directory 
- To set config vars on heroku type in `heroku config:set TIMES=2`
- You can view the config variables via `heroku config`

## Database

- Heroku automatically setups a postgresql database. Check it out by typing `heroku addons`, `heroku config` and `heroku pg`
- The hostname of your database is: `https://<my-app-name>.herokuapp.com/db`






