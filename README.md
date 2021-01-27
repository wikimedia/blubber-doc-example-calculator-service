# A Simple Online Calculator
Service allows for simple calculations, parsing logic from: https://www.dabeaz.com/ply/example.html

Used in the Kubernetes Workshop, currently hosted at:https://docs.google.com/document/d/1bccjDlu3v-6aHTdlMvH1Z3XiJ3lRNGe4hWTMYf3_1Ac/edit



To run:
- python3 server.py
  - needs ply library installed

    - pip3 install ply

      or

    - apt install python3 ply

Or

- docker build . --tag=calc
- docker run -d -p 8080:8080 calc

To access:
- curl http://localhost:8080/api?op=2+7 # json answer
- curl -d "2+9" -X POST http://localhost:8080/api
- browser to http://localhost:8080 for a form based test interface
- http://localhost:8080/healthz for some usage info

To test:
- python3 tests/test01.py
  - requires service running on localhost:8080

File overview

- server.py - the python3 program that implements the service. Uses the built-in http server to serve a simple API. It also has a page that serves health and usage information at /healthz. There is also a form based access that can be used for some simple testing - this function  only works in test builds.
  Note that this implementation needs to generate local files in the working directory for the parser library used and so needs to run with the insecurely: true flag set in blubber.
- Dockerfile - a file that can be used for local testing - not WMF styled
- calcblubber-debian.yaml - the YAML input file for blubber to generate a valid WMF styled Dockerfile
- tests/test01.py - a basic test file for the calculator functionality