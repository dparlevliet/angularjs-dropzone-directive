angularjs-dropzone-directive
============================

An AngularJS dropzone directive with support for CSRF making it ideal for use with Django or RoR


Example HTML
=====
```
<div dropzone ng-config="images.config" ng-csrftokenname="csrfmiddlewaretoken" ng-csrftoken="csrftoken" class="dropzone">
</div>
```

Example Config
====
```
  $scope.images = {
    config: {
      'options': {
        'url': '/files/upload/image'
      },
      'eventHandlers': {
        'error': function(file, response, xhr) {
        },
        'complete': function() {
        },
        'sending': function (file, formData, xhr) {
        },
        'success': function (file, response) {
        }
      }
    }
  };
```


Example CSRF with Django
====
```
function getCookie(name) {
  var cookieValue = null;
  if (document.cookie && document.cookie != '') {
    var cookies = document.cookie.split(';');
    for (var i = 0; i < cookies.length; i++) {
      var cookie = jQuery.trim(cookies[i]);
      // Does this cookie string begin with the name we want?
      if (cookie.substring(0, name.length + 1) == (name + '=')) {
        cookieValue = decodeURIComponent(cookie.substring(name.length + 1));
        break;
      }
    }
  }
  return cookieValue;
}
var csrftoken = getCookie('csrftoken');

app.controller("main", function(
  $scope,
  $rootScope,
) {

  $rootScope.csrftoken = csrftoken;

});
```
This will make the csrftoken variable available to Dropzone via <tt>ng-csrftoken</tt>. However, <tt>ng-csrftokenname</tt> 
is also required and expected if you want this to work. For Django the CSRF token name should be
<tt>csrfmiddlewaretoken</tt>.
