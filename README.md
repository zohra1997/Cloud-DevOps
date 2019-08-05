---


---

<h1 id="cloud-devops">Cloud DevOps</h1>
<h2 id="introduction">Introduction</h2>
<p>This repository breaks down the steps on how to deploy a project to amazon server. I have developed a REST API for trading which I would be deploying to AWS, the GitHub URL is: <a href="https://github.com/zohra1997/Trading-App">https://github.com/zohra1997/Trading-App</a><br>
Trading app is an online stock trading simulation REST API which can be used to check stock market, create a user account, deposite and withdraw money, buy and sell stocks. This REST API can be utilized by front-end developers, mobile-app developers, and traders.  It is a MicroService which is implememnted in Java with SpringBoot, PSQL database, IEX market Data and Http pooling connection manager.</p>
<h1 id="docker-architecture-diagram">Docker Architecture Diagram</h1>
<p>Following is the docker architecture of the trading application.<br>
<img src="https://lh3.googleusercontent.com/FeWLM0Skp6pwbhI9RhRxhKLfZMyg9Wrg-ukrqLGgJoJrNq8-6kGzEsr758xn4g01wtuLc72v2Gw" alt="enter image description here"><br>
To dokcerize the applicatoin the following steps should be followed in order.</p>
<ol>
<li>Docker psql database Image: is a standalone, executable package that containes all the tables and dependencies of the database.<br>
(4) <code>docker build -t jrvs-psql</code></li>
<li>Docker Trading App image: is a lighwieght, executable package that containes codes and all other dependencies of the application.<br>
(5) <code>docker build -t trading-app</code></li>
<li>Network Bridge: connects psql database to application.<br>
(3)<code>docker network create --driver bridge trading-net</code></li>
<li>Docker jrvs-psql container:<br>
(2) <code>dcoker run --rm --name jrvs-psql -e POSTGRES_PASSWORD=psql-password -e POSTGRES_DB=jrvstrading -e POSTGRES_USER=postgres-user --network trading-net -d -p 5432:5432 jrvs-psql</code></li>
<li>Docker trading-app container:<br>
(1)<code>IEX_TOKEN="your-token" dcoker run -e "PSQL_URL=jdbc://postresql://jrvs-psql:5432/jrvstrading" -e "PSQL_USER=psql-user" -e "PSQL_PASSWORD=psql-password" -e "IEX_PUB_TOKEN=${IEX_TOKEN}" --network trading-net -p 8080:8080 -t trading-app</code></li>
</ol>
<h1 id="cloud-architecture-diagram">Cloud Architecture Diagram</h1>
<p><img src="https://lh3.googleusercontent.com/T7sqWjzw2XZs1SZ-bFWfF6A53hyoFdzQmH_dJTT1HKNgrLafLGvZOaQdmWIJP3Xi68XZoX2l8s8" alt="enter image description here"><img src="https://picasaweb.google.com/106388341762798004438/6721791064472506625#6721791070538037714" alt="" title="cloud architecture"></p>
<h1 id="elastic-beanstalk-todo">Elastic Beanstalk (TODO)</h1>
<h1 id="jenkins-cicd-pipeline-todo">Jenkins CI/CD pipeline (TODO)</h1>

