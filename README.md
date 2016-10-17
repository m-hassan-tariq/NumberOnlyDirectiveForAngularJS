# Number Only Directive For AngularJS
Custom AngularJS directive to allow number only as per user key input or through paste/cut

Here I show how to use AngularJS directive to allow only numbers to be entered in a textbox. This is useful for phone numbers, IDs, ZipCodes, and, well, that’s about it.

### Features
- On key input.
- With pasted text (right click & ctrl+v).
- With cut text (right click & ctrl+x).
- With pre-loaded text.

#### Angular Code:

      (function () {
          'use strict';

          angular
              .module('sampleApp', [])
              .directive('numbersOnly', numbersOnly);

          numbersOnly.$inject = [];

          function numbersOnly() {

              var directive = {
                  restrict: 'A',
                  require: 'ngModel',
                  link: function (scope, element, attr, ngModelCtrl) {
                      function fromUser(text) {
                          if (text) {
                              var transformedInput = text.replace(/[^0-9-]/g, '');
                              if (transformedInput !== text) {
                                  ngModelCtrl.$setViewValue(transformedInput);
                                  ngModelCtrl.$render();
                              }
                              return transformedInput;
                          }
                          return undefined;
                      }
                      ngModelCtrl.$parsers.push(fromUser);
                  }
              };
              return directive;
          };
      })();

#### Angular HTML Code:

    <input type="text" name="txtAccountNumber" numbers-only ng-model="account">
    
### Update:

I have tested on chrome/firefox/IE 9+, It is working fine,  It doesn’t allow space even.

For all those have issues like not working in specific browser or space(' ') character is allowed etc, please make sure there are no integration issues by inspecting browser console window. Please update your browser versions.

P.S. ng-model attribute is required to use that directive

    <input type="text" name="txtAccountNumber" numbers-only ng-model="account">
      
#### After user input through keystrokes:

![screenshot_5](https://cloud.githubusercontent.com/assets/10474169/19459612/c44420c0-9499-11e6-9a60-60bc0f7065a7.png)
