**Foreword**

A note on cloud computing.

---

# What Is Data Science, and What Does a Data Scientist Do?

[From this article](https://www.innoarchitech.com/what-is-data-science-does-data-scientist-do/?utm_source=datacamp&utm_medium=post&utm_content=postlink&utm_campaign=blog):

- Actionable insights (via dashboards, reports, visualizations, ...);
- Anomaly detection (e.g., fraud detection);
- Automated processes and decision-making (e.g., credit card approval);
- Classification (e.g., spam or not spam);
- Forecasts (e.g., sales and revenue);
- Optimization (e.g., risk management);
- Pattern detection and grouping (e.g., classification without known classes);
- Prediction (predict a value based on inputs);
- Recognition (image, text, audio, video, facial, ...);
- Recommendations (e.g., Amazon and Netflix recommendations);
- Scoring and ranking (e.g., FICO score);
- Segmentation (e.g., demographic-based marketing).

# Scalable Data Science Beyond The Local Machine

As advanced analytics becomes more prevalent and data science teams grow, collaborative needs also extend to include those outside of data science teams.  

# What Is the Cloud Exactly?

Computers connected together that share resources are called a network, with the Internet itself being the largest.  
Computers in a network are usually called nodes.  
Computers are often not located on-premise, meaning that applications and data are often hosted on computers located in a data center.  
Group of computers are connected to the same network and are working together to accomplish the same task or set of tasks, this is referred to as a cluster.  
A cluster can be thought of as a single computer, but can offer massive improvements in performance, availability, and scalability as compared to a single machine.  
The term distributed computing or distributed systems refers to software and systems that are written to leverage clusters to perform specific tasks, such as Spark.  
A cloud describes the situation where a single party owns, administers, and manages a group of networked computers and shared resources typically to host and provide software-based solutions.  Given this definition, while the Internet is definitely considered a network, it is not a cloud since it's not owned by a single party.

# Data Science in the Cloud

Once the development environment is setup, the typical data science workflow or process begins.  
The iterative workflow steps typically include:

- Acquiring data;
- Parsing, munging, wrangling, transforming, and sanitizing data;
- Analyzing and mining the data, such as Exploratory Data Analysis (EDA), summary statistics, etc.;
- Building, validating, and testing models, such as predictive, recommendations, etc.;
    - Note: If not building models, then identifying patterns or trends, generating actionable insights, extracting useful information, creating reports, and so on. Here, this tutorial will consider either case "creating a deliverable";
- Tuning and optimizing models or deliverables.

Sometimes however, it is not practical or desirable to perform all data science or big data-related tasks on ones local development environment.  
Here is a list of some of the main reasons why:

- Datasets are too large and will not fit into the development environment's system memory (RAM) for model training or other analytics;
- The development environment's processing power (CPU) is unable to perform tasks in a reasonable or sufficient amount of time, or at all for that matter;
- The deliverable needs to be deployed to a production environment, and possibly incorporated as a component into a larger application (for example, web application, SaaS platform, ...);
- It is simply preferred to use a faster, and more powerful machine (CPU, RAM, ...) and not impose the necessary load on the local development machine.

Typically, people offload the computing work to either an on-premise machine, or cloud-based virtual machine.  
There are many cloud and service-based offerings available: 

- AWS EC2;
- Google Cloud ML;
- AzureML;
- Rackspace;
- Algorithmia;
- DominoLab;
- Continuum;
- and many more.

Read on [application types, requirements, and components](
https://www.innoarchitech.com/cloud-software-big-data-architecture-application-types-requirements-components/?utm_source=datacamp&utm_medium=post&utm_content=postlink&utm_campaign=blog)

# Advantages

Working in the cloud has two main advantages:

- Scalability: you can tailor the power (RAM, CPU, GPU) of your instance to your immediate needs. Starting with a small and cheap instance and adding memory, storage, CPUs or GPUs as your project evolves.
- Reproducibility: a key condition of any data science project. Allowing other data scientists to review your models and reproduce your research is a necessary condition of a successful implementation. By setting up a working environment on a virtual instance, you make sure your work can easily be shared, reproduced, and vetted by other team members.
