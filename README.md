Game - Adding Habitica Avatar
---
This repository contains the HTML, dependencies and PNG files needed to generate a Habitica avatar for [e-mission-phone](https://github.com/e-mission/e-mission-phone) and similar repositories. The avatar PNG are converted into CSS using [gulp.spritesmith](https://github.com/twolfson/gulp.spritesmith/blob/master/README.md)

Habitrpg frequently updates sprites PNG and CSS folders and the dependencies may change too, so this repository may have to change sprites folders using the following guide:

Habitrgp uses Jade template instead of HTML but e-mission-phone uses HTML. 
	
	1. Use the [Habitica API](https://habitica.com/apidoc/#api-DataExport-ExportUserAvatarHtml) with a habitica user id on the browser to render an user avatar HTML page.
	2. Right click on the HTML page and click the Inspect option (This shows the Avatar HTML instead of Jade).
	3. Use the body of HTML inside the <figure> tag

The avatar has seperate PNG for head, costume, shirt, pet etc. Spritesmith converts the PNG to an avatar. The spritesmith gulp JavaScript that converts the PNG to a CSS avatar is located at www/tasks/gulp-sprites.js, updated this file according to Habitrpg repo. If there is a new PNG with different height and width than the defult PNGs, change this JavaScript.

The PNG and CSS folder that has the avatar is located at www/common/. Add new avatar PNG and CSS here.

Walk through to clone the required files from habitrpg to emission
	
1. Clone habitrpg repository

		$ git clone https://github.com/HabitRPG/habitrpg.git

2. Make task file in emission

		$ cd e-mission-phone/www/js/
		$ mkdir tasks

3. Copy the gulp-sprites.js file from habitrpg to emission

		$ cp -r habitrpg/tasks/gulp-sprites.js e-mission-phone/www/js/tasks/

4. Add the following line to e-mission-phone/gulpfule.js to sycn the gulp-sprites.js file

		require('glob').sync('/www/tasks/gulp-*').forEach(require);

5. Copy the 3 folders from habitrpg/common- css, dist and img, and paste it to e-mission-phone/www/common

		$ cd e-mission-habitica-local
		$ mkdir common
		$ cp -r habitrpg/common/css e-mission-phone/www/common
		$ cp -r habitrpg/common/dist e-mission-phone/www/common
		$ cp -r habitrpg/common/img e-mission-phone/www/common
	
6. In e-mission-phone/www/js/tasks/gulp-sprite.js add www/ before common to all the lines those point to the common folder that was copied from habitrpg to e-mission-phone

7. To add the avatar herobox css copy all the herobox class from habitrpg/website/build/app.css to one of the css folders in e-mission-phone 

After these changes, check in the modified repository, and pull the changes to
the phone repo.

Alternative way is to get the avatar PNG directly through the API. E-mission-phone has Content-Security-Policy that blocks unknown contents, to allow E-mission-phone to recognize the URL add the Habitrpg server URL and the s3 URL to “Content-Secutiry-Policy” in the head of www/templates/index.html   
