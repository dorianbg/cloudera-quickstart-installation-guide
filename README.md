## How to install Cloudera quickstart

For this quick installation we will be using this docker image: https://hub.docker.com/r/cloudera/quickstart/

It has got 100k+ pulls and is the easiest solution for installating Hadoop on a single machine.

Services it contains are:

Apache Hadoop (Common, HDFS, MapReduce, YARN), Apache HBase, Apache ZooKeeper, Apache Oozie, Apache Hive, Hue (Apache licensed), Apache Flume, Cloudera Impala (Apache licensed), Apache Sentry, Apache Sqoop, Cloudera Search (Apache licensed), Apache Spark

Installation process:

0. Please adjust the setting of how much RAM is maximally allocated to docker. Probably adding eg. "-m 6G" to docker run as I used below will work but on MacOS Docker you have to change it within GUI preferences. Please set it to 6GB, but don't worry unless you are doing a lot of computation it shouldn't use more than 2-3GB of RAM.

#### 1. Pull the image from docker hub (4.5 GB in size)  

      docker pull cloudera/quickstart:latest

#### 2. Find the Image ID of the image by running:
 
      docker images

#### 3. Start the container with:  
  
      docker run --hostname=quickstart.cloudera --privileged=true -t -i -m 6G -p 80 -p 8888 -p 7180 [IMAGE ID] /usr/bin/docker-quickstart
  
  Because port forwarding from the above command didn't work for me on MacOS, I used:    
  
      docker run --hostname=quickstart.cloudera --privileged=true -t -i -m 6G -p 80:80 -p 8888:8888 -p 7180:7180 [IMAGE ID] /usr/bin/docker-quickstart

#### 4. (Re)starting services

After the docker container loads up, most likely Hue server failed to load, so just run this to restart it:  

    sudo service hue restart  
  
Also it is very likely that the Cloudera Manager did not work, so use this command to restart it:  
  
      sudo service cloudera-scm-server restart  
  
The cloudera manager works on port 7180, and Hue uses port 8888.  

 
  
#### 5. Login to Hue by going to localhost:8888 using for both username and password  "cloudera"


##### Now that hadoop is working, let's check the files on HDFS:

![1](https://github.com/dorianb96/Cloudera_Quickstart_Install/blob/master/1.png?raw=true)

##### We will quickly define a workflow in Hue:

![2](https://github.com/dorianb96/Cloudera_Quickstart_Install/blob/master/2.png?raw=true)

##### Using the HDFS action from the tool bar, we will create a folder and a file in HDFS:

![3](https://github.com/dorianb96/Cloudera_Quickstart_Install/blob/master/3.png?raw=true)

##### Oozie says it succeeded

![4](https://github.com/dorianb96/Cloudera_Quickstart_Install/blob/master/4.png?raw=true)

##### Let's just check the file succeeded in creation: 

![5](https://github.com/dorianb96/Cloudera_Quickstart_Install/blob/master/5.png?raw=true)
