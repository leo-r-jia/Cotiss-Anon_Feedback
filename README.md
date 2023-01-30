<h1>Cotiss Anon Feedback Project</h1>

<p>
  <a href="https://youtu.be/QcGtofB6Nl8">View Demo Video</a>
  ·
  <a href="https://www.cotiss-anon-feedback.com">Website</a>
<p>
  
  ![image](https://user-images.githubusercontent.com/105583042/212533326-64bc3baf-ee2e-49c0-b685-6c111a37de81.png)


<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About the Project</a>
    </li>
    <li>
      <a href="#product-objectives">Product Objectives</a>
    </li>
    <li>
      <a href="#first-iteration">First Iteration</a>
      <ul>
        <li><a href="#web-hosting">Web Hosting</a></li>
        <li><a href="#auto-scaling">Auto Scaling</a></li>
        <li><a href="#domain-registration">Domain Registration</a></li>
      </ul>
    </li>
    <li>
      <a href="#second-iteration">Second Iteration</a>
      <ul>
        <li><a href="#external-data">External Data</a></li>
        <li><a href="#micro-services-and-apis">Micro Services and APIs</a></li>
        <li><a href="#web-hosting-platform-as-a-service">Web Hosting Platform-as-a-Service</a></li>
      </ul>
    </li>
        <li>
      <a href="#final-iteration">Final Iteration</a>
      <ul>
        <li><a href="#amplify-hosting">Amplify Hosting</a></li>
        <li><a href="#micro-services-and-apis-2">Micro Services and APIs</a></li>
        <li><a href="#web-hosting-platform-as-a-service-2">Web Hosting Platform-as-a-Service</a></li>
      </ul>
    </li>

  </ol>
</details>
  
## About the Project
<h3>The Client</h3>
Cotiss is built specifically to help organisations be more effective in how they buy & supply goods and services. They’re a B2B company that creates software for companies to track their spending and make better business decisions. 

<h3>The Project</h3>
As Cotiss has grown over the years, the need for collecting feedback internally and externally has become a more prominent issue. Cotiss leadership is looking for a simple website where employees can anonymously submit feedback. To encourage employees to share honestly, they want a randomly selected piece of existing feedback to be displayed on the site on each page load. 
<br><br>
The UX design is simple; a random piece of feedback displayed on each page load, and a box at the bottom of the page with a submit button to add new feedback to the feedback bank. 

## Product Objectives

The simple honest anonymous feedback site encourages Cotiss employees to submit honest feedback. User interactions should be straight-forward: type feedback into the input text field, and click the submit button. Each feedback submitted should be stored into a feedback bank, which will be accessed on each site reload to pick a random piece of feedback to display on the site.
<br><br>
This documentation should help admins manage the website and know how to access and read the reviews submitted by employees.

## First Iteration

### Web Hosting
Created a simple HTML/CSS page that met the requirements of the project - text for random piece of feedback generated on each load, text area for users to input their feedback, and a submit button to submit the feedback - however purely visual. At this point, no JavaScript had been added and the main purpose of the simple site was to ensure web hosting worked properly. Below: the 20 lines of code used in this interation, the site displayed.

```html
<html lang="en">
​
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=, initial-scale=1.0">
    <link rel="stylesheet" href="styles.css">
    <title>Anonymous Feedback</title>
</head>
​
<body>
    <div class="container">
        <h1>Anonymous Feedback</h1>
        <p>"Some quote... <br>Second line "</p>
        <textarea name="" id="" cols="30" rows="10" placeholder="Enter your feedback here" class="input"></textarea>
        <button>Submit</button>
    </div>
</body>
​
</html>
   ```

<br>

![image](https://user-images.githubusercontent.com/105583042/212622208-f0da670d-8e9f-4dd6-9263-7d9b5fa2c525.png)

<br>
For web hosting, an Amazon EC2 virtual machine (VM) was deployed. The operating system used for the VM was Amazon Linux AMI, SSD Volume Type; the instance type of this VM was t2 micro. A security group was configured to allow two types of inbound traffic - SSH (to log in to the virtual computer) and HTTP (to view the webpage from a browser).
<br><br>
When the EC2 instance was set up, an apache web server was installed onto the VM and the HTML file was linked to be served by the apache web server.

### Auto Scaling

Once the HTML page was viewable from the EC2 instance via a browser, an Amazon Machine Image was created from the virtual machine. This was then put into an auto scaling group so that one virtual machine always exists. There were a minimum of 1 virtual machine running at all times, a maximum of 2, and 2 running at a single time preferred, and each one in a different availability zone. An Elastic Load Balancer was put in front of the virtual machines to load balance between two availability zones. This modelled an active/active multi-region architecture, pictured below.

![activeactive](https://user-images.githubusercontent.com/105583042/212634092-d9c13816-d8d5-458b-a026-9ca406797494.PNG)


### Domain Registration

Once, auto scaling was set up, a domain (www.cotiss-anon-feedback.com) was registered using Amazon Route 53. Certificates were created using AWS Certificate Manager for domains `cotiss-anon-feedback.com` and `www.cotiss-anon-feedback.com`. All traffic to the domain was redirected to the Load Balancer, which would balance inbound traffic to the two instances.

## Second Iteration

### External Data

To store the feedback submitted by users, a DynamoDB table was created. 

### Micro Services and APIs

The architecture: Website calls API Gateway which executes a Lambda Function which reads/updates data in the DynamoDB table. With the help of JavaScript, the HTML site was transformed into a dynamic site. 
<br><br>
Firstly, a Lambda function was created that retrieved an item from the DynamoDB table created earlier. This was achieved through IAM roles and Python. A GET REST API was created using API Gateway that invoked the Lambda function when called. Using JavaScript, the website would call the API with every reload of the page and display the retrieved piece of feedback on the website.
<br><br>
Secondly, a Lambda function was created that stored the feedback text, from the text field on the website to the Lambda table. Again, this was achieved through IAM roles and Python. A POST REST API was created using API Gateway that invoked the Lambda function when called. Again using JavaScript, with each click of the submit button (as long as the text field was not empty), the POST API would be called to store the feedback text in the DynamoDB table as well as the date and time the feedback was submitted.

### Web Hosting Platform-as-a-Service

This step saw the retirement of the EC2 instances, the auto scaling groups, and the Load Balancers. An Amazon S3 bucket was created which contained the files for the website, and hosted the simple site along with AWS CloudFront. Using Amazon Route 53, all traffic to the domain previously registered `cotiss-anon-feedback.com` was routed to the CloudFront distribution. Now, there are no longer servers, web server software, load balancing to manage.

## Final Iteration

![image](https://user-images.githubusercontent.com/105583042/215595835-1f5665c1-2181-46dd-b92d-c2e815c0c306.png)


### Amplify Hosting

The final product saw the retirement of the S3 bucket and CloudFront distribution, and instead a GitHub repo and AWS Amplify App. Using Amplify Hosting, the Amplify App connects to this GitHub repository where it gets the files to host. With each GitHub repo update (update to the website), Amplify will automatically update those changes in the background. A CloudFront distribution is automatically created with the Amplify app.

### Route 53

Using Amazon Route 53, all traffic to the domain previously registered `cotiss-anon-feedback.com` was routed to the CloudFront distribution. Now, there is no S3 bucket to manage everytime an update needs to be made live. All traffic going to the http port will be redirected to https, providing a layer of security.

### Micro Services and APIs

The architecture: Website calls API Gateway which executes a Lambda Function which reads/updates data in the DynamoDB table. With the help of JavaScript, the HTML site was transformed into a dynamic site. 
<br><br>
A Lambda function that retrieved an item from the DynamoDB table is called by a GET REST API created using API Gateway. Using JavaScript, the website calls the API with every reload of the page and display the retrieved piece of feedback on the website.
<br><br>
A Lambda function that stores the feedback text, from the text field on the website to the Lambda table is called by a POST REST API created using API Gateway. Again using JavaScript, with each click of the submit button (as long as the text field was not empty), the POST API is called to store the feedback text in the DynamoDB table as well as the date and time the feedback was submitted.
