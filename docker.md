# Mount a host path and run a file on the host within a docker

```
docker run -it --rm --name pythonApp -v "$PWD":/usr/src python:2 python /usr/src/hello.py
```
