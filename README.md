# Alpine Cloud9 IDE Docker</br>![Maintenance](https://img.shields.io/maintenance/no/2019.svg)

**NOT MAINTAINED!**

I'm no longer maintaining this repository!

This project has has been deprecated for [tomerfi/c9sdk_docker](https://github.com/TomerFi/c9sdk_docker).

You can still use the files :point_up:, if you want.</br>
These :point_down: are the instructions.

__________________________________________

Alpine based image running [Cloud9-SDK IDE](https://cloud9-sdk.readme.io/). </br>

## Base image
`From alpine:3.8` described [here](https://hub.docker.com/_/alpine).

## Image configuration
### Arguments
- *html_page_name*</br>
(applicable for build stage only) used for setting the main page name (origin and default is `ide`).</br>
this is nice to have if you're working in a "multi ide's" enviroment, it's quicker to identify which enviroment you are working on.
### Enviroment variables
- *C9USER*</br>
used for setting the user name for login to the ide, default value is `c9user`.
- *C9PASSWORD*</br>
used for setting the password for login to the ide, default value is `c9password`.
### Volumes
- */workspace*</br>
used for binding a path from the host for allowing data persistence.
### Ports
- *8080*</br>
used for accessing the ide.
## Usage
### Run from hub
#### docker run from hub
```text
docker run -p 8080:8080 -v /path_for_data_persistence:/workspace -e C9USER="user_name" -e C9PASSWORD="nice_password" --name my_container_name tomerfi/alpine-c9:latest
```
#### docker-compose from hub
```yaml
version: "3"
services:
  ide:
    image: tomerfi/alpine-c9:latest
    container_name: my_container_name
    environment:
      - C9USER=user_name
      - C9PASSWORD=nice_password
    ports:
      - 8080:8080
    volumes:
      - /path_for_data_persistence:/workspace
    restart: unless-stopped
```

### Manual build
```text
git clone https://github.com/TomerFi/alpine_cloud9_docker.git /path_for_repository
```
#### docker run from manual build
```text
docker build /path_for_repository --build-arg html_page_name="cool_page_name" --tag alpine-c9:some_tag
```
```text
docker run -p 8080:8080 -v /path_for_data_persistence:/workspace -e C9USER="user_name" -e C9PASSWORD="nice_password" --name my_container_name alpine-c9:some_tag
```
#### docker-compose from manual build
```yaml
version: "3"
services:
  ide:
    build:
      context: .
      dockerfile: Dockerfile
      args:
        - html_page_name=cool_page_name
    container_name: my_container_name
    environment:
      - C9USER=user_name
      - C9PASSWORD=nice_password
    ports:
      - 8080:8080
    volumes:
      - /path_for_data_persistence:/workspace
    restart: unless-stopped

```
