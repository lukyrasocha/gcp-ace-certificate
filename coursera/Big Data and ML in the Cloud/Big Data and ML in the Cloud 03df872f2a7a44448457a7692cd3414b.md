# Big Data and ML in the Cloud

## Google cloud big data platform

### Apache hadoop

- open source framework for big data
- based on MapReduce programming model
    - The MapReduce model is, at its simplest, means that one function, traditionally called the "Map function," runs in parallel with a massive dataset to produce intermediate results. And another function, traditionally called the "Reduce function," builds a final result set based on all those intermediate results.

### Apache spark

- related

All you have to do is request a Hadoop cluster (it will be built for you in 90 seconds or less on top of Compute Engine VM whose number and type you control)

Once your data is in a cluster, you can use Spark and Spark SQL to do data mining and you can use MLib, which is Apache Spark’s ML library to discover patterns through machine learning

## Cloud Dataproc

- great when you have a data set of known size or when you want to manage your cluster size yourself
- if your data shows up in real time or if its of unpredictable size or rate you should use Cloud Dataflow

## Cloud Dataflow

- lets you develop and execute a big range of data processing patterns (extract, transform, load batch computation and continuous computation)
- you use Dataflow to build data pipelines and the same pipeline work for both batch and streaming data

![Untitled](Big%20Data%20and%20ML%20in%20the%20Cloud%2003df872f2a7a44448457a7692cd3414b/Untitled.png)

- no cluster maintenance required

## BigQuery

- fully managed data warehouse
- provides near real time interactive analysis of massive datasets using SQL syntax
- fully managed petabyle scale low cost analytics data warehouse
- no infrastructure to manage so you can focus on analyzing data to find meaningful insights
- pay as you go model
- no cluster maintenance required
- you can load data from cloud storage , cloud data store, or stream it into BigQUery at up to 100 000 rows per second
    - Once its in there you can run fast SQL queries against multiple terabytes of data in seconds using the processing power of Google’s infrastructure
    - you can also read and write data in BigQuery via Cloud Dataflow, Haddop and Spark

## Cloud Pub/Sub and Cloud Datalab

- messaging service
- simple reliable scalable foundation of stream analytics
- pub = publisher
- sub = subscriber
- scalability to one million messages per second and beyond
- important when data arrives at high and unpredictable rates like Internet of Things

Cloud Datalab

- like jupyter notebook

## Machine Learning APIs

- pretrained models
- and platform to generate your own tailored models
- Tenserflow (is developed by Google Brain)

### Cloud Vision API

- gain insight from images
- extract text
- detect inappropriate content

### Cloud Natural Language API

- can return text in real time
- voice to text (transcribe)