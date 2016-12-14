# How to correctly use $http GET/POST in AngularJS

## $http GET Method
```javascript
	$http({
		method: 'GET',
		url: '/someUrl'
	}).then(function successCallback(response) {
		// this callback will be called asynchronously
		// when the response is available
	}, function errorCallback(response) {
		// called asynchronously if an error occurs
		// or server returns response with an error status.
	});
```


## $http POST Method
### Send JSON format
In Angularjs, default post method send out JSON format.
```javascript
	$http({
		method: 'POST',
		url: '/someUrl'
		data: { test: 'test' }
	}).then(function successCallback(response) {
		// this callback will be called asynchronously
		// when the response is available
	}, function errorCallback(response) {
		// called asynchronously if an error occurs
		// or server returns response with an error status.
	});
```

### Send as Form Data
If you want all post method send out data as from data in current module ('app'), insert this into module config:
```javascript
	app.config(
	    function ($httpProvider) {
			$httpProvider.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
		}
	);	
```
Or you can directy apply it inside $http config:
```javascript
	var data = $.param({test: 'test' });
	$http({
		method: 'POST',
		url: '/someUrl'
		data: data
		headers: {'Content-Type': 'application/json'}
	}).then(function successCallback(response) {
		// this callback will be called asynchronously
		// when the response is available
	}, function errorCallback(response) {
		// called asynchronously if an error occurs
		// or server returns response with an error status.
	});
```