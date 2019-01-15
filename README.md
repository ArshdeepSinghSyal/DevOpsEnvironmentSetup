# HW0-DevOps

#### Name: Arshdeep Singh Syal
#### Unity Id: asyal
#### Link to screencast video: https://drive.google.com/file/d/1j61B-rnTEHbqhJeddvYQnJkrKizEYr0X/view?usp=sharing

I have set up a delivery pipeline with git hooks using shell commands in this homework.

A delivery pipeline is a workflow system for building, validating, and deploying changes into a production environment. 

1) Created profiles on Mattermost, Stack Overflow & edited profile on Moodle as per mentioned requirments.

#### Moodle: https://moodle-courses1819.wolfware.ncsu.edu/user/profile.php?id=131751
#### Mattermost (username): asyal
#### Stack Overflow: https://stackoverflow.com/users/10893282/arshdeep-singh-syal

2) Created private repository called "HW0-DevOps" on NCSU's GitHub and added the TAs and instructor as a collaboratorors.

3) Before working on building the pipeline, we need to perform opunit checks, for which we need to install opunit.(Before installing opunit install node.js on the machine)

Opunit is a simple tool for verifying the configuration of a machine.

Opunit Install using the following command:

```npm install opunit -g```

Now, to perform opunit checks, run the following command:

```opunit profile CSC-DevOps/profile:519.yml```

This command basically checks my local systems configuration against a course profile.
#### Oppunit Checks:

<img width="823" alt="screenshot 2019-01-14 at 12 38 20 pm" src="https://media.github.ncsu.edu/user/12952/files/622c5180-1851-11e9-89b4-0c1f226b8e4c">

In case we get any of the opunit checks failing, which will be denoted by :x:<br/>
We update settings as required and update the tools, to their latest versions.

Then we clone this repo with the followong command:

```git clone --recursive https://github.com/CSC-DevOps/Pipelines```

<img width="1068" alt="screenshot 2019-01-14 at 2 53 03 pm" src="https://media.github.ncsu.edu/user/12952/files/32d31000-1864-11e9-8819-ebf9604ca027">

To check our progress ie. to check for existing issues with the current setup, we run the following command from the Pipelines directory:

```opunit verify local```

<img width="993" alt="screenshot 2019-01-14 at 3 00 49 pm" src="https://media.github.ncsu.edu/user/12952/files/52b70380-1865-11e9-8bce-9dd98563356f">

Now we begin creating a simple hook.

A hook is used to specify what happens, in response to the occourance of an event. The outcome of a hook can be used to trigger other events. Hence, hooks may be used to create a simple pipeline.

Inside a new directory ```mkdir hook-demo```, we create a new git repository with ```git init```.

We then create a "post-commit" file located in "hook-demo/.git/hooks/post-commit". 

<img width="196" alt="screenshot 2019-01-14 at 4 05 43 pm" src="https://media.github.ncsu.edu/user/12952/files/ee00a680-186e-11e9-83be-c2e0bb8fa05e">

Then we run the ```chmod +x post-commit``` to make the post-commit file an executable file.

<img width="632" alt="screenshot 2019-01-14 at 4 07 04 pm" src="https://media.github.ncsu.edu/user/12952/files/ee00a680-186e-11e9-93fd-3327b54cad01">

We then trigger the commit by create a simple commit in hook-demo.

```
touch demo; 
git add demo; 
git commit -m "init";
```

<img width="422" alt="screenshot 2019-01-14 at 4 09 40 pm" src="https://media.github.ncsu.edu/user/12952/files/ee00a680-186e-11e9-9f3c-fc005597e013">

We see a webpage pop open.

<img width="1440" alt="screenshot 2019-01-14 at 4 14 50 pm" src="https://media.github.ncsu.edu/user/12952/files/8a2aad80-186f-11e9-8ff9-ce959a3bc73c">

4) Now we begin creating our simple pipeline
Using the node.js application in the App directory, we setup the app locally by running ```npm install```

We run ```git checkout master``` which allows us to git things to the master branch.

Then we run ```npm start```:

<img width="625" alt="screenshot 2019-01-15 at 1 18 23 am" src="https://media.github.ncsu.edu/user/12952/files/7a38bb00-18bb-11e9-8084-012b911b0895">

We see the following, at http://localhost:5001.

<img width="505" alt="screenshot 2019-01-15 at 1 27 05 am" src="https://media.github.ncsu.edu/user/12952/files/c7695c80-18bc-11e9-8544-792581e4640c">

Then we run the test with ```npm test``` to check if the 2 tests to pass.

<img width="545" alt="screenshot 2019-01-15 at 1 23 33 am" src="https://media.github.ncsu.edu/user/12952/files/4611ca00-18bc-11e9-9825-e8f97334d301">

Now, we add a test stage by adding a "pre-commit" hook for the App directory which cancels a commit on failing of npm test.(Hooks for App directory are stored in .git/modules/App/hooks as App is a submodule)

<img width="457" alt="screenshot 2019-01-15 at 1 39 36 am" src="https://media.github.ncsu.edu/user/12952/files/70fd1d80-18be-11e9-89e8-a0a718f9adc0">

