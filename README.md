# Continuous Deployment

## Thing things needed
* Continuous testing
* Team notifications of broken builds
* Auto Deployment

## Continuous Testing
Testing is very important to continuous deployment.  Without it, you will break production often.  We use
Cucumber/Webkit for intergration tests and Jasmine for unit tests.  Once you have a test suite, you will need some
way to run them before deployment.  We use Github's Post-Receive hook to notify Concrete of a push to 'master'.
Concrete then runs our test suite.

    sudo apt-get install mongodb
    sudo apt-get install git
    sudo apt-get install nodejs
    sudo apt-get install npm
    sudo apt-get install build-essential
    sudo npm install -g forever
    sudo npm install -g concrete
    git clone https://github.com/Moveline/deployment-talk.git
    cd deployment-talk
    git config --add concrete.runner "npm test"
    concrete .
    forever start /usr/local/bin/concrete /home/ubuntu/deployment-talk

## Team notifications
Tests will fail.  So we need to know when they do.  Concrete executes a git hook after every test.  Our current fail
hook emails everyone on the team.  We have been playing around with the idea of having Hubot notify us in HipChat.

    ln -s build-failed .git/hook/build-failed

## Auto Deployment
Concrete has a success hook.  Since we use Heroku, our success hook is a simple 'git push'.

    ln -s build-worked .git/hook/build-worked


## Links
* https://help.github.com/articles/post-receive-hooks
* https://github.com/ryankee/concrete
* https://github.com/nodejitsu/forever