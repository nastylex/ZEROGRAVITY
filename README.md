# FTP Server

A lightweight static file HTTP server.

## Features

* Supports multiple path mappings
* Supports Angular routing
* Supports custom index files
* Supports TLS (HTTPS)
* Supports Basic Authentication
* Supports file compression
* Supports log files and colorful console output
* Supports file uploads

## Run

### Simple Startup

Maps the current directory to the web root. The default port is `8080`.

```sh
./simplehttpserver
```

Open your browser and visit:

```text
http://localhost:8080
```

### Support Angular Routing

Maps the `dist` directory to the web root, uses port `4200`, serves `index.html` as the default file, and falls back to `index.html` for client-side routing.

```sh
./simplehttpserver -addr :4200 -path dist -indexnames index.html -fallback index.html
```

### Enable TLS (HTTPS)

First, use mkcert to generate development certificates.

```sh
mkcert -install
mkcert -cert-file ssl-cert.pem -key-file ssl-cert.key localhost 127.0.0.1 ::1
```

Then start the server with TLS enabled:

```sh
./simplehttpserver -addrtls :8081 -certfile ssl-cert.pem -keyfile ssl-cert.key -username admin -password admin -logfile 1.log
```

Open your browser and visit:

```text
https://localhost:8081
```

### Using a Configuration File

#### 1. Generate a configuration file

```sh
./simplehttpserver -makeconfig config.yaml
```

#### 2. Edit `config.yaml`

You can configure multiple path mappings.

Lines beginning with `#` are treated as comments.

```yaml
addr: 0.0.0.0:8080
#addrtls: 0.0.0.0:8081
#certfile: ./ssl-cert.pem
#keyfile: ./ssl-cert.key
#username: admin
#password: admin
compress: false
paths:
  #/c: "C:\\"
  #/d: "D:\\"
indexnames:
  - index.html
  - index.htm
verbose: true
enablecolor: true
enableupload: true
## Set maxrequestbodysize to 0 to use the default size
maxrequestbodysize: 9223372036854775807
## Set timeout to 0s for no timeout limit
readtimeout: 0s
writetimeout: 0s
logfile: ./simplehttpserver.log
#fallback: ./index.html
#HTTP_PROXY:
#HTTPS_PROXY:
#NO_PROXY: ::1,127.0.0.1,localhost
```

#### 3. Run with the configuration file

```sh
./simplehttpserver -config config.yaml
```

### Show Help

```sh
./simplehttpserver -help
```

## Build

```sh
bash ./build.sh
```

## Acknowledgements

Powered by httpserver-master
created By httpserver-master
For AirSPACEx
