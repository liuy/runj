# runj

## Introduction

`runj` is a Python script that runs a Jupyter notebook and serves the output as a web page for you.

### Gallery
- A standard setup in a server
![Image text](https://github.com/liuy/runj/blob/master/.images/runj3.png?raw=true)

- Update the log periodically which contains [**tqdm**](https://github.com/tqdm/tqdm) progress bar
![Image text](https://github.com/liuy/runj/blob/master/.images/runj1.png?raw=true)

- Show the error log that contains [**ANSI escape sequences**](https://en.wikipedia.org/wiki/ANSI_escape_code) on the phone
![Image text](https://github.com/liuy/runj/blob/master/.images/runj2.jpg?raw=true)

- Show notebook file content
![Image text](https://github.com/liuy/runj/blob/master/.images/runj4.png?raw=true)

- Show versioned notebook list on the phone
![Image text](https://github.com/liuy/runj/blob/master/.images/runj5.jpg?raw=true)

## Why

I was struggling to search for a lightweight and simple program that  

- run the whole cells of a Jupyter book that would span hours
- serve the output for viewing in a browser so I can view it remotely on my phone
- show tqdm progress bar nicely
- *could edit and maintain a versioned list of notebooks and logs* (For AI hyperparams tuning)

Supprisingly, there was NO such tools. So I ended up wrting it on my own through a late night.

## Requirement

- Jupyter or ipython & nbconvert installed

## Setup

```bash
$ git clone https://github.com/liuy/runj.git
$ cd runj
$ chmod +x runj # allow execution
$ pip install -r requirements.txt # check requirements
```

Then volia there you are!

## **Usage**

To use `runj`, simply run the script with the path to your Jupyter notebook as an argument:

```bash
$ ./runj -h
usage: ./runj [-h] [--ip IP] [--port PORT] [-t] filename

Run a Jupyter notebook and serve the output for viewing in a browser

positional arguments:
  filename     Name of the notebook file to run

options:
  -h, --help   show this help message and exit
  --ip IP      IP address to serve the output on (default: 0.0.0.0)
  --port PORT  Port to serve the output on (default: 8090)
  -t, --token  Generate a token for a safe URL

Example: ./runj text.ipynb
```

By default, `runj` will serve the notebook on `http://0.0.0.0:8090`. You can specify a different IP address and port number with the `--ip` and `--port` options:

```bash
./runj /path/to/notebook.ipynb --ip 192.168.1.32 --port 8888
```

`runj` saves the output of the notebook to a log file in the same directory as the notebook. The log file is named `runj.log`. To view the log, simply open a web browser and go to the URL `http://<ip>:<port>`

## Termination

To stop the `runj`, simply press `Ctrl-C` in the terminal where `runj` is running. This will shut down the web server and kill the notebook ipython process. 

If you run `runj` in the background as in

```bash
$ ./runj text.ipynb &
```

you can gracefully terminate the program by sending a SIGINT

```bash
$ pkill --signal SIGINT python
# Or by PID
$ kill --signal SIGINT {pid}
```
