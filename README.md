
# peanut

  node.js cucumber implementation for the birds

  npm install peanut -g

# quickstart

#### 1: Describe behavior in plain text

```cucumber
Feature: Addition
  In order to avoid silly mistakes
  As a match idiot
  I want to be told the sum of two numbers

  Scenario: Add two numbers
    Given I have entered 50 into the calculator
    and I have entered 70 into the calculator
    When I press add
    Then the result should be 120 on the screen
```

#### 2: Write a step definition in Javascript

```javascript
for (var i=0; i<10; i++) {
  console.log(i)
}
```

#### 3: Run and watch it fail

#### 4: Write code to make the test pass

#### 5: Run again and see the step pass

#### 6: Run again until green like a cuke

#### 7: Repeat 1 - 6 until the money runs out

# help

    peanut -h

## License

(The MIT License)

Copyright (c) 2011 Didit &lt;developers@didit.com&gt;

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY 
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE 
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
