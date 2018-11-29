# Lab. Assignment. MongoDB

## The Dataset

The dataset that we are using consists of 
a MongoDB collection with 88 documents.
Each document corresponds to a movie, described by 
the following attributes: title, year,
genre, summary, country,  director
and actors.
The value of the attribute director is  a document that describes
an artist with the following attributes: first_name,
last_name, birth_date and role.
The value of the attribute actors is a list of 
documents, each describing an artist.
The values of all the other attributes are strings.

# Preliminaries

You will need to have Docker installed on your computer.
If it is not the case, please [click on this link](https://store.docker.com/). 

In order to use MongoDB, you will need to:

1. Launch a MongoDB server.
2. Import the data into the database.
3. Launch a MongoDB client. 

The client queries the database through the server over a network.

Open a terminal (Windows users: Command Prompt or PowerShell, but not PowerShell ISE)
and create a directory named mongo-assignment with the following command:

```
mkdir mongo-assignment
```

Move to that directory with the following command:

```
cd mongo-assignment
```

Create a new directory named data with the following command:

```
mkdir data
```

Download the file moviesEmbedded.json and place it
in the directory data.

### Launch a MongoDB server

First, create a network, so as the client and the server can 
communicate, with the following command.

```
docker network create app-tier --driver bridge
```

Then launch a MongoDB server with the following command (make sure you are connected to the Internet).

```
docker run -d --name mongodb-server --network app-tier bitnami/mongodb:latest
```

### Import the data

In order to import the data, run the following command:

```
docker run --mount type=bind,source=data,target=/home/data -it --rm --network app-tier bitnami/mongodb:latest mongoimport --db movie --collection moviesEmbedded --drop --jsonArray --file  /home/data/moviesEmbedded.json  --host mongodb-server
```

### Launch a MongoDB client

To launch a MongoDB client, run the following command:

```
docker run -it --rm --network app-tier bitnami/mongodb:latest mongo --host mongodb-server
```

