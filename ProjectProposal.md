
# GSOC '16

## 1. Project Info

- Project title: Improve SegAnnDB interactive genomic segmentation web app

- Project short title (30 characters): Improve SegAnnDB

- URL of project idea page: [Idea link](https://bitbucket.org/mugqic/gsoc2016#markdown-header-improve-seganndb-interactive-genomic-segmentation-web-app)  

## 2. Biographical Information 

I am an under graduate student pursuing my Bachelors in Computer Science from Indian Institute of Technology, Mandi. 

### 2.1 Why I think my background qualifies me for this project.

- Strong background and experience with programming in Python and JavaScript.

- Web-apps developed in Python(Flask) and JavaScript(AngularJS and NodeJS).

- Developed applications with D3js as visualization tool.

- Good experience working in UNIX/LINUX environment.

- Good experience working with GIT version control system.

### 2.2 Why I choose this project
- I am strongly interested in strengthening my Python and JavaScript skills.

- I find this project very interesting and challenging to work with.

- Computer Vision applied to a working project is exciting to me.

- I want to contribute to a project which will be potentially used by a number of people in the research, practical or academic field.

## 3. Contact Information

- Student name: Shubham Chandel

- Student postal address: 265, Sector 1, Ambala City (134003), Haryana, India

- Telephone(s): +91 8628890396

- Email(s): shubham_chandel@students.iitmandi.ac.in / shubham.zeez@gmail.com

- Other communications channels: Skype/Google+, etc. : shubham.zeez@gmail.com 


## 4. Student Affiliation

- University: Indian Institute of Technology, Mandi, India

- Program: Bachelors in Technology in Computer Science Engineering

- Stage of completion: Third Year

- Contact to verify: 

## 5. Schedule Conflicts

- Exams from 3 June to 10 June
Would be able to contribute marginally, will put in more hours after exam completion.

- No other conflicts during whole course of summer.
Will be able to contribute all my time to this project.

## 6. Mentors

- Mentor name: Toby Hocking

- Mentor emails: toby.hocking@mail.mcgill.ca

- Mentor link_ids: 

- Have you been in touch with the mentors? When and how? 
Yes, I have been in touch with the mentor Toby through E-mail. We discussed the current state of SegAnnDB web-app and I proposed certain features which can be implemented over the course of this summer. 

## 7. Synopsis

SegAnnDB is a Web-based computer vision system for genomic segmentation. My project will add a number of improvements including (but not limited to) render very large (> 500K pixels) DNA sequence in browser, adding unit test using Pyramid recommendations, social sharing of DNA sequence annotations to other users.

##  8. Benefits to Community

- Rendering of large DNA sequence will be useful to academicians working with large data set.

- Social sharing will help researchers share and discuss their opinions.

- A better UX and UI of web-app will attract larger audience.

## 9. Coding Plan & Methods

### 9.1 Project Goals

- Browser support to render large PNG.

- Social features for sharing annotations.

- Improve UI and UX of app

- Unit Test for Pyramids

- Periodically deletion of BerkeleyDB log file

#### Stretch Goals

- Add Sign in via multiple social platforms.

- Easier local installation via npm or pip installation package.

### 9.2 Implementation

#### **1. Browser support to render large PNG.**

#### Problem
Very large (> 500K pixels) DNA sequence cannot be rendered by the browser. Therefore it makes the SegAnnDB limited to testing and visualizing not so large DNA sequences. [This](http://sugiyama-www.cs.titech.ac.jp/~toby/images/) link demonstrates the problem in the browser.

#### Proposed solution
- **Provide link to sub-sequence**
Instead of making the browser render the whole image DOM as one, break the large image into small sequence of pixel size equal to user's display screen size (say about 1500 pixels) and have the sub-section link to the child DNA sequence. 
Example demonstration is present [here](http://bioviz.rocq.inria.fr/profile/dr3hg19/).

- **Render when required**
Currently the browser receives the whole image as a single DOM element. Browser has to render the whole image before the user can interact with it.
Instead of this, the image will be divided into several sub-images and each will be assigned to a DOM object. When the user will scroll through the DNA seq, only a small number of images (say 5 out of 50K) will be rendered and displayed by browser. New DOM will only be added if the user scrolls to that part of page. In the meantime the previous not visible DOM will be thrashed out to prevent memory usage.
This method will drastically reduce memory consumption by browser and will not hinder the work performed by the user.
Example demonstration is present [here](http://codepen.io/sksq/pen/grWgNp).

#### Coding Style

```
splitDNASequence()
```
- break the large DNA sequence into multiple about 1500 pixel image

```
renderWhenRequired()
```

- keep track of user position relative to page.
- create and assign new DOM elements.
- thrash old DOM not present in user's field of view.

```
trackUserMovement()
```
- track if user scrolls
- find where user is relative to page

#### **2. Social features for sharing annotations**

#### Problem

Currently if a user is logged in he can add annotations and view them later. These annotations are currently only accessible to the user that creates them, there is no option to share these annotations other users. 

#### Proposed Solution

- A sharing option is provided to all users, where the user simply type the E-mail address of recipient and an e-mail is sent to him.

- Three level of sharing will be implemented
	- Read only
	- Comment only
	- Write access

- Sharing annotation to multiple social media platform can be implemented as a stretch goal.

	![](http://students.iitmandi.ac.in/~shubham_chandel/GSOC/Sharing.png)

#### Coding Style 

```
generateShortURL()
```
- Generate short URL to be e-mailed

```
sendMailWithPermission()
```
- Assign permission to as described by user.
- Send out e-mail to recipient.

#### **3. Improve UI and UX of app**

#### Problem

The current UI of web-app is very outdated. The UX is not very intuitive and can be improved by adding various design improvements.

#### Proposed Solution

- [AngularJS](https://angularjs.org/) will be used as front-end design framework for implementing better UX and adding support for as-required DOM render, search feature.

- Improve the landing page of app by adding support for [responsive design](https://en.wikipedia.org/wiki/Responsive_web_design). 

- The UI of app will be in accordance with either [Flat design](https://en.wikipedia.org/wiki/Flat_design) or [Material Design](https://www.google.com/design/spec/material-design/introduction.html).


#### **4. Unit Test for Pyramids**

#### Problem

Currently there are no unit test for SegAnnDB in accordance with [pyramid unit test](http://docs.pylonsproject.org/projects/pyramid/en/latest/narr/testing.html).

#### Proposed Solution

- When a profile will be processed, there will be a test for presence of objects already present in the database.

- When the profile will be deleted, there will be a check for deletion of relevant objects and files. Example:
	- PNG scatterplots
	- BedGraph.gz data
	- Annotated regions


#### **5. Periodically deletion of BerkeleyDB log file**

#### Problem

Database log files consumes a lot of disk space. Depending on the rate at which the application writes to the databases and the available disk space, the number of log files may increase quickly enough so that disk space will be a resource problem.

#### Proposed Solution

- Periodically want to remove log files in order to conserve disk space.

- Log files may be removed at any time, as long as:

	- the log file is not involved in an active transaction.
	- a checkpoint has been written subsequent to the log file's creation.
	- the log file is not the only log file in the environment.

- This whole process is run as a separate daemon, when the server starts.

#### Coding Style

```
redundantLogFilesPresent()
```
- Check periodically is redundant log files are present on disk
```
removeLogFile()
```
- If file not currently used
- If the log file is not the only one
- Remove log file

#### **6. Add Sign in via multiple social platforms** (Stretch Goal)

#### Problem

Currently SegAnnDB supports on log in via Mozilla Persona and the user is provided with no option to log in with other platforms like GitHub, GMail, Facebook.

#### Proposed Solution

- Use [OAuth 2.0](http://oauth.net/2/) along with [GMail](https://developers.google.com/gmail/api/auth/about-auth), [GitHub](https://developer.github.com/v3/auth/), [Facebook](https://developers.facebook.com/docs/facebook-login) login API.


#### **7. Easier local installation via npm or pip** (Stretch Goal)

#### Problem

The current local installation process for the SegAnnDB web-app is tedious and cumbersome. No direct resource is available for developers to install SegAnnDB on their local machines.

#### Proposed Solution

- Develop a [Personal Package Archive](https://help.launchpad.net/Packaging/PPA) for the web-app, which can be easily installed by any Debian user using `apt-get`.

- Develop an [npm](https://www.npmjs.com/) or [pip](https://en.wikipedia.org/wiki/Pip_(package_manager)) package for the web-app.


## 10.  Timeline

### Before Project Starts
**Now - 22 May**
Setting up development platform. Reading complete code, creating basic documentation while reading. Setting up design layouts.

## 11. Management of Coding Project

- Clone [SegAnnDB repo](https://github.com/tdhock/SegAnnDB) to my working repo.

- After every progress in timeline, commit to the repo.

- Two concurrent progress will be done on separate branches.

- Report test result to mentor after every commit.

- At the end of project, a merge request to original [SegAnnDB repo](https://github.com/tdhock/SegAnnDB) will be made.

## 12. Selection Test

### Problem
- Install SegAnnDB on your local machine. 

- Make a YouTube video screen-cast where you upload and label some data sets on your local SegAnnDB server.

### Solution
- Youtube Video: [Installation: SegAnnDB genomic data segmentation on the web](https://youtu.be/sORxFrPyCvo)

- Youtube Video: [Upload and Label: SegAnnDB genomic data segmentation on the web](https://youtu.be/SmJGz-V5qcY)