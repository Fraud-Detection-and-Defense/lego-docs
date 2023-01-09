# lego-docs

## Contents
- [lego-docs](#lego-docs)
  - [Contents](#contents)
  - [Introduction](#introduction)
    - [What is Sybil defense?](#what-is-sybil-defense)
    - [What are Legos?](#what-are-legos)
  - [What does a lego look like?](#what-does-a-lego-look-like)
  - [What Legos are already available?](#what-legos-are-already-available)
  - [Building Legos](#building-legos)
    - [How do I build a Lego?](#how-do-i-build-a-lego)
    - [Lego spec](#lego-spec)
      - [Inputs](#inputs)
      - [Containerization](#containerization)
        - [Containeriation using Docker:](#containeriation-using-docker)
        - [What is Docker?](#what-is-docker)
        - [Why use Docker?](#why-use-docker)
        - [Containerization using Docker: Tutorial](#containerization-using-docker-tutorial)
    - [Contribution guidelines](#contribution-guidelines)
    - [Handling Gitcoin data](#handling-gitcoin-data)
    - [Documenting a new Lego](#documenting-a-new-lego)
  - [Roadmap](#roadmap)
    - [Lego ideas](#lego-ideas)
    - [UX/UI](#uxui)
    - [Performance](#performance)
  - [Downloads](#downloads)
  - [Lego Documentation](#lego-documentation)
    - [Gitcoin passport](#gitcoin-passport)
    - [Levenstein Distance](#levenstein-distance)
    - [Shared IP](#shared-ip)
    - [SAD model](#sad-model)
    - [DonorDNA](#donordna)
    - [GrantDNA](#grantdna)
    - [Onchain Intersectionality](#onchain-intersectionality)
  - [Resources](#resources)
    - [FAQs](#faqs)
    - [Read/Watch/Listen](#readwatchlisten)


## Introduction

### What is Sybil defense?

Sybils are "fake" users. They are users that do not represent real humans. Sybils are created in order to make a single human appear to be many in order to have outsized weight in a voting protocol or to receive more than a single person's worth of some reward (e.g. an airdrop). These Sybils should be eliminated from a fair voting/funding protocol, but theyare no always easy to detect.

![honest user vs Sybil](/assets/man-with-multiple-shadows.png)

Do Androids Dream of Electric Sheep tells the story of a detective tasked with eliminating humanoid "replicants" that are almost indistinguishable from natural humans. They do this using a system of tests, including an instrumented interview that look for subtle "tells" such as a limited ability to make complex moral judgments in hypothetical scenarios. Sybil defenders are similarly tasked with distinguishing real and virtual humans in a mixed population where they are difficult to tell apart. They too look for subtle "tells" that give Sybils away. Sometimes the Sybil signals are obvious and unambiguous, sometimes they are not. The additional complication for Sybil hunters is that the entire population exists in a digital space where a human's physical existence cannot be proven by their presence- it can only be demonstrated using forgeable proxies. Reliably linking actions to identities is therefore a subtle science that pieces together multiple lines of evidence to build a personhood profile.

For Gitcoin grants, Sybil detection is extremely important because minimizing the influence of Sybils creates a funding environment that more accurately represents the true preferences of the community of donors. Sybils skew the allocated funds in favour of individual projects to benefit some specific user or group, rather than efficiently distributing funds to genuine public goods. Gitcoin aims to solve for one-human one-vote, while Sybils actuively try to subvert that and unfairly allocate more votes to fewer humans.

To date, Sybil defense has been executed by a small group of Gitcoin data scientists manually applying algorithms to user data and reviewing disputes. Now, as Gitcoion becomes a protocol, Sybil defense will be executed in a more decentralized way. This requires composable tools for Sybil defense that can be applied to open data. These composable tools are known as Sybil defense Legos because they can be recombined and reconfigured to built bespoke defense strategies fit for specific purposes.

### What are Legos?

Gitcoin is decentralizing by converting the core Sybil defense functions into a set of tools that can easily be implemented by users or eventually forked and recombined in creative ways in other projects. This requires the Sybil defense procedures currently managed by humans to be broken down into discrete units, defined in code, documented and made accessible as composable building blocks. These are known as "Legos". Lego bricks are simple building blocks that can be connected to each other in creative combinations to form all kinds of structures or even machines that are much more complex than their component parts. Similarly, modular, composable software tools can be used to build imaginative systems for defending against Sybils. 

![](https://i.imgur.com/kAEnsYf.png)

For Gitcoin grants, Legos start as useful insights from analysis of Gitcoin data - some metric that reveals users to be Sybils. Then, this finding is expressed algorithmically and turned into some executable code. At the moment, most Legos exist in this form - shareable scripts in a Github repository. However, the ideal scenario is to make these Legos executable with no coding required, probably through a web interface where Lego's can be selected to be executed remotely, returning a simple result to the user. 

## What does a lego look like?

A "Lego"is a discrete unit that performs one, specific function in the Gitcoin protocol. It should work as a building block, meaning that it should be deployable on its own, taking well defined inputs and returning some known outputs. It should also connect to other Legos, which requires some standardization of types and formats for inputs and outputs so that tools can be chained together in intuitive pipelines. Making these Lego's available empowers the community to build on top of them and saves developers from having to repeatedly reinvent the wheel when building out new products.

For a truly composable Lego, the code should be:

- **Tightly scoped**: the tool should fulfill one single function without side-effects so that it can be deployed in a variety of contexts with reliable outcomes.
- **Free and open**: open source codes that is publicly available, auditable, able to run on normal consumer hardware.
- **Permissionless**: not requiring special credentials or licenses to view, download or deploy, and users have the ability to fork the code any time.
- **Accessible**: sufficiently well-documented and with intuitive UX to enable a wide community of users
- **Minimal dependencies**: protect the "supply chain" by minimizing the dependencies. Where dependencies are unavoidable, bundle them or make them very easy to access.
- **Modular**: uses common formats and types so that outputs of one Lego can become inputs to another in pipelines - i.e. the legos are designed to be used as building blocks for larger systems with no specific predetermined structure.
- **Open governance**: Decisions about the development of the Lego's should not be gated by individuals or centralized groups - instead governance should be open so that users can trust that the code will be developed and maintained with integrity and community participation. 

Some examples of Lego's that conform to these norms are smart contracts on Ethereum. Smart contracts, or even individual functions of smart contracts, can be forked and rewritten, or stacked on top of each other in creative ways to build new protocols. This is common practise in DeFi, where primitives such as asset borrowing, lending and staking contracts are combined in many different ways by teams aiming to create protocols optimized for yield, or resilience, or security. Token standards such as ERC-20 (Ethereum token standard) and ERC-721 (Ethereum NFT standard) are composable primitives that can be built on top of - there is a huge diversity of token and NFT projects built on top of these original standards, often in combination with DeFi Legos, creating a diverse landscape of decentralized financial products and a community with freedom and agency to create new versions and implement new ideas.

We want to bring that freedom and agency to public goods funding. Rather than being centralized overseers of public goods funding, we want to share tools that empower the community to do it in clever and creative new ways.

## What Legos are already available?

Several Lego's are already being used to manage Sybils in Gitcoin grants. These are:

- **Gitcoin Passport:** When a user connects a passport, a trust score can be calculated for them which is used as evidence of personhood - the greater the score the more likely they are to be a genuine user.
- **Levenstein distance:** Every user has a username - when they sign up to Gitcoin grants the similarity of their name can be compared against all other usernames to generate a likelihood of the username being auto-generated - evidence of a Sybil account. This Lego **will be deprecated** in the grants protocol because usernames will no longer be available - only Ethereum addresses, wallet IDs and grant/round nonce. 
- **Shared IP**: User IP addresses can also be checked to see if they are shared with many other users. Lots of addresses originating from the same IP could be a marker for Sybil attackers.
- **SAD model:** The user also has a Gitcoin account whose history can be analyzed using the SAD model to give another Sybil-likelihood score.
- **DonorDNA**: When a donor connects their wallet their profile of past donations can be analyzed to see whether it is similar to groups of other users, which may be indicatative of Sybil rings.
- **GrantDNA**: Each grant has a set of donors that can be represented as a set of binary data. This can be used to compare grants against flagged grants to see if they have similar donor profiles.
- **Onchain Intersectionality**: How many out of a set of on-chain credentials does a user have?

The outputs from these Legos are collated into a single dataset where each user has a Sybil likelihood as measured across several dimensions. A threshold value that separates "suspicious" and "not suspicious" users can be applied to each metric individually such that the final dataset is a set of Booleans for each user, and the final decision about whether to omit or allow a particular user is a simple summation (e.g. if sum > 3, squelch). Alternatively, the actual value from each metric can be propagated to the final dataset and a (weighted) average applied there to identify Sybils. Either way, the outputs from the Legos themselves are aggregated and used collectively to come to a decision about the trustability of the user. In summary, the Legos are run independently and the results passed to an aggregator. The user sees the result of each independent Lego and also the result of the aggregator - i.e. they get an overall Sybil likelihood score/trust score and also a break down of the individual Sybil "dimensions".


## Building Legos

### How do I build a Lego?

### Lego spec

This section details the desired properties for a new Lego.

#### Inputs

The Lego should only require some subset of the following data as inputs:

  - Ethereum address: User's Ethereum address
  - Passport ID: User's Gitcoin passport digital identifier
  - Grant round nonce: A counter that tracks the number of donations a user has made in a round 

#### Containerization

Containerization is the packaging of software code with just the operating system (OS) libraries and dependencies required to run the code to create a single lightweight executable—called a container—that runs consistently on any infrastructure. More portable and resource-efficient than [virtual machines (VMs)](https://www.ibm.com/topics/virtual-machines), containers have become the de facto compute units of modern cloud-native applications. Containerization allows developers to create and deploy applications faster and more securely. With traditional methods, code is developed in a specific computing environment which, when transferred to a new location, often results in bugs and errors.

The concept of containerization and process isolation is actually decades old, but the emergence in 2013 of the open source Docker engine, an industry standard for containers with simple developer tools and a universal packaging approach—accelerated the adoption of this technology.

##### Containeriation using Docker:

Step 1: Application structure

Step 2: Build/Import codes for containerization.

Step 3: Outlining key requirements

Step 4: Create a docker file

Step 5: Perform the docker compose

Step 6: Building and testing

##### What is Docker?

Docker is “a computer program that performs operating-system-level virtualization, also known as ‘containerization’” Wikipedia. As any first line of a Wikipedia article about tech, this sentence is obscure to anyone not already familiar with the content of the article.

So, to put it more simply, Docker is a program that allows to manipulate (launch and stop) multiple operating systems (called containers) on your machine (your machine will be called the host). Just imagine having 10 RaspberryPi with different flavors of Linux, each focused on doing one simple thing, that you can turn on and off whenever you need to ; but all of this happens on your computer.

##### Why use Docker?

Docker is designed to enclose environments inside an image / a container. What this allows, for example, is to have a Linux machine on a Macbook, or a machine with R 3.3 when your main computer has R 3.5. Also, this means that you can use older versions of a package for a specific task, while still keeping the package on your machine up-to-date.

This way, you can “solve” dependencies issues: if ever you are afraid dependencies will break your analysis when packages are updated, you can build a container that will always have the software versions you desire: be it Linux, R, Python or any other software package.

##### Containerization using Docker: Tutorial

Here are the prerequisites:

- Basic understanding of R and [Flask.](https://flask.palletsprojects.com/en/2.2.x/)
- Basic understanding of the command line.
- A code editor (IDE) such as VS Code or R studio.

Install Docker and Docker Compose via the links below:

- [Docker](https://www.section.io/engineering-education/how-to-containerize-a-python-application/www.docker.com)
- [Docker Compose](https://docs.docker.com/compose/)

Note that this tutorial assumes the user wants to use a preconfigured official R image. There are many alternatives - search the [Docker Hub](https://hub.docker.com/) for images that suit your specific needs.

**Docker image Vs Docker containers**

On your machine, you’re going to need two things: images, and containers. Images are the definition of the OS, while the containers are the actual running instances of the images. You’ll need to install the image just once, while the containers are to be launched whenever you need this instance. And of course, multiple containers of the same images can be run at the same time. To compare with R, this is the same principle as installing vs loading a package: a package is to be downloaded once, while it has to be launched every time you need it. And a package can be launched in several R sessions at the same time easily.

So to continue with this metaphore: we’re building an image when we’re install.packages(), and we run the image when we library().

**Docker File**

A Docker image is built from a Dockerfile. This file is the configuration file, and describes several things: from what previous docker image you are building this one, how to configure the OS, and what happens when you run the container. In a sense, it’s a little bit like the DESCRIPTION + NAMESPACE files of an R package, which describes which are the dependencies to your package, gives meta information, and states which functions and data are to be available to the users library()ing the package.

So, let’s build a very basic Dockerfile for R, focused on reproducibility. The idea is this one: I have today an analysis that works (for example contained in a .R file), and I want to be sure this analysis will always work in the future, regardless of any update to the packages used.

So first, create a folder for your analysis, and a Dockerfile:

```jsx
*mkdir ~/mydocker*
```

```jsx
*cd ~/mydocker*
```

```jsx
*touch Dockerfile*
```

And let’s say this is the content of the analysis we want to run, called myscript.R, and located in the ~/mydocker folder:

```jsx
*library(tidystringdist)*
```

```jsx
*df <- tidy_comb_all(iris, Species)*
```

```jsx
*p <- tidy_stringdist(df)*
```

```jsx
*write.csv(p, "p.csv")*
```

**FROM**

Every Dockerfile starts with a FROM, which describes what image we are building our image from. There are a lot of official images, and you can also build from a local one.

This FROM is, in a way, describing the dependency of your image ; just as in R, when building a package, you always rely on another package (be it only the {base} package).

If you’re going for an R based image, Dirk Eddelbuettel & Carl Boettiger are maintaining rocker, a collection of Docker images for R you can use. The basic image is rocker/r-base, but what we want is our image to be reproducible: that is to say to rerun the exact same way anytime we run it. For this, we’ll be using rocker/r-ver, which are Docker images containing a fixed version of R (back to 3.1.0), and that you can run as if from a specific date. So what we’ll do is look up the image corresponding to the R version we want. You can get your current R Version with:

```jsx
*R.Version()$version.string*
```

```jsx
*## [1] "R version 3.6.1 (2019-07-05)"*
```

```jsx
So, let’s start the Dockerfile with:
```

```jsx
*FROM rocker/r-ver:3.4.4*
```

**RUN**

Once we’ve got that, we’ll add some RUN statements: these are commands which mimic command line commands. we’ll create a directory to receive our analysis.

```jsx
*FROM rocker/r-ver:3.4.4*
```

```jsx
*RUN mkdir /home/analysis*
```

**Install our package**

The command to make R execute something, from the terminal, is R -e "my code". Let’s use it to install our script dependencies, but from a specific date. We’ll mimic the way rocker/r-ver works when building from a specific date: setting the options("repos") to this specific date, using the MRAN image: in other word, using a repo url like https://mran.microsoft.com/snapshot/1979-01-01.

```jsx
*FROM rocker/r-ver:3.4.4*
```

```jsx
*RUN mkdir /home/analysis*
```

```jsx
*RUN R -e "options(repos = \*
```

```jsx
*list(CRAN = 'http://mran.revolutionanalytics.com/snapshot/2019-01-06/')); \*
```

```jsx
*install.packages('tidystringdist')"*
```

**Making it more programmable with ARG**

In our last Dockerfile, the date can’t be modified at build time - something we can change if we use an ARG variable, that will be set when we’ll do docker build, with --build-arg WHEN=

```jsx
*FROM rocker/r-ver:3.4.4*
```

```jsx
*ARG WHEN*
```

```jsx
*RUN mkdir /home/analysis*
```

```jsx
*RUN R -e "options(repos = \*
```

```jsx
*list(CRAN = 'http://mran.revolutionanalytics.com/snapshot/${WHEN}')); \*
```

```jsx
*install.packages('tidystringdist')"*
```

Here, the {tidystringdist} that will be installed in the machine will be the one from the date we will specify when building the container, even if we build this image in one year, or two, or four.

**COPY**

Now, I need to get the script for my analysis from my machine (host) to the container. For that, we’ll need to use COPY localfile pathinthecontainer. Note that here, the myscript.R has to be in the same folder as the Dockerfile on your computer.

```jsx
*FROM rocker/r-ver:3.4.4*
```

```jsx
*ARG WHEN*
```

```jsx
*RUN mkdir /home/analysis*
```

```jsx
*RUN R -e "options(repos = \*
```

```jsx
*list(CRAN = 'http://mran.revolutionanalytics.com/snapshot/${WHEN}')); \*
```

```jsx
*install.packages('tidystringdist')"*
```

```jsx
*COPY myscript.R /home/analysis/myscript.R*
```

**CMD**

Now, CMD, which is the command to be run every time you launch the docker. What we want is myscript.R to be sourced.

```jsx
*FROM rocker/r-ver:3.4.4*
```

```jsx
*ARG WHEN*
```

```jsx
*RUN mkdir /home/analysis*
```

```jsx
*RUN R -e "options(repos = \*
```

```jsx
*list(CRAN = 'http://mran.revolutionanalytics.com/snapshot/${WHEN}')); \*
```

```jsx
*install.packages('tidystringdist')"*
```

```jsx
*COPY myscript.R /home/analysis/myscript.R*
```

```jsx
*CMD R -e "source('/home/analysis/myscript.R')"*
```

**Build, and run**

**Build**

Remember what we want: an image that will, ad vitam aeternam, run an analysis as if we were still today. To do this, we’ll use the --build-arg WHEN= argument for the docker build. Just after the =, put the date you want your analysis to be run from.

Now, go and build your image. From your terminal, in the directory where the Dockerfile is located, run:

```jsx
*docker build --build-arg WHEN=2019-01-06 -t analysis .*
```

- t name is the name of the image (here analysis), and . means it will build the Dockerfile in the current working directory.

**Run**

Then, just launch with:

```jsx
*docker run analysis*
```

And your analysis will be run

**Export container content**

One thing to do now: you want to access what is created by your analysis (here p.csv) outside your container ; i.e, on the host. Because yes, as for now, everything that happens in the container stays in the container. So what we need is to make the docker container share a folder with the host. For this, we’ll use what is called Volume, which are (roughly speaking), a way to tell the Docker container to use a folder from the host as a folder inside the container.

That way, everything that will be created in the folder by the container will persist after the container is turned off. To do this, we’ll use the -v flag when running the container, with path/from/host:/path/in/container. Also, create a folder to receive the results in both :

```jsx
*FROM rocker/r-ver:3.4.4*
```

```jsx
*ARG WHEN*
```

```jsx
*RUN mkdir /home/analysis*
```

```jsx
*RUN R -e "options(repos = \*
```

```jsx
*list(CRAN = 'http://mran.revolutionanalytics.com/snapshot/${WHEN}')); \*
```

```jsx
*install.packages('tidystringdist')"*
```

```jsx
*COPY myscript.R /home/analysis/myscript.R*
```

```jsx
*CMD cd /home/analysis \*
```

```jsx
*&& R -e "source('myscript.R')" \*
```

```jsx
*&& mv /home/analysis/p.csv /home/results/p.csv*
```

```jsx
*mkdir ~/mydocker/results*
```

```jsx
*docker run -v ~/mydocker/results:/home/results  analysis*
```

```jsx
Wait for the computation to be done, and…
```

```jsx
*ls ~/mydocker/results*
```

```jsx
*P.csv*
```

**What to do next?**

So now, every time you’ll launch this Docker image, the analysis will be performed and you’ll get the result back. With no problem of dependencies: the packages will always be installed from the day you desire. Although, this can be a little bit long to run as the packages are installed each time you run the container. But as I said in the Disclaimer, this is a basic introduction to Docker, R and reproducibility, so the goal was more to get beginners on board with Docker :)

Other things you can do would be:

- Use remotes::install_version() if you want your analysis to be based on package version instead of a time based installation	.

```jsx
*FROM rocker/r-ver:3.4.4*
```

```jsx
*RUN R -e "install.packages('remotes'); \*
```

```jsx
*remotes::install_version('tidystringdist', '0.1.2')"*
```

```jsx
*…*
```

- Use the Volume trick to bring data into your container, so that any data will be analysed in the very same environment.

### Contribution guidelines

### Handling Gitcoin data

### Documenting a new Lego



## Roadmap
### Lego ideas
### UX/UI
### Performance

## Downloads

Add links to gitcoin data downloads here

## Lego Documentation
### Gitcoin passport
### Levenstein Distance
### Shared IP
### SAD model
### DonorDNA
### GrantDNA
### Onchain Intersectionality


## Resources
### FAQs
### Read/Watch/Listen