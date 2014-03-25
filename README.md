## impact-crater.js

    Please be aware this project is highly experimental and the API will change rapidly.

Impact.js meet the world of multiplayer! Take the excellent Impact.js framework and
expand your game to include multiplayer. I have seen many attempts to transform Impact.js into a
multiplayer framework with little success. The main problem being the clients control the game.
Impact-crater is an authoritative server meaning the server makes all the moves and the clients are
merely controllers sending commands to the server. Game development is basically the same, the largest
difference you will notice is the seperation of client and server code, trust me it's still simple and fun.

## Setup

To get started with impact-crater you need to install the nodejs package.

    yum install npm         # CentOS
    apt-get install nodejs  # Debian
    brew install nodejs     # MacOS X

Next you need to install coffee script for the impact-crater command to run properly.

    npm install -g coffee-script

### Git installation

    git clone --recursive git@github.com:impact-crater/impact-crater-core.git

    --- or ---

    git clone git@github.com:impact-crater/impact-crater-core.git
    cd impact-crater-core
    git submodule update --init

Now run:

    cd impact-crater-core
    npm link

### Create project

To make a new impact-crater project run the following:

    impact-crater generate path/to/my-mp-game simple-game

This will setup the folder structure needed to use impact-crater. You should see the following structure. I will list the important files.

    my-mp-game/
        ├── impact/
        │   ├── lib/
        │   │   ├── game/
        │   │   ├── plugins/
        │   │   │   ├── client.js - The plugins for network access
        │   │   │   └── server.js
        │   ├── media/
        ├── public/
        │   └── index.ejs --------- HTML file for your game
        ├── server/
        │   ├── config.js --------- Settings for the server

Next unzip your copy of impact.js over the path/to/my-mp-game/impact folder. If the zip file is on your desktop the command will look like this:

    cd path/to/my-mp-game
    unzip ~/Desktop/impact-1.23.zip

*Important*: Unzipping impact-1.23.zip will overwrite an important file in the template. We created a side copy at `impact/lib/game/main.js.side`. You just need to copy it into place:

    cp impact/lib/game/main.js.side impact/lib/game/main.js

### Config

Make sure the options in the config file are suitable for your environment.

    vim server/config.js

## Starting the server

    impact-crater start path/to/my-mp-game

    ---- or ----

    cd path/to/my-mp-game
    impact-crater start

By default the port is 3000 so visit the following URL in your browser:

    http://localhost:3000

and you should see a game screen. The example template will setup a very simple game using the impact-crater classes that allow for network interaction. You will see a player that you can move with WASD keys. The tree entity is just a drone that moves on its own. If you look at the code you will see that none of the movement is being generated on the client. It's receiving all the movement commands from the server. To truly see the network interaction, duplicate your current browser window
and you should now see two characters on the screen. Both characters should move independently.

## Notes

After installation your file structure should look like the following:

    my-mp-game/
        ├── impact/
        │   ├── lib/
        │   │   ├── game/
        │   │   │   ├── entities/
        │   │   │   ├── levels/
        │   │   │   ├── main.js
        │   │   │   └── server/
        │   │   │       ├── entities/
        │   │   │       └── main.js
        │   │   ├── impact/
        │   │   ├── plugins/
        │   │   └── weltmeister/
        │   ├── media/
        │   ├── tools/

Notice the server folder under the game folder. This is required by impact-crater to differientiate between your server and client code. As you develop your games for multiplayer you will have to start thinking of entities from two points of
view, client-side and server-side.

## Docs

###### Client Classes
* [GameClient](https://github.com/cha55son/impact-crater/wiki/GameClient)
* [EntityClient](https://github.com/cha55son/impact-crater/wiki/EntityClient)

###### Server Classes
* [GameServer](https://github.com/cha55son/impact-crater/wiki/GameServer)
* [EntityServer](https://github.com/cha55son/impact-crater/wiki/EntityServer)

## TODO
* Create an actual server script for people who don't want to use the ```impact-server start``` command
* Move configs to env vars and/org command line args
* Test out on heroku, etc.
* Modularize the template so we can provide say board game templates, rpg templates, arcade shooter templates, lobby/session play templates
* Provide a better logging interface
* Provide a console mode for server control
* Watch the serverProcess so we can restart it potentially
* Allow for several servers to run at the same time

