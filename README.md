# Batch processing runtime analytics

<a name="readme-top"></a>

<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->


<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>    
    <li><a href="#about-the-project">About the Project</a></li>
    <li><a href="#data-sources-transfer">Data Sources, Transfer and Load</a></li>
    <li><a href="#data-analysis">Data Analysis</a></li>
    <li><a href="#built-with">Built With</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
  </ol>
</details>


<!-- ABOUT THE PROJECT -->
## About The Project

Sponsor / client: Large communication, IT and entertainment company<br>
Status: Test

**Summary**:<br>
A central scheduling system submits batch jobs for many customers (end-of-day processing, file transfers, automated software installations, etc.). More than 1.1 million such batch runs are executed every day. The runtimes of these batch jobs are partially saved, but only used sporadically for further analysis. 

Goals:
- Collect runtime data and transfer it to a suitable system for storage and further processing
- Identify use cases to help optimize operations, increase customer satisfaction or create additional customer services
- Analyzing and evaluating data and visualizing it in a useful way


## Data Sources, Transfer and Load
Raw data is extracted from the following systems:
- Core application
- Scheduling system
- Atlassian Jira

<img src="https://github.com/0LIFR1/big-data-run-time-analytics/blob/main/data_sources.png">

Data has to be transferred to the existing big data platform where it can be imported into HDFS

<img src="https://github.com/0LIFR1/big-data-run-time-analytics/blob/main/data_transfer.png">

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Data Analysis
To start with, two use cases have been identified.

### Use Case 1 - End of Period Analysis
The master schedule is a workflow in the scheduling system that contains all batch jobs of the end-of-day processing on the core system. This use case is intended to show runtime changes for the entire end-of-day processing, taking into account the maintenance activities carried out on the core applications (e.g. deployment of a new release) and the company-wide maintenance windows (e.g. firewall or storage changes).

Main tasks:
- Load csv files
- Data selection and various data conversions
- Joining data sets
- Visualize data
- Analyze result

### Use Case 2 - Slow Poison
A sudden and significant runtime increase of a batch job raises alerts through the monitoring application. But there are batch processes with a small but regular runtime increase that are not detected or only detected by chance. Over a long period of time, such jobs may lead to operational issues. The aim of this use case is to systematically identify such processes so that they can be investigated early.

Main tasks:
- Define overall concept and criterias
  - Median is used to calculate the average runtime because it is more robust against outliers
  - Current quarter is compared with the three previous quarters
  - At least three successful executions per batch job and quarter (for median calculation)
  - Runtime between two quarters must increase by at least 3%. This increase must also exist between all compared quarters
  - Median per job in the current quarter must be at least 600 seconds (shorter runtimes have too little of an effect)
- Load csv files
- Data selection and various data conversions
- Filter data according to criterias
- Various data aggregations
- Pivoting
- Visualize data

Sample:

<img src="https://github.com/0LIFR1/big-data-run-time-analytics/blob/main/slow_poison_anon.png">

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Built With

[![Apache Hadoop][apache-hadoop-shield]][apache-hadoop-url] [![Spark][spark-shield]][spark-url]\
[![Python][python-shield]][python-url] [![Pandas][pandas-shield]][pandas-url] [![Matplotlib][matplotlib-shield]][matplotlib-url]

<!-- Logo examples
<div>
	<code><img height="50" src="https://user-images.githubusercontent.com/25181517/183914128-3fc88b4a-4ac1-40e6-9443-9a30182379b7.png" alt="Jupyter Notebook" title="Jupyter Notebook" /></code>
	<code><img height="50" src="https://user-images.githubusercontent.com/25181517/183423507-c056a6f9-1ba8-4312-a350-19bcbc5a8697.png" alt="Python" title="Python" /></code>
</div>
-->

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Roadmap
There is still room for improvement :-), some ideas:
- Automate data pipeline
- Optimize some of the code
- Make visualisations look nicer (e.g. usage of Tableau)

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/github_username/repo_name.svg?style=for-the-badge
[contributors-url]: https://github.com/github_username/repo_name/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/github_username/repo_name.svg?style=for-the-badge
[forks-url]: https://github.com/github_username/repo_name/network/members
[stars-shield]: https://img.shields.io/github/stars/github_username/repo_name.svg?style=for-the-badge
[stars-url]: https://github.com/github_username/repo_name/stargazers
[issues-shield]: https://img.shields.io/github/issues/github_username/repo_name.svg?style=for-the-badge
[issues-url]: https://github.com/github_username/repo_name/issues
[license-shield]: https://img.shields.io/github/license/github_username/repo_name.svg?style=for-the-badge
[license-url]: https://github.com/github_username/repo_name/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/linkedin_username
[product-screenshot]: images/screenshot.png
[linux-shield]: https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black
[linux-url]: https://www.linux.org/
[rstudio-shield]: https://img.shields.io/badge/R-276DC3?style=for-the-badge&logo=r&logoColor=white
[rstudio-url]: https://posit.co/
[jupyter-shield]: https://img.shields.io/badge/Jupyter-F37626.svg?&style=for-the-badge&logo=Jupyter&logoColor=white
[jupyter-url]: https://jupyter.org/
[python-shield]: https://img.shields.io/badge/Python-FFD43B?style=for-the-badge&logo=python&logoColor=blue
[python-url]: https://www.python.org/
[scikit-learn-shield]: https://img.shields.io/badge/scikit_learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white
[scikit-learn-url]: https://scikit-learn.org/stable/
[apache-hadoop-shield]: https://img.shields.io/badge/Apache%20Hadoop-6CF?logo=apachehadoop&logoColor=fff&style=for-the-badge
[apache-hadoop-url]: https://hadoop.apache.org/
[spark-shield]: https://img.shields.io/badge/Apache_Spark-FFFFFF?style=for-the-badge&logo=apachespark&logoColor=#E35A16
[spark-url]: https://spark.apache.org/
[cassandra-shield]: https://img.shields.io/badge/Cassandra-1287B1?style=for-the-badge&logo=apache%20cassandra&logoColor=white
[cassandra-url]: https://cassandra.apache.org/_/index.html
[pandas-shield]: https://img.shields.io/badge/Pandas-2C2D72?style=for-the-badge&logo=pandas&logoColor=white
[pandas-url]: https://pandas.pydata.org/docs/index.html
[numpy-shield]: https://img.shields.io/badge/Numpy-777BB4?style=for-the-badge&logo=numpy&logoColor=white
[numpy-url]: https://numpy.org/
[matplotlib-shield]: https://img.shields.io/badge/Matplotlib-%23ffffff.svg?style=for-the-badge&logo=Matplotlib&logoColor=black
[matplotlib-url]: https://matplotlib.org/
