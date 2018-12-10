---
title: 'Challenge: analyzing Twitter streaming'
author: Thinkful
team: grading
time: 90
uuid: 17df2909-27b4-417f-a7ad-ace0f69c56d8
---

In the previous checkpoint, we simulated streaming data by splitting a static dataset into segments and streaming each segment one at a time through Spark locally. Now, you'll be working with live streaming data via Twitter's API. In this exercise, you'll set up a Twitter app, run a Docker network to handle the data, and complete a data analysis based on a research question of your choosing.

Streaming data is extremely fragile, which is why most production-level Spark environments use software like [Apache Kafka](https://kafka.apache.org/intro) to create a persistence layer between Spark and the data feed. For our purposes, we'll use a network of two Docker containers - one data serving container (managed by a bash shell session), and a second container to process our streams, which you'll work on within a typical Jupyter notebook.

## Setting up the Twitter app

Before getting started, you'll need to set up a [Twitter account](https://twitter.com/) (if you don't already have one) and get credentials to access the Twitter API.

Ian Anderson Gray has written a great set of [instructions for setting up a Twitter app](https://iag.me/socialmedia/how-to-create-a-twitter-app-in-8-easy-steps/) if you get stuck.

Go to [apps.twitter.com](https://apps.twitter.com/), click on "Create New App", and follow the instructions. For your website URL, you can use the URL to your forked big data student resources GitHub repo.

Once you've set up your "app," copy the following tokens: Consumer Key, Consumer Secret, Access Token, and Access Secret.

**A note on the tokens:** treat them as you would passwords. This means you should store them in a safe place that is outside of source control. This can be as simple as a text file backed up on Dropbox, or a more secure location like a secure note in LastPass. The easiest way to expose them to your application is to set them as environment variables and reference the variables in Python. You'll see this in action when we set up our server.

## Setting up the network

Before we start our containers, we need to set up our network. Docker's syntax for interacting with networks builds on the syntax we're already familiar with. We've seen `docker image`, `docker container`, and `docker build`. The command for interacting with Docker networks is simply: `docker network`.

We'll need to do the following:

1. Create our network.
2. Start our containers and attach them to the network.
3. Inspect the network to make sure that the two containers are, in fact, properly attached.
4. Stream data across the network.

To create our network, we simply use the following command in a terminal window: `docker network create --driver bridge thinkful-net`. This command uses the default bridge network and creates a network called `thinkful-net`.

To confirm that the network was set up, we can check with: `docker network ls`.

Now, it's time to launch our two containers. We'll use the standard `docker run` command, but in this case, we have two containers, not one. We want them to connect to the network, have a readable name, and map the right data into each container. In addition, for the data server, we need to easily get into the container's shell so we can activate the server.

Launch the server with the following command: 

```
docker run -dit --rm --name data_server --network thinkful-net -v /path/to/big-data-student-resources/ServeStreams:/home/ds/data thinkfulstudent/simple_server /bin/bash
```

Note the switches we use:

* `-dit` launches in the background, but also lets the container know we may want an interactive session.
* `--rm` removes the container when we stop it.
* `--name` allows us to assign our own name to the container.
* `--network` attaches to the network.
* `-v` is the same folder mapping we've consistently used to assign data to the container.

As usual, be sure to swap out `/path/to/big-data-student-resources` for the path that's local to your machine. After the image name (`thinkfulstudent/simple_server`), you'll note that we have a `/bin/bash` statement - that's so we can easily get into our shell.

Launch the Spark instance in the same way we have before, but this time we'll also add a name and a network flag to the `run` statement.

```
docker run -d --rm --name pyspark1 --network thinkful-net -v /path/to/big-data-student-resources:/home/ds/notebooks -p 8888:8888 thinkfulstudent/pyspark:2.2.1
```

Once both containers are up and running, we need to confirm that they are on the `thinkful-net` network and find their IP addresses so we can have them talk to each other.

Check the network status by typing `docker network inspect thinkful-net`. You should see formatted JSON output to the window, and if you find the `Containers` field, you'll see the name and IPv4 address of each container. Take note of these, we may need them later.

If you want to learn more about networking with Docker, the best place to start is with their [network tutorial](https://docs.docker.com/network/network-tutorial-standalone/).

## Streaming the data

Now that the network is set up and our containers are running, it's time to get going on our streaming datasets. 

First, we'll access the bash shell for the data server by running the command `docker attach data_server`. Next, move into the `twitter` directory, where the code for our server lives. Open the `server.py` file in your preferred text editor. This file lives locally on your machine at `big-data-student-resources/ServeStreams/twitter/server.py`, assuming you haven't reorganized your big data student resources directory.

A few things to note:

* If you haven't yet, from the terminal `bash` shell, set four environment variables as follows: 
	* `export CONSUMER_KEY=<paste-your-key-without-quotes>`
	* `export CONSUMER_SECRET=<paste-your-key-without-quotes>`
	* `export ACCESS_TOKEN=<paste-your-token-without-quotes>`
	* `export ACCESS_SECRET=<paste-your-token-without-quotes>`
* You are authenticating to Twitter with a `requests_oauthlib` object. Using the four keys mentioned above makes this clean and simple.
* There is a `get_tweets` function that builds a URL and sends the query to Twitter. Take a look at the various options here. They come from the Twitter Realtime Filter API. In our example, we're trying something simple - just find tweets sent from New York City that contain a hashtag, and then count the occurrences of that hashtag. This will tell us what the most popular hashtag in NYC is while we're running our server.
* You should modify the query to reflect the question you want to answer - check out the [API Documentation](https://developer.twitter.com/en/docs/tweets/filter-realtime/overview) for details on parameters and usage.
* The API returns a JSON object, which we then use to send the full text of the tweet to Spark. You're not limited to this, though - you can examine the object to see what else is there that you might want to test.

Once you're happy with the query and the information you want to analyze in Spark, you can start the server by running `python3.6 server.py` in the shell. The server will wait for your notebook to initiate its connection.

Now, you're ready to run the `Twitter streaming challenge` notebook in your big data student resources directory. When you're done, submit a link to your notebook below.

Whenever you're ready to terminate the server, use `ctrl-c`, and exit the shell with the shortcut `ctrl-p ctrl-q`.

