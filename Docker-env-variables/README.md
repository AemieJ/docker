## DOCKER ENVIRONMENT VARIABLES 

* The app.py written below has a color parameter that can be modified hence we will access it through environment variables.

```
app.py 

import os 
from flask import Flask

app = FLask(__name__) 

color = os.environ.get("APP_COLOR")
@app.route("/")
def main() : 
	print(color)
	return render_template("hello.html", color=color)

if(__name__ == " __main__") : 
	app.run(host="0.0.0.0", port="8080")
```

* To run this using python : 
```
export APP_COLOR="blue"; python app.py
```

* To run this using docker : 
```
docker run -e APP_COLOR="blue" <container-name>
```
