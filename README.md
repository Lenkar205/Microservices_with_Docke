# Microservices_with_Docke

Boué Bigne Lucas 
M2-Technologie de l'internet
UPPA

This project consist in the display of a game in a browser.
The game is a pong replica. If you want in the archive there is the documentation of the game, it's "rapport.html"(the documentation is in french).

Unfortunately I have fail to achive this project but I will show you what I have done.

I managed to deploy my game in in a containner and open a brower in another containner but these two containner are not connected.

1) open a terminal and go into the archive 

2) enter the command "xhost +" 
for allow clients to connectfrom any host

3) enter the command "docker-compose up --build".

At this point a firefox browser should be open but unfortunatly I didn't succced to display the game in this browser
If you want to see the game you have to use your browser and go into your localhost : 127.0.0.3:80

4) display the game
 the containner "Pong3D" run must running


* with CHROME:
        open your chrome browser
        enter 127.0.0.3:8080

* with firefox:
        open another windows in the bash tap the command "docker stop RenardFeu"
        open your firefox browser
        enter 127.0.0.3:8080


Here I will describe my two containers:

The first one use a ngix image where I replace the homepage by my game

The second use a ubuntu image and display a firefox browser


The part that I have fail is to connect my containners. I think it's about add "networks" into my docker-compose

here you have my unfinished docker-compose with the networks section: 

version: '2'
services:
    pong:
        build: ./dockerfile_pong
        container_name: Pong3D
        ports:
            - "8080:80"
	networks: 
	 - MyNetwork
    os:
        build: ./dockerfile_browser
        container_name: RenardFeu
        environment:
            - DISPLAY=$DISPLAY
        volumes: 
            - /tmp/.X11-unix:/tmp/.X11-unix
        command: firefox
	networks: 
	 - MyNetwork

Networks:
	MyNetwork:
		driver: bridge
		config:
		  - subnet: 127.0.0.3/24
		    gateway: 127.0.0.3
