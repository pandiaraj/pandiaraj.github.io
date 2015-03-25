---
layout: post
title: AngularJS ng-repeat Sort Order 
summary: By default AngularJS ng-repeat will sort the values and display them in ascending order.  
---

By default AngularJS ng-repeat will sort the values and display them in ascending order. But sometimes, we may need to show the values in insertion order. To do that, we have to override Javascript's Object.keys method. 

Lets say, we have a map (country code as key and name as value) and we want to display the key and values in a checkbox group. If we use ng-repeat like,

    <div ng-repeat=(key, value) in applicableCountries">
      <input type="checkbox" name="applicableCountries[]" value="{ {key} }">{ {value} }
    </div>

it will sort the keys in ascending order and display the checkboxes. But if we want to display the checkboxes in the insertion order, we need to override the Object.keys method,

    $scope.keys = function(obj) {
       return obj ? Object.keys(obj) : [];
    };

and in the ng-repeat,

    <div ng-repeat="key in keys(applicableCountries)">
      <input type="checkbox" value="{ {key} }>{ {applicableCountries[key]} }
    </div>

Now it will display the checkboxes in insertion order.
