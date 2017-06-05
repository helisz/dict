#Configuring HTML 5 mode


AngularJS uses a “#” in it’s urls. HTML5Mode of AngularJS removes these “#” from URL.

##Activate HTML 5 Mode
Create html5.mode.config.js file in webapp/app/blocks/config/ directory:

```
(function() {
  'use strict';

  angular
    .module('<YourAppName>')
    .config(html5ModeConfig);

  html5ModeConfig.$inject = ['$locationProvider'];

  function html5ModeConfig($locationProvider) {
    $locationProvider.html5Mode({ enabled: true, requireBase: true });
  }
})();
```
Then open index.html and add this line in head tag:
```
<base href="/">
```
##Redirection filter
Now, to have relative paths links working correctly (ex. activation link sent to user e-mail) we will create a controller to forward the URI to index.html:
```
@Controller
public class AngularJsForwardController {
    @RequestMapping(value = "/**/{[path:[^\\.]*}")
    public String redirect() {
        return "forward:/";
    }
}
```
