This is a simple demonstration application used in the [Jenkins: The Definitive Guide](http://wakaleo.com/books/jenkins-the-definitive-guide) book.

## Building the project

The project is a simple multi-module Maven project. To build the whole project, just run `mvn install` from the root directory.

## Running the game

The application is a very simple online version of [Conway's 'game of life'](http://en.wikipedia.org/wiki/Conway's_Game_of_Life). To see what the game does, run `mvn install` as described above, then go to the gameoflife-web directory and run `mvn jetty:run`. The application will be running on http://localhost:9090.

## Running the acceptance tests

The acceptance tests are written using Webdriver and [Serenity (previously known as 'Thucydides')](http://thucydides.info). They are designed to run against a running server. Run the jetty instance as described about, then, in another window, go to the gameoflife-acceptance-tests directory and run `mvn clean verify`. The test reports will be generated in the `target/site/thucydides` directory.

Run the project using jenkins
----------------------------
To build the project :

1.create a free style job --game-build
2.give repo: https://github.com/rjshk013/gameoflife-jenkinsproject
3.In the build tab, click on invoke top level maven targets and type the below command:

compile

To test:

create one more Freestyle Project for unit testing.
Add the same repository URL in the source code management tab
in the "Build Trigger" tab click on the "build after other projects are built". 
type the name of the previous project (game-build) where we are compiling the source code, and you can select any of the below options:

    Trigger only if the build is stable
    Trigger even if the build is unstable
    Trigger even if the build fails

In the Build tab, click on invoke top level maven targets and use the below command:

test

Go to the Post-build Actions section and tick "Publish JUnit test result report" checkbox

Enter "**/target/surefire-reports/*.xml" in the "Test report XMLs" field

save & build the job

Create war file:
-----------------
Create one more freestyle project and add the source code repository URL
in the build trigger tab, select build when other projects are built
give previous test project job name
In the build tab, select shell script. Type the below command to package the application in a WAR file:

clean install or clean package

If you want to create all this steps in a single job ,do this steps & it will automatically compile ,test & create war file .
