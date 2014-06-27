angular-time-format
===================

AngularJS filter for formatting time.

## Usage ##
Add `angular-time-format` as your app dependency.

```
  angular.module('myModule', [
    angular-time-format'
  ]);
```

In templates you can use
```
  <p>
    Time passed: {{ passed | time:'hh:mm:ss:sss' }}<br/>
    Preformatted: {{ passedPre }}
  </p>
```

In controllers (or directives, services, everywhere)
```
  angular.module('myModule').controller('exampleCtrl', function($scope, $filter) {
    var timeFilter = $filter('time');
    
    $scope.passed = 123456789;
    $scope.passedPre = timeFilter($scope.passed, 'hh:mm:ss:sss');
  });
```

The result should be the same in both cases:
```
  Time passed: 34:17:36:789
  Preformatted: 34:17:36:789
```

## Format options ##
Available formatting options:
 * (y)ear
 * (d)ay
 * (h)our
 * (m)inute
 * (s)econd
 * `sss` for milliseconds

Each number will be zero-padded to two places if you double letters (ex. `hh`, `mm`). Milliseconds are exception - they are padded to four places and you have to pass four letters (`ssss`).

You can use all kind of separator you want, but be careful. Passing format `h hours, m minutes` will produce unexpected results `34 34ours, 17 17inutes`. To avoid that, wrap every separator containing reserved letters in quotaion marks, like that `h 'hours', m 'minutes'`. (remember about escape them in your code!). Now, the result should be nicely `34 hours, 17 minutes`.

## Additional notes ##
Note, that you can ommit some unit "levels", but it can produce weird results. If in example above you change format to `hh:mm`, result will be `34:1056`, because 17 minutes and 36 seconds it is 1056 seconds.
 
