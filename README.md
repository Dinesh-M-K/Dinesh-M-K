### Laravel-Auth is a Complete Build of Laravel 5.2 with FULL Email and Social Authentication - COMPLETE WORKING Implementation. [![License](http://jeremykenedy.com/license-mit.svg)]()

Laravel 5.2 with user authentication, registration with email confirmation, social media authentication, password recovery, and captcha protection. This also makes full use of Controllers for the routes, templates for the views, and makes use of middleware for routing.  Super easy setup, can be done in 15 minutes. It will take longer to obtain your Facebook, Twitter, and Google Plus API Keys than it will to set this up.

###### A [Laravel](http://laravel.com/) 5.2.x with minimal [Bootstrap](http://getbootstrap.com) 3.5.x project.
| Laravel-Auth Features  |
| :------------ |
|Built on [Laravel](http://laravel.com/) 5.2|
|Uses [MySQL](https://github.com/mysql) Database|
|Uses [Artisan](http://laravel.com/docs/5.2/artisan) to manage database migration, schema creations, and create/publish page controller templates|
|Dependencies are managed with [COMPOSER](https://getcomposer.org/)|
|Laravel Scaffolding **User** and **Administrator Authentication**.|
|User Socialite Logins ready to go - See API list used below|
|Google Maps API v3 for User Location lookup and Geocoding|
|CRUD (Create, Read, Update, Delete) User Management|
|Google Captcha Protection with Google API|
|User Registration with email verification|
|Capture IP to users table upon signup|
|User Password Reset via Email Token|
|User Login with remember password|
|User roles implementation|
|Eloquent user profiles|
|Custom 404 Page|

### Quick Project Setup
###### (Not including the dev environment)
1. Run `sudo git clone https://github.com/jeremykenedy/laravel-auth.git laravel-authentication`
2. Create a MySQL database for the project
    * ```mysql -u root -p```, if using Vagrant: ```mysql -u homestead -psecret```
    * ```create database laravelAuth;```
    * ```\q```
3. From the projects root run `cp .env.example .env`
4. Configure your `.env` file // NOTE: Google API Key will prevent maps error
5. Run `sudo composer update` from the projects root folder
6. From the projects root folder run `sudo chmod -R 755 ../laravel-authentication`
7. From the projects root folder run `php artisan key:generate`
8. From the projects root folder run `php artisan migrate`
9. From the projects root folder run `composer dump-autoload`
10. From the projects root folder run `php artisan db:seed`

###### Seeds
1. Seeded Roles
   * user
   * editor
   * administrator

And thats it with the caveat of setting up and configuring your development environemnt. I recommend [VAGRANT](https://docs.vagrantup.com/v2/getting-started/) or the Laravel configured instance of Vagrant called [HOMESTEAD](http://laravel.com/docs/5.1/homestead).

### Laravel-Authentication URL's (routes)
* ```/```
* ```/auth/login```
* ```/auth/logout```
* ```/auth/register```
* ```/password/email```

### Laravel-Authentication Alias Redirect URL's (routes)
* ```/home```
* ```/reset```
* ```/login```
* ```/logout```
* ```/register```

### Laravel-Authentication Profile Routes
* ```/profile/{username}```
* ```/profile/{username}/edit``` <- Editing in this view is limited to current user only.

### Laravel-Authentication Admin Routes
* ```/users```
* ```/users/create```
* ```/users{user_id}```
* ```/users{user_id}/edit```

### Get Socialite Login API Keys:
* [Google Captcha API] (https://www.google.com/recaptcha/admin#list)
* [Facebook API] (https://developers.facebook.com/)
* [Twitter API] (https://apps.twitter.com/)
* [Google &plus; API] (https://console.developers.google.com/)
* [GitHub API] (https://github.com/settings/applications/new)
* [YouTube API] (https://developers.google.com/youtube/v3/getting-started)
* [Twitch TV API] (http://www.twitch.tv/kraken/oauth2/clients/new)
* [Instagram API] (https://instagram.com/developer/register/)
* [37 Signals API] (https://github.com/basecamp/basecamp-classic-api)

### Other API keys
* [Google Maps API v3 Key] (https://developers.google.com/maps/documentation/javascript/get-api-key#get-an-api-key)

### Add More Socialite Logins
* See full list of providers: [http://socialiteproviders.github.io](http://socialiteproviders.github.io/#providers)
###### **Steps**:
  1. Go to [http://socialiteproviders.github.io](http://socialiteproviders.github.io/providers/twitch/) and select the provider to be added.
  2. From the projects root folder in terminal run compser command to get the needed package.
     * Example:
      ```
         composer require socialiteproviders/twitch
      ```
  3. From the projects root folder run ```composer update```
  4. Add the service provider to ```/app/services.php```
     * Example:
     ```
   	'twitch' => [
   	    'client_id' 	=> env('TWITCH_KEY'),
   	    'client_secret' => env('TWITCH_SECRET'),
   	    'redirect' 		=> env('TWITCH_REDIRECT_URI'),
   	],
     ```
  5. Add the API credentials to ``` /.env  ```
     * Example:
      ```
         TWITCH_KEY=YOURKEYHERE
         TWITCH_SECRET=YOURSECRETHERE
         TWITCH_REDIRECT_URI=http://YOURWEBSITEURL.COM/social/handle/twitch
      ```
  6. Add the social media login link:
      * Example:
      In file ```/resources/views/auth/login.blade.php``` add ONE of the following:
         * Conventional HTML:
      ```

         <a href="{{ route('social.redirect', ['provider' => 'twitch']) }}" class="btn btn-lg btn-primary btn-block twitch">Twitch</a>

      ```
         * Use Laravel HTML Facade (recommended)
      ```

         {!! HTML::link(route('social.redirect', ['provider' => 'twitch']), 'Twitch', array('class' => 'btn btn-lg btn-primary btn-block twitch')) !!}

      ```

--

## Environment File

Example `.env` file:
```
APP_ENV=local
APP_KEY=SomeRandomString
APP_DEBUG=true
APP_LOG_LEVEL=debug
APP_URL=http://localhost

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravelAuth
DB_USERNAME=homestead
DB_PASSWORD=secret

CACHE_DRIVER=file
SESSION_DRIVER=file
QUEUE_DRIVER=sync

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_DRIVER=smtp
MAIL_HOST=smtp.gmail.com
MAIL_PORT=465
MAIL_USERNAME=YOURGMAILusernameHERE
MAIL_PASSWORD=YOURGMAILpasswordHERE
MAIL_ENCRYPTION=tls

# https://www.google.com/recaptcha/admin#list
RE_CAP_SITE=YOURGOOGLECAPTCHAsitekeyHERE
RE_CAP_SECRET=YOURGOOGLECAPTCHAsecretHERE

# https://developers.facebook.com/
FB_ID=YOURFACEBOOKidHERE
FB_SECRET=YOURFACEBOOKsecretHERE
FB_REDIRECT=http://yourwebsiteURLhere.com/social/handle/facebook

# https://apps.twitter.com/
TW_ID=YOURTWITTERidHERE
TW_SECRET=YOURTWITTERkeyHERE
TW_REDIRECT=http://yourwebsiteURLhere.com/social/handle/twitter

# https://console.developers.google.com/ - NEED OAUTH CREDS
GOOGLE_ID=YOURGOOGLEPLUSidHERE
GOOGLE_SECRET=YOURGOOGLEPLUSsecretHERE
GOOGLE_REDIRECT=http://yourwebsiteURLhere.com/social/handle/google

# https://github.com/settings/applications/new
GITHUB_ID=YOURIDHERE
GITHUB_SECRET=YOURSECRETHERE
GITHUB_URL=https://larablog.io/social/handle/github

# https://developers.google.com/youtube/v3/getting-started
YOUTUBE_KEY=YOURKEYHERE
YOUTUBE_SECRET=YOURSECRETHERE
YOUTUBE_REDIRECT_URI=https://larablog.io/social/handle/youtube

# http://www.twitch.tv/kraken/oauth2/clients/new
TWITCH_KEY=YOURKEYHERE
TWITCH_SECRET=YOURSECRETHERE
TWITCH_REDIRECT_URI=http://laravel-authentication.local/social/handle/twitch

# https://instagram.com/developer/register/
INSTAGRAM_KEY=YOURKEYHERE
INSTAGRAM_SECRET=YOURSECRETHERE
INSTAGRAM_REDIRECT_URI=http://laravel-authentication.local/social/handle/instagram

# https://basecamp.com/
# https://github.com/basecamp/basecamp-classic-api
37SIGNALS_KEY=YOURKEYHERE
37SIGNALS_SECRET=YOURSECRETHERE
37SIGNALS_REDIRECT_URI=http://laravel-authentication.local/social/handle/37signals

// NOTE: YOU CAN REMOVE THE KEY CALL IN app.blade.php IF YOU GET A POP UP AND DO NOT WANT TO SETUP A KEY FOR DEV
# Google Maps API v3 Key - https://developers.google.com/maps/documentation/javascript/get-api-key#get-an-api-key
GOOGLEMAPS_API_KEY=YOURGOOGLEMAPSkeyHERE
```

### File Structure of Common Used Files
```
laravel-auth/
    ????????? .env.example
    ????????? .gitattributes
    ????????? .gitignore
    ????????? artisan
    ????????? composer.json
    ????????? gulpfile.js
    ????????? LICENSE
    ????????? package.json
    ????????? phpspec.yml
    ????????? phpunit.xml
    ????????? README.md
    ????????? server.php
    ????????? app/
    ???   ????????? Http/
    ???   ???  ????????? kernal.php
    ???   ???  ????????? routes.php
    ???   ???  ????????? Controllers/
    ???   ???  ???   ????????? Auth/
    ???   ???  ???   ???   ????????? AuthController.php
    ???   ???  ???   ???   ????????? PasswordController.php
    ???   ???  ???   ????????? Controller.php
    ???   ???  ???   ????????? HomeController.php
    ???   ???  ???   ????????? ProfilesController.php
    ???   ???  ???   ????????? UserController.php
    ???   ???  ???   ????????? UsersManagementController.php
    ???   ???  ???   ????????? WelcomeController.php
    ???   ???  ????????? Middleware/
    ???   ???  ???   ????????? Administrator.php
    ???   ???  ???   ????????? Authenticate.php
    ???   ???  ???   ????????? CheckCurrentUser.php
    ???   ???  ???   ????????? Editor.php
    ???   ???  ???   ????????? EncryptCookies.php
    ???   ???  ???   ????????? RedirectAuthenticated.php
    ???   ???  ???   ????????? VerifyCsrfToken.php
    ???   ???  ????????? Requests/
    ???   ???      ????????? Request.php
    ???   ????????? Logic/
    ???   ???   ????????? macros.php
    ???   ???   ????????? Mailers/
    ???   ???   ???   ????????? Mailer.php
    ???   ???   ???   ????????? UserMailer.php
    ???   ???   ????????? User/
    ???   ???       ????????? CaptureIp.php
    ???   ???       ????????? UserRepository.php
    ???   ????????? Models/
    ???   ???   ????????? Password.php
    ???   ???   ????????? Profile.php
    ???   ???   ????????? Role.php
    ???   ???   ????????? Social.php
    ???   ???   ????????? User.php
    ???   ????????? Providers/
    ???   ???   ????????? AppServiceProvider.php
    ???   ???   ????????? BusServiceProvider.php
    ???   ???   ????????? ConfigServiceProvider.php
    ???   ???   ????????? EventServiceProvider.php
    ???   ???   ????????? MacroServiceProvider.php
    ???   ???   ????????? RouteServiceProvider.php
    ???   ????????? Services/
    ???   ???   ????????? Registrar.php
    ???   ????????? Traits/
    ???       ????????? CaptchaTrait.php
    ????????? config/
    ???   ????????? app.php
    ???   ????????? auth.php
    ???   ????????? cache.php
    ???   ????????? compile.php
    ???   ????????? database.php
    ???   ????????? filesystems.php
    ???   ????????? mail.php
    ???   ????????? queue.php
    ???   ????????? services.php
    ???   ????????? session.php
    ???   ????????? view.php
    ????????? database/
    ???   ????????? migrations/
    ???   ???   ????????? 2014_10_12_000000_create_users_table.php
    ???   ???   ????????? 2014_10_12_100000_create_password_resets_table.php
    ???   ???   ????????? 2015_05_15_124334_update_users_table.php
    ???   ???   ????????? 2015_10_21_173121_create_users_roles.php
    ???   ???   ????????? 2015_10_21_173333_create_user_role.php
    ???   ???   ????????? 2015_10_21_173520_create_social_logins.php
    ???   ???   ????????? 2015_11_02_004932_create_profiles_table.php
    ???   ???   ????????? 2015_12_25_010553_add_signup_ip_address_to_users_table.php
    ???   ???   ????????? 2015_12_25_011117_add_signup_confirmation_ip_address_to_users_table.php
    ???   ???   ????????? 2015_12_25_025231_add_signup_sm_ip_address_to_users_table.php
    ???   ???   ????????? 2016_04_19_045644_add_signup_admin_ip_address_to_users_table.php
    ???   ????????? seeds/
    ???       ????????? DatabaseSeeder.php
    ???       ????????? SeedRoles.php
    ????????? public/
    ???   ????????? .htaccess
    ???   ????????? index.php
    ???   ????????? robots.txt
    ???   ????????? assets/
    ???       ????????? css/
    ???       ????????? fonts/
    ???       ????????? ~~js/~~
    ????????? resources/
    ???   ????????? assets/
    ???   ???   ????????? Less/
    ???   ???       ????????? bootstrap/
    ???   ???       ????????? app.less
    ???   ????????? lang/
    ???   ???   ????????? en/
    ???   ???       ????????? auth.php
    ???   ???       ????????? emails.php
    ???   ???       ????????? forms.php
    ???   ???       ????????? links-and-buttons.php
    ???   ???       ????????? modals.php
    ???   ???       ????????? pagination.php
    ???   ???       ????????? passwords.php
    ???   ???       ????????? profile.php
    ???   ???       ????????? titles.php
    ???   ???       ????????? validation.php
    ???   ????????? views/
    ???       ????????? app.blade.php
    ???       ????????? welcome.blade.php
    ???       ????????? admin/
    ???       ???   ????????? create-user.blade.php
    ???       ???   ????????? edit-user.blade.php
    ???       ???   ????????? edit-users.blade.php
    ???       ???   ????????? show-user.blade.php
    ???       ???   ????????? show-users.blade.php
    ???       ????????? auth/
    ???       ???   ????????? activateAccount.blade.php
    ???       ???   ????????? guest_activate.blade.php
    ???       ???   ????????? login.blade.php
    ???       ???   ????????? password.blade.php
    ???       ???   ????????? register.blade.php
    ???       ???   ????????? reset.blade.php
    ???       ???   ????????? tooManyEmails.blade.php
    ???       ????????? emails/
    ???       ???   ????????? activateAccount.blade.php
    ???       ???   ????????? password.blade.php
    ???       ????????? errors/
    ???       ???   ????????? 403.blade.php
    ???       ???   ????????? 404.blade.php
    ???       ???   ????????? 503.blade.php
    ???       ????????? modals/
    ???       ???   ????????? modal-delete.blade.php
    ???       ???   ????????? modal-save.blade.php
    ???       ????????? pages/
    ???       ???   ????????? home.blade.php
    ???       ???   ????????? status.blade.php
    ???       ????????? partials
    ???       ???   ????????? form-status.blade.php
    ???       ???   ????????? nav.blade.php
    ???       ????????? profiles
    ???       ???   ????????? edit.blade.php
    ???       ???   ????????? show.blade.php
    ???       ????????? scripts
    ???           ????????? delete-modal-script.blade.php
    ???           ????????? gmaps-address-lookup-api3.blade.php
    ???           ????????? google-maps-geocode-and-map.blade.php
    ???           ????????? save-modal-script.blade.php
    ????????? storage/
    ????????? tests/
    ????????? vendor/
```

---

#### Laravel Developement Packages Used References
* http://laravel.com/docs/5.1/authentication
* http://laravel.com/docs/5.1/authorization
* http://laravel.com/docs/5.1/routing
* http://laravel.com/docs/5.0/schema

---

###### Updates:
* Update from Laravel 5.1 to 5.2
* Added eloquent editable user profile
* Added IP Capture
* Added Google Maps API v3 for User Location lookup
* Added Google Maps API v3 for User Location Input Geocoding
* Added Google Maps API v3 for User Location Map with Options
* Added CRUD(Create, Read, Update, Delete) User Management

---

## [Laravel](http://laravel.com/) PHP Framework

[![Build Status](https://travis-ci.org/laravel/framework.png)](https://travis-ci.org/laravel/framework) [![Latest Stable Version](https://poser.pugx.org/laravel/framework/version.png)](https://packagist.org/packages/laravel/framework) [![Total Downloads](https://poser.pugx.org/laravel/framework/d/total.png)](https://packagist.org/packages/laravel/framework) [![License](https://poser.pugx.org/laravel/framework/license.svg)](https://packagist.org/packages/laravel/framework)

Laravel is a web application framework with expressive, elegant syntax. We believe development must be an enjoyable, creative experience to be truly fulfilling. Laravel attempts to take the pain out of development by easing common tasks used in the majority of web projects, such as authentication, routing, sessions, and caching.

Laravel aims to make the development process a pleasing one for the developer without sacrificing application functionality. Happy developers make the best code. To this end, we've attempted to combine the very best of what we have seen in other web frameworks, including frameworks implemented in other languages, such as Ruby on Rails, ASP.NET MVC, and Sinatra.

Laravel is accessible, yet powerful, providing powerful tools needed for large, robust applications. A superb inversion of control container, expressive migration system, and tightly integrated unit testing support give you the tools you need to build any application with which you are tasked.

### Official Laravel Documentation

Documentation for the entire framework can be found on the [Laravel website](http://laravel.com/docs).

### Contributing To Laravel

**All Laravel Framework related issues and pull requests should be filed on the [laravel/framework](http://github.com/laravel/framework) repository.**

### Laravel License

The Laravel framework is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)

## [Bootstrap](http://getbootstrap.com) Front-End Framework

[![Build Status](https://img.shields.io/travis/twbs/bootstrap/master.svg)](https://travis-ci.org/twbs/bootstrap) ![Bower version](https://img.shields.io/bower/v/bootstrap.svg) [![npm version](https://img.shields.io/npm/v/bootstrap.svg)](https://www.npmjs.com/package/bootstrap) [![devDependency Status](https://img.shields.io/david/dev/twbs/bootstrap.svg)](https://david-dm.org/twbs/bootstrap#info=devDependencies) [![License](https://poser.pugx.org/laravel/framework/license.svg)](https://packagist.org/packages/laravel/framework)

Bootstrap is a sleek, intuitive, and powerful front-end framework for faster and easier web development, created by [Mark Otto](https://twitter.com/mdo) and [Jacob Thornton](https://twitter.com/fat), and maintained by the [core team](https://github.com/orgs/twbs/people) with the massive support and involvement of the community.

[Bootstrap](http://getbootstrap.com)'s documentation, included in this repo in the root directory, is built with [Jekyll](http://jekyllrb.com) and publicly hosted on GitHub Pages at [<http://getbootstrap.com>](http://getbootstrap.com).

---

## Development Environement References and help

#### VAGRANT Dev Environment References

###### VAGRANT Virtual Machine Details
|Item        |Value:
|:------------- |:-------------|
|Hostname|homestead|
|IP Address|192.168.10.10|
|Username|vagrant|
|SU Password|vagrant|
|Database Host|127.0.0.1|
|Database Port|33060|
|Database Username|homestead|
|Database Password|secret|
###### Start VAGRANT
|Command        |Action
|:------------- |:-------------|
| `vagrant up` | Start Vagrant VM |
| `vagrant up --provision` | Start Vagrant VM if vagrantfile updated |
| `vagrant halt` | Stop Vagrant VM |

###### Access VAGRANT SSH and MySQL
|Command        |Action      |
|------------- |:------------- |:-------------|
| ```sudo ssh vagrant@127.0.0.1 -p 222``` | Access Vagrant VM via SSH. Password is ``` vagrant  ``` |
| ```mysql -u homestead -psecret``` | Access Vagrant VM MySQL. Password is ``` vagrant  ``` |

If you do not have Bower, it can be installed using Node Package Manager (NPM).
If you do not have NPM, it can be installed using NODE JS.

###Install NODE JS
####Node JS can be installed muliple ways:
Mac GUI Installer, easiest way (Simply [Download](https://nodejs.org/en/) and Install)

####Node JS can also be installed using Homebrew Package Manager with the following command:
```
brew install node
```

###Install Node Package Manager (NPM)
####NPM can be installed using the following command:
```
npm install -g bower
```

###Install Bower
####Bower can be installed with the following command:
```
sudo npm install -g bower
```

###Install GULP
####GULP can be installed using the following command:
```
npm install -g gulp
```

###Install COMPOSER

####COMPOSER can be installed using the following commands:
```
sudo curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```

####COMPOSER on MAC OS X can be installed using the following commands:
```
sudo brew update
sudo brew tap homebrew/dupes
sudo brew tap homebrew/php
sudo brew install composer
```

#### Very Helpful Aliases
You can edit/or create your systems (MAC OS X) alias file with the follwing command:
```
sudo vim ~/.bash_profile
```

To update TERMINAL CLI to be able to use the the added aliases run the following command:
```
. ~/.bash_profile
```

##### *You can choose all or some of the following aliases to add to your `.bash_profile`:*

###### Vagrant/Homestead Aliases
```
alias machost='sudo vim /etc/hosts'
alias edithost='sudo vim /etc/hosts'
alias sshlara='sudo ssh vagrant@127.0.0.1 -p 2222'
alias laraedit='vim ~/.homestead/Homestead.yaml '
alias aliaslara='vim ~/.homestead/aliases'
alias laraalias='vim ~/.homestead/aliases'
alias sql='mysql -u homestead -psecret'
alias larasql='mysql -u homestead -psecret'
alias updatecomposer='sudo composer self-update'
alias rollbackcomposer='sudo composer self-update --rollback'
```

A helpful bashfile alias function to **start VAGRANT** instance:
```
function laraup {
  _pwd=$(pwd)
  startVM(){
    vagrant up --provision
  }
  echo "=============================================================================="
  echo "****** STARTING LARAVEL VAGRANT INSTANCE "
  echo "=============================================================================="
  cd ~/Homestead/
  if startVM ; then
    echo "=============================================================================="
    echo "****** SUCCESS - LARAVEL VAGRANT STARTED :)~"
    echo "=============================================================================="
  else
    echo "=============================================================================="
    echo "****** ERROR - LARAVEL VAGRANT DID NOT START :("
    echo "=============================================================================="
  fi
  cd $_originalDir
}
```

A helpful bashfile alias function to **shutdown/halt/stop VAGRANT** instance:
```
function laradown {
  _pwd=$(pwd)
  stopVM(){
    vagrant halt
  }
  echo "=============================================================================="
  echo "****** STOPPING LARAVEL VAGRANT INSTANCE "
  echo "=============================================================================="
  cd ~/Homestead/
  if stopVM ; then
    echo "=============================================================================="
    echo "****** SUCCESS - LARAVEL VAGRANT SHUTDOWN :)~"
    echo "=============================================================================="
  else
    echo "=============================================================================="
    echo "****** ERROR - LARAVEL VAGRANT DID SHUTDOWN :("
    echo "=============================================================================="
  fi
  cd $_originalDir
}
```

A helpful bashfile alias function to **remove VAGRANT** instance:
```
function larakill {
  _pwd=$(pwd)
  killVM(){
    vagrant destroy
  }
  echo "=============================================================================="
  echo "****** DESTROYING LARAVEL VAGRANT INSTANCE "
  echo "=============================================================================="
  cd ~/Homestead/
  if killVM ; then
    echo "=============================================================================="
    echo "****** SUCCESS - LARAVEL VAGRANT DESTROYING :)~"
    echo "=============================================================================="
  else
    echo "=============================================================================="
    echo "****** ERROR - LARAVEL VAGRANT WAS NOT DESTROYING :("
    echo "=============================================================================="
  fi
  cd $_originalDir
}
```

##### General Very Helpful Aliases
###### Cleanup
A nice alias to **list all** the MAC and OSX filesystem booger:
```
alias cleanprint='
find . -name "*.DS_Store" -print;
find . -name "*.DS_Store" -print;
find . -name "*._DS_Store" -print;
find . -name "._.DS_Store" -print;
find . -name ".DS_Store" -print;
find . -name "Thumbs.db" -print;
find . -name "._.*" -print;
find . -name "._*" -print ;
'
```

A nice alias to **delete all** the MAC and OSX filesystem booger:
```
alias cleanrm='
find . -name "*.DS_Store" -delete;
find . -name "*.DS_Store" -delete;
find . -name "*._DS_Store" -delete;
find . -name "._.DS_Store" -delete;
find . -name ".DS_Store" -delete;
find . -name "Thumbs.db" -delete;
find . -name "._.*" -delete;
find . -name "._*" -delete ;
'
```

A nice alias to **list and delete all** the MAC and OSX filesystem boogers:
```
alias cleanboth='
find . -name "*.DS_Store" -print;
find . -name "*.DS_Store" -print;
find . -name "*._DS_Store" -print;
find . -name "._.DS_Store" -print;
find . -name ".DS_Store" -print;
find . -name "Thumbs.db" -print;
find . -name "._.*" -print;
find . -name "._*" -print ;
find . -name "*.DS_Store" -delete;
find . -name "*.DS_Store" -delete;
find . -name "*._DS_Store" -delete;
find . -name "._.DS_Store" -delete;
find . -name ".DS_Store" -delete;
find . -name "Thumbs.db" -delete;
find . -name "._.*" -delete;
find . -name "._*" -delete ;
'
```
###### Show MAC OS X files
Alias to **show all hidden files** on MAC OS X filesystem:
```
alias showfiles='defaults write com.apple.finder AppleShowAllFiles YES; killall Finder /System/Library/CoreServices/Finder.app'
```

Alias to **hide all hidden files** on MAC OS X filesystem:
```
alias hidefiles='defaults write com.apple.finder AppleShowAllFiles NO; killall Finder /System/Library/CoreServices/Finder.app'
```

##### GIT CLI Quick alias functions
###### Quick GIT PUSH
```
function quickpush {
    _currentBranch=$(git branch | sed -n -e 's/^\* \(.*\)/\1/p')
    sudo git add -A
    sudo git commit -m "quick push"
    sudo git push $_currentBranch
}
```

###### Another flavor of Quick GIT PUSH
```
function push {
    _currentBranch=$(git branch | sed -n -e 's/^\* \(.*\)/\1/p')
    sudo git add -A
    sudo git commit -m "quick push"
    sudo git push $_currentBranch
}
```

###### Quick GIT PULL
```
function quickpull {
    _currentBranch=$(git branch | sed -n -e 's/^\* \(.*\)/\1/p')
    sudo git pull $_currentBranch
}
```

###### Another flavor of Quick GIT PULL
```
function pull {
    _currentBranch=$(git branch | sed -n -e 's/^\* \(.*\)/\1/p')
    sudo git pull $_currentBranch
}
```

##### My keyboard hates me GIT helper aliases:
```
alias gut='git'
alias got='git'
alias car='cat'
alias commut='commit'
alias commmit='commit'
alias comit='commit'
alias commot='commit'
```

##### Typing `clear` takes too many keystrokes alias helper:
```
alias cl='clear'
```

###### Helpful quick filesystem `ls` alias helpers:
```
alias la='ls -la'
alias ll='ls -la'
```

##### **Alias** and **`.bash_profile management`** aliases:
###### **Show** Aliases helpers:
```
alias listalias='cat ~/.bash_profile'
alias aliaslist='cat ~/.bash_profile'
alias list='cat ~/.bash_profile'
alias text='cat ~/.bash_profile'
alias aliasshow='cat ~/.bash_profile'
```

###### **Edit** Aliases helpers:
```
alias aliasedit='sudo vim ~/.bash_profile'
alias editalias='sudo vim ~/.bash_profile'
```

#### **Restart/Enable** Aliases helpers:
```
alias aliasreset='. ~/.bash_profile'
alias aliasr='. ~/.bash_profile'
alias alr='. ~/.bash_profile'
alias alsr='. ~/.bash_profile'
alias aliasrestart='. ~/.bash_profile'
```

#### Things not working (Troubleshooting)?

##### Issue: Cannot access project through web browser after running vagrant up / homestead up

###### Error Message from Browser:
```
This webpage is not available
ERR_NAME_NOT_RESOLVED
```

##### 1. Check Vagrant/Homestead configuration
###### a. Open configuration with the following command:

vim ~/.homestead/Homestead.yaml or laraedit

###### b. Check to make sure your folders are mapped (See example A1.):
Note:
map: Is the path to the your files on your local machine
to: Is the virtual file path to your projects that vagrant will create
###### Example A1
```
folders:
  - map: /Users/yourLocalUserName/Sites/project1
    to: /home/vagrant/Sites/project1/public

  - map: /Users/yourLocalUserName/Sites/project2
    to: /home/vagrant/Sites/project2/public
```
##### c. Check to make sure your projects URI and SYMLINK is mapped (See example A2):
map: Is the local URI of your project
to: Is the virtual symlink to your projects virtual file path
###### Example A2
```
sites:
  - map: project1.local
    to: /home/vagrant/Sites/project1/public

  - map: project2.app
  to: /home/vagrant/Sites/project2/public
```
#### 2. Check your local hosts file for local pointer redirect:
##### a.  Open your hosts file (See example B1):
Note: Instructions are for Mac OS X
###### Example B1
`sudo vim /etc/hosts` or `edithost`

##### b.  Edit your hosts file (See example B2):
Note: Replace examples URI used in Vargrant/Homestead configuration file and use the IP address of your local Vargrant/Homestead virtual machine instance

###### Example B2 - The last line is the important part of the example
```
##
# Host Database
#
# localhost is used to configure the loopback interface
# when the system is booting.  Do not change this entry.
##
127.0.0.1        localhost
255.255.255.255  broadcasthost
192.168.10.10    laravel-authentication.local
```

---

## Enjoy

###### ~ **Jeremy**