<img width="327" alt="screenshot 2019-01-15 at 1 38 06 am" src="https://media.github.ncsu.edu/user/12952/files/3b583480-18be-11e9-8cc9-21eb128a7f8c">

We then modify the message in App/main.js from "Hi From" to "Bye From".

<img width="338" alt="screenshot 2019-01-15 at 1 47 11 am" src="https://media.github.ncsu.edu/user/12952/files/7f980480-18bf-11e9-8ad5-54c345b939da">

<img width="686" alt="screenshot 2019-01-15 at 1 43 11 am" src="https://media.github.ncsu.edu/user/12952/files/f08aec80-18be-11e9-9159-0f96094f871c">

<img width="692" alt="screenshot 2019-01-15 at 1 44 28 am" src="https://media.github.ncsu.edu/user/12952/files/1e703100-18bf-11e9-8254-4b7a7eadc23a">

Then we try to commit the file using the following commands:
```
git add main.js; 
git commit -m "checkin";
```
We observe that the tests fail, preventing the commit from being added.

<img width="480" alt="screenshot 2019-01-15 at 1 49 47 am" src="https://media.github.ncsu.edu/user/12952/files/dd2c5100-18bf-11e9-9e54-ca39f2ffd81c">

Now we add an install and deploy stage

We need to create a new directory "deploy" and two sub-directory:

deploy/production.git — remote repository.
deploy/production-www — holds the contents of our deployed web app.

We make production.git a bare repository (repository without a working tree)
Bare repository only holds git objects, from which code can be extracted as needed. 
Using bare repository helps avoids having merge issues on production server.

In production.git, we run git ```init --bare``` to initialize it as a bare repository.

<img width="677" alt="screenshot 2019-01-15 at 2 06 32 am" src="https://media.github.ncsu.edu/user/12952/files/32696200-18c2-11e9-84a1-4258a16a31eb">

To hold the current version of software, we use production-www, extract it from the bare repository using git checkout and we use the "post-receive" event, to create a hook to perform the git checkout operation for us.

<img width="393" alt="screenshot 2019-01-15 at 2 12 15 am" src="https://media.github.ncsu.edu/user/12952/files/fedb0780-18c2-11e9-808d-39c655bdbc94">

We create the following post-receive hook for production.git:

<img width="355" alt="screenshot 2019-01-15 at 2 13 17 am" src="https://media.github.ncsu.edu/user/12952/files/25993e00-18c3-11e9-9776-ac80479960a8">

This command copies over the content of the latest code in production.git into production-www, and installs the appropriate dependencies for our web app.

This script does not run the web app, inorder to do that we install pm2, by running npm '''install pm2 -g'''. (pm2 will ensure that the web app will stay running, even if it crashes)

<img width="555" alt="screenshot 2019-01-15 at 2 19 54 am" src="https://media.github.ncsu.edu/user/12952/files/11097580-18c4-11e9-9889-cd352999b046">

We then add the following steps to our script, after npm install:
npm run stop
npm run start

<img width="353" alt="screenshot 2019-01-15 at 2 16 40 am" src="https://media.github.ncsu.edu/user/12952/files/9d676880-18c3-11e9-9443-8171cc3ed589">

Now, to link the App repository with the remote production.git repository.

Inside the App directory, we run the following commands:

```git remote add prod ../deploy/production.git```

<img width="563" alt="screenshot 2019-01-15 at 2 26 12 am" src="https://media.github.ncsu.edu/user/12952/files/f2f04500-18c4-11e9-817d-dd2f471d690e">

We then ppdate the message, to be "Hi From production".

<img width="684" alt="screenshot 2019-01-15 at 2 24 47 am" src="https://media.github.ncsu.edu/user/12952/files/c0464c80-18c4-11e9-821f-a30c4fcf1fb8">

We then commit the changes locally.

<img width="470" alt="screenshot 2019-01-15 at 11 26 52 am" src="https://media.github.ncsu.edu/user/12952/files/bfd3a300-1910-11e9-90e7-112bce2c0c01">

Finally, we push changes in App to remote repository using the following command:

```git push prod master```

<img width="751" alt="screenshot 2019-01-15 at 11 25 57 am" src="https://media.github.ncsu.edu/user/12952/files/bba78580-1910-11e9-9ed0-985f9cb03476">

We see the following, at http://localhost:5001.

<img width="594" alt="screenshot 2019-01-14 at 2 57 02 am" src="https://media.github.ncsu.edu/user/12952/files/4a2ee080-1805-11e9-80e5-2da2dd291aa5">

To check our progress, we run the following command from the Pipelines directory again.

```opunit verify local```

<img width="997" alt="screenshot 2019-01-15 at 6 22 54 am" src="https://media.github.ncsu.edu/user/12952/files/137cc700-18e6-11e9-97d5-7cd912850448">

This time we observe that the delivery pipeline passes all the checks.

Hence we have successfully set up a simple delivery pipeline, consisting of git hooks and shell commands and have deployed a web app using it. This pipeline runs tests, installs, and "deploys" an application into production based on a commit.
