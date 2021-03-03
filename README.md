# texada-docker

Docker files to build and run Texada ([https://github.com/ModelInference/texada](https://github.com/ModelInference/texada)).

You can run the texada webapp by using the following commands:
<pre><code>git clone https://github.com/cbdm/texada-docker
cd texada-docker
docker build -t texada texada
docker build -t texada-webapp texada-webapp
docker run -p 127.0.0.1:1234:8080 texada-webapp
</code></pre>

Then just open a browser and navigate to 127.0.0.1:1234/texada.
