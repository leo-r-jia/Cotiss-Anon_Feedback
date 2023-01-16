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
      <a href="#about-the-project">About The Project</a>
    </li>
    <li>
      <a href="#product-objectives">Product Objectives</a>
    </li>
    <li>
      <a href="#first-iteration">First Iteration</a>
    </li>
  </ol>
</details>
  
## About The Project
<h3>The Client</h3>
Cotiss is built specifically to help organisations be more effective in how they buy & supply goods and services. They’re a B2B company that creates software for companies to track their spending and make better business decisions. 

<h3>The Project</h3>
As Cotiss has grown over the years, the need for collecting feedback internally and externally has become a more prominent issue. Cotiss leadership is looking for a simple website where employees can anonymously submit feedback. To encourage employees to share honestly, they want a randomly selected piece of existing feedback to be displayed on the site on each page load. 
<br><br>
The UX design is simple; a random piece of feedback displayed on each page load, and a box at the bottom of the page with a submit button to add new feedback to the feedback bank. 

## Product Objectives

The simple honest anonymous feedback site encourages Cotiss employees to submit honest feedback. User interactions should be straight-forward: type feedback into the input text field, and click the submit button.
<br><br>
This documentation should help admins manage the website and know how to access and read the reviews submitted by employees.

## First Iteration

<b>Web Hosting</b>
Created a simple HTML/CSS page that met the requirements of the project - text for random piece of feedback generated on each load, text area for users to input their feedback, and a submit button to submit the feedback - however purely visual. At this point, no JavaScript had been added and the main purpose of the simple site was to ensure web hosting worked properly.
<br><br>
For web hosting, an EC2 virtual machine (VM) was deployed. The operating system used for the VM was Amazon Linux AMI, SSD Volume Type; the instance type of this VM was t2 micro.
<br><br>
