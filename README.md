plantuml-editor v1 docker-compose environment
=============================================

Usage

#### Start

    docker-compose up --build -d

#### Connect

    # open this url in your browser
    echo "https://$(docker-compose port httpd 443)/"

    # also avaiable over hare http
    echo "http://$(docker-compose port httpd 80)/"

#### Stop

    docker-compose down

