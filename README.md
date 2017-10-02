GDG-X Boomerang for App Engine (Java)
==============================

[![Join the chat at https://gitter.im/Splaktar/boomerang-gae](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/Splaktar/boomerang-gae?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

## Notice

This project has been deprecated in favor of using either GitHub Pages or Firebase Hosting with the core [boomerang project](https://github.com/gdg-x/boomerang). That approach is much more straightforward. Firebase Hosting provides free SSL Certificates and HTTPS hosting.

However this project can still be used in combination with Prerender.io if SEO is important for your chapter. You will need to manually update the contents of `/war` with the latest changes from [boomerang](https://github.com/gdg-x/boomerang). I had been manually keeping this project updated in the past, but that will no longer happen.

==============================

This is forked from the [GDG-X boomerang](https://github.com/gdg-x/boomerang) project.

Boomerang is a template for a dynamic material design GDG chapter web site that can be deployed
within 30 minutes. It pulls data from [GDG-X Hub](https://github.com/gdg-x/hub) and 
[Google+ API](https://developers.google.com/+/api/) using [AngularJS](https://angularjs.org/) and 
[Angular-Material](https://material.angularjs.org).

See it in action: http://gdg-x.github.io/boomerang

Prerequisites
---------------
* Install the [Google Cloud SDK](https://cloud.google.com/sdk/).
* GAE requires Java 7. Configure your IDE to use Java 7 for the project.
* [Node.js](http://nodejs.org/download/)

On IntelliJ:
---------------
* Setup your local App Engine Dev Server in Preferences->Build, Execution, Deployment->Application Servers.
* Define the path to your App Engine SDK.
* Add the following directories to the libraries list of your new Application Server:
* google-cloud-sdk/platform/appengine-java-sdk/lib
* google-cloud-sdk/platform/appengine-java-sdk/lib/agent
* google-cloud-sdk/platform/appengine-java-sdk/lib/opt/user/appengine-endpoints/v1
* google-cloud-sdk/platform/appengine-java-sdk/lib/opt/user/datanucleus/v2
* google-cloud-sdk/platform/appengine-java-sdk/lib/shared
* google-cloud-sdk/platform/appengine-java-sdk/lib/user
* google-cloud-sdk/platform/appengine-java-sdk/lib/user/orm

Configuring
---------------
Update war/app/services/configService.js with values appropriate for your group:

1. **name**: The name of your GDG
2. **id**: The ID of the Google+ page for your GDG; for example, if your page
   URL is https://plus.google.com/u/0/b/115803993493374365281/, then the ID is '115803993493374365281'.
3. **google_api**: The API key for your project, available from the [Cloud Console](https://cloud.google.com/console)
  1. Create a new project then go to APIs & Auth->APIs, activate Google+ API.
  2. Go to APIs & Auth->Credentials and under Public API access 'Create new Key' of BrowserKey with `Any referrer allowed`.
4. **pwa_id**: The ID for a Picasa web album from which pictures will be drawn. If you do not have a Picasa web album
   for your group, you will want to comment out the photos tab in **index.html**.
5. **twitter**, **facebook**, **meetup**: Update these with your chapter's social network handles. Setting them to '' will hide the icon.
6. Create your Google Analytics account and modify the Google Analytics tracking code in **index.html**.
7. Open **war/WEB-INF/appengine-web.xml** and put your Project ID (available from Project Overview page of Cloud Console) in the `<application></application>` tag.

Additional Optional Config
---------------
5. **domain**: Your custom domain name (or base appspot URL).
6. **cover.title**: An announcement that will appear on the landing page.
7. **cover.subtitle**: More text to support the landing page announcement.
8. **cover.button.text**: Text for the announcement button.
9. **cover.button.url**: The URL that the announcement button will open in another window.
10. **cover.url**: If the cover image drawn from your Google+ page does not work with the default layout,
   you can specify a URL for a specific image instead.
12. Edit the snippet details in the **index.html** to change how your page looks when it is shared.
13. Modify the images in war/app/images/sponsor1 and war/app/images/sponsor2 to be your sponsor images.
14. Modify the sponsor links in **about.html**.
16. Create a free https://prerender.io account (up to 250 pages).
17. Find your token on prerender.io, insert it into **web.xml** where it says `INSERT_YOUR_PRERENDER_TOKEN_HERE`.
18. Update the war/sitemap.xml with the URL of your site.

NOTE: You cannot test prerendering of pages locally.

Building
---------------
Here you will install dependencies and tooling, build, minify, run static analysis, and more.

You must have Node.js installed to use the build tools. Download it [here](http://nodejs.org/download/).

From the boomerang directory, run the following:

1. `npm install`
2. `bower install`
3. `gulp prod`

NOTE: You may need to use `sudo` for running `npm` on OS X or Linux.

NOTE: For easier debugging and development use, use `gulp dev` but make sure to run `gulp prod` before deploying to production.

Deploy locally
---------------
Make sure you cd into the boomerang-gae directory, then: `dev_appserver.sh war`

On Windows: `dev_appserver.cmd war`

Testing
---------------
1. Unit tests can be run once via `gulp karma` or constantly via `gulp karma-watch`.
2. Integration tests can be run via:
  1. `node node_modules/protractor/bin/webdriver-manager update`
  2. `node node_modules/protractor/bin/webdriver-manager start`
  3. Then in a separate terminal: `node node_modules/protractor/bin/protractor test/e2e/conf.js`
3. WebStorm or IntelliJ IDEA can make this testing a lot easier if you configure the idea to do it for you.

Deploy to App Engine via the CLI
---------------
Make sure you cd into the boomerang-gae directory, then: `sudo appcfg.sh --oauth2 update war`

On Windows: `appcfg.cmd --oauth2 update war`

If you see an exception about creds, run `gcloud auth login` and go through the OAuth flow with the proper account.
This always needs to be done at least the first time.

Development Details
---------------
Make sure that you do the following successfully before committing:

1. `gulp prod` - Make sure you fix any JSCS or JSHint errors.
2. `gulp karma` - Make sure that you fix any broken tests.
3. Protractor tests - Make sure that you fix any broken tests.
4. If you changed any dependency versions in `bower.json`, make sure that `config/CDN.json` is updated to match.

### Contributors
See [list of contributors](https://github.com/gdg-x/boomerang-gae/graphs/contributors)

Maintainer: None.

###### GDG Apps, GDG[x] are not endorsed and/or supported by Google, the corporation.

License
--------

    © 2013-2016 GDG[x]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
