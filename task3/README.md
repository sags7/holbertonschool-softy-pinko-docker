Connects the front-end to the back-end allowing you to have dynamic data on your front-end. This means that communication will occur between your two Docker images (each of which will be running in their own Docker container). To facilitate this, be sure to have multiple terminal instances open so you can have one Docker container running on each.

First thing we should do is prepare the front-end. We need to add a couple of things:

New HTML to add

<h1 id="dynamic-content"></h1>
This needs to be added before the <h1> that includes the text “We provide the best strategy to grow up your business”.

index.html

// . . . SOME HTML BEFORE . . . 
<div class="offset-xl-3 col-xl-6 offset-lg-2 col-lg-8 col-md-12 col-sm-12">
    <h1 id="dynamic-content"></h1>
    <h1>We provide the best <strong>strategy</strong><br>to grow up your<strong>business</strong></h1>
    <a href="#features" class="main-button-slider">Discover More</a>
</div>
// . . . SOME HTML AFTER . . . 
This new <h1> tag with the ID of dynamic-content is the place we’re going to insert dynamic data from our API server.

Now we need to actually use some JavaScript code to make the request. Place the following script near the bottom of the HTML as the last <script> tag before the closing </body> tag.

Add this script to your index.html

<script>
    // Load dynamic data from the back-end on port 5252
    $(function() {
        $.ajax({
            type: "GET",
            url: "http://localhost:5252/api/hello",
            success: function(data) {
                console.log(data);
                $('#dynamic-content').text(data);
            }
        });
    });
</script>
That is all the front-end needs to be able to connect to the back-end, however there is one more thing we must do to our back-end so that it can accept cross-origin requests from our front-end. We must use the CORS plugin for Flask.

In your back-end’s back-end/Dockerfile, use pip3 to install flask-cors after you have installed flask through pip3. Next, use this updated python script as your api.py.

api.py

from flask import Flask
from flask_cors import CORS

app = Flask(__name__)
CORS(app)

@app.route('/api/hello')
def hello_world():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5252)
Now, your back-end will allow your front-end to communicate with it even though they are not on the same server (they are on two different Docker containers).