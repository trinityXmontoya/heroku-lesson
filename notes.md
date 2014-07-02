## Heroku




### What is it?
* a platform for easily deploying web apps (popular for rails app, you can also use amazon ec2 (funny bc when you are using heroku your app is actually hosted on ec2))
* right now you've been running everything locally, but when you're working on your projects, and when you actually want other people on *other* computers to be able to use your app you have to host it online
* if anyone has their own website right now or has helped setup a website before, you typically FTP your files and drag and drop them in, using something like GoDaddy, everytime you make a change you go back and have to replace the old file with the new one
* heroku is easy to use if you feel comfortable navigating around the command line  with git which you all do

### Why use it?

- you focus on your app, they handle setting up, configuring, and mainting a production server
- instantly make changes using git 
	- (for anyone who hosts on another site you know you have to manually go in and load / upload new files via FTP, this way you can just push from the command-line)
	- guarantees your local version is the same as on the site
	- heroku can only deploy from the master branch, so if you are pushing from a branch other than master either merge that with master or 
	
	`git push heroku myfeaturebranch:master`
	
- addons 
	- not important right now but in the future there are a lot of (usually 3rd party)resources you can do for things like monitoring your site and analytics tracking(new relic)
	- support for a few databases (postgres, redis, mongodb)
	- they're free but as your app grows, scaling on heroku is pretty simple and usually just a matter of upgrading your plan, but that can get expensive depending on how big your site is
	
	`heroku addons:add heroku-postgresql:hobby-basic`
	
***explore heroku postgres***
	
- logging, in the same way you can see output in your terminal from rails heroku keeps logs of your 

- good support for a few languages (node, java, python, php), but again, not needed for a simple site

- (go daddy only supports ruby v 1.9)

* heroku hosted on amazon ec2, basically makes a git repo for you to post to and then runs the app on their servers

* they let you host 

#### Vocabulary
* dyno (unit of computing power)
	- run your code and respond to HTTP requests
	- heroku runs one for you automatically
	- after the first one oyu pay
* procfile 
	- a document where you declare what commands you need to be run when your app starts
	- heroku automatically detects the language of your app and will run the default web process command for you
	- while it's not necessary it will allow you greater flexibility/control over your app if that's something you need, for example if you have background workers ( ex. image processing, delete users) you could set those up in the Procfile



####Example heroku-hosted sites
* code for america
* apartment list
* level up
* miley cyrus's official site (25k visitors a month)

###Deployment Steps 



LOCAL SETUP

---

1. install Heroku toolbelt 
	* heroku client - allows you to easily interface w heroku from the command line
	* foreman - you create a Procfile that specifies what processes need to be performed in order for you app to run
		* not necessary to create a Procfile but will help your app run faster, webrick should not be used in production
	* git - for version control, and setting up the remotes for you
	
2. login to your heroku account
 	* generate ssh key for $ecurity
 	
APP

---
3. Navigate to the app you want to deploy
4. Add rails_12factor gem (gem 'rails_12factor', group: :production)
	* 12factor.net/
	* logs outtped to stdout
	* dev/prod parity

QUESTIONS

---
`heroku restart` 
Restarts your app on heroku the same way you ctrl+c in terminal and restart your rails server

TROUBLESHOOTING

---



####logs -

* heroku logs (last 100)
* heroku logs -n 1500 (last 1500)
* for anything more than that use an add-on


###Limitations
* no file-system write access (you can't store files from your app on heroku, for example if you allow users to upload photos, use something like s3 for storing documents)
* no direct database access, you can either pull it down or by using ActiveRecord thru the remote ruby console
