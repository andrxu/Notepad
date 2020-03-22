### Mount a host path with a script and execute the script within a docker

```
docker run -it --rm --name pythonApp -v "$PWD":/usr/src python:2 python /usr/src/hello.py
```
