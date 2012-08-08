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

## Team notifications
Tests will fail.  So we need to know when they do.  Concrete executes a git hook after every test.  Our current fail
hook emails everyone on the team.  We have been playing around with the idea of having Hubot notify us in HipChat.

## Auto Deployment
Concrete has a success hook.  Since we use Heroku, our success hook is a simple 'git push'.

