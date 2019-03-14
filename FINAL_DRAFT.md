Web Application Tester - Workout of the Day

This exercise will let you show us how you create test suites and set up your testing environment.
The workout is meant to give you a feel for the kind of work that you will be performing in this position.

In this workout, there are a few different tasks which are aimed at different facets of web application testing.

1. Automated Selenium Tests

For this task you will be creating a selenium test to drive a browser and make an assertion about elements on the page.
You may use/configure any non-headless browser to complete this part.
You can use any Selenium WebDriver compatible framework but ideally the language should be JavaScript.

The requirements:

Write a JavaScript Driven Selenium WebDriver project to perform the following tasks:

- Visit the page https://education.nsw.gov.au/
- Click log in
- Click staff portal
- When it is presented with the username and password inputs, enter the text “wod” into both username and password input boxes.
- Assert that the span with id eror-text DOES exist on the page, otherwise fail the test.

import java.util.concurrent.TimeUnit;

import org.openqa.selenium.By;

import org.openqa.selenium.WebDriver;

import org.openqa.selenium.WebElement;

import org.openqa.selenium.firefox.FirefoxDriver;

import org.openqa.selenium.support.ui.ExpectedConditions;

import org.openqa.selenium.support.ui.WebDriverWait;


public class LoginDemo {

    public static void main(String[] args) {

            WebDriver driver = new FirefoxDriver();

            driver.manage().window().maximize();

            String url = "https://education.nsw.gov.au/";

            driver.get(url);

            driver.findElement(By.id("Log in")).click(); 
            driver.findElement(By.id("staff portal")).click(); 

            //driver.manage().timeouts().implicitlyWait(20, TimeUnit.SECONDS);      

            WebDriverWait wait=new WebDriverWait(driver, 20);               

            driver.findElement(By.id("Username").sendkeys("wod"); 
            driver.findElement(By.id("password").sendkeys("wod");   

            driver.manage().timeouts().implicitlyWait(50, TimeUnit.SECONDS);        

           boolean isEmpty = driver.findElements(By.xpath(textLocator)).isEmpty();
if (isEmpty) {  
   //Write to log that text is not present (PASS)
} else {
        //Write to log that text is present (FAIL)
} 

    }  

}

2. Node.JS Backend testing

In this task you will be writing a backend unit test.
Use either Mocha.js or Jasmine to write the test case.

The requirements:

- Write a test that asserts that the User Controller will return a list containing a user object with the following properties:

    {"id": 1, "username": "sample", "email": "sample@sample.com"}

- Mock out the user service so that the controller test only covers the User Controller and does not test the User Service.
- Make sure that we can install the testing dependencies using `npm install` and run the tests using `npm test`.

npm install mocha sinon
mkdir tests

var request = require('request');
var assert = require('assert');
var sinon = require('sinon');
var PassThrough = require('stream').PassThrough;
var http = require('http');
var api = require(../server');

describe('api',function(){
beforeEach(function(){
this.request=sinon.stub(http,'request');
});

it('should get valid result', function(done) {
	var expected = {"id": 1, "username": "sample", "email": "sample@sample.com"};
	var response = new PassThrough();
	response.write(JSON.stringify(expected));
	response.end();
 
	var request = new PassThrough();
 
	this.request.callsArgWith(1, response)
	            .returns(request);
 
	api.get(function(err, result) {
		assert.deepEqual(result, expected);
		done();
	});
});
});

npm test
    
    
    

3. JavaScript API Testing

In this exercise we would like you to test a remote API using Mocha.js
Be sure to use spies for services.

We have 3 endpoints that return 3 different payloads and HTTP Statuses, as follows:

HTTP Status 200
http://www.mocky.io/v2/5c77422c30000051009d619a

HTTP Status 401
http://www.mocky.io/v2/5c77407d3000000f009d6195

HTTP Status 418 Custom Error
http://www.mocky.io/v2/5c7741c53000004f009d6198

Please provide tests that make calls to these endpoints and assert that:

1. The status code is the one expected written above the URL given. If not, the test should fail.
2. Assert that the array returned in the status 200 example contains exactly this JSON structure:

    {"id": 1, "username": "sample", "email": "sample@sample.com"}

3. In the last 2 examples, assert that the "error" key exists in the json object returned.

npm install mocha sinon
mkdir tests

var request = require('request');
var assert = require('assert');
var sinon = require('sinon');
var http = require('http');
var api = require(http://www.mocky.io/v2');

describe('api',function(){
beforeEach(function(){
this.request=sinon.stub(http,'request');
var expected = {"id": 1, "username": "sample", "email": "sample@sample.com"};
});


it('should return valid response', function(done) {
     request.get('/5c77422c30000051009d619a')
                .expect(200)
                .end(function(err, res) {
                    expect(res.body).to.deep.equal(expected);
                    done(err);
                });
        });
it('should return 401', function(done) {
     request.get('/5c77407d3000000f009d6195')
                .expect(401)
                .end(function(err, res) {                    
                if (err) return done(err);
                expect(res.error.text).to.equal("Unauthorized");
                });
        });
it('should return 418', function(done) {
     request.get('/5c7741c53000004f009d6198')
                .expect(418)
                .end(function(err, res) {
                    if (err) return done(err);
                });
        });
});

npm test


How to submit your exercise:

- Please e-mail the team at ~COR0916ITInfraservPlatformMonitoring@det.nsw.edu.au with a link to your github/gitlab/or bitbucket public repository
containing the project(s) for each task.
