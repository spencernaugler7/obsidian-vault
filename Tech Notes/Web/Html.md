---
tags:
  - web
  - tech
  - reference
source: https://www.w3schools.com/tags/
---
# Checkbox

#### Unchecked
```html
<input type="checkbox" id="vehicle2" name="vehicle2" value="Car" />  
<label for="vehicle2"> I have a car</label><br>
```

> [!example] Example
> <input type="checkbox" name="vehicle2" />
#### Checked
```html
<input type="checkbox" id="vehicle2" name="vehicle2" value="Car" />  
<label for="vehicle2"> I have a car</label><br>
```

> [!example]
> <input type="checkbox" name="vehicle2" checked />

___
# Script
#### Inline js
```html
<script>  
let x = 2
console.log(x);
</script>
```

#### Import  libarary via CDN
```html
<script type="module" src="https://cdn.jsdelivr.net/gh/starfederation/datastar@v1.0.2/bundles/datastar.js"></script>
```
___
# Button

```html
<button id="testId" onclick="window.alert('Hello');">Click Me!</button>
```

> [!example]
> <button type="button" onclick="window.alert('Hello');">Click Me!</button>

___
# Table

```html
<table>
  <caption>
    Front-end web developer course 2021
  </caption>
  <thead>
    <tr>
      <th scope="col">Person</th>
      <th scope="col">Most interest in</th>
      <th scope="col">Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Chris</th>
      <td>HTML tables</td>
      <td>22</td>
    </tr>
    <tr>
      <th scope="row">Dennis</th>
      <td>Web accessibility</td>
      <td>45</td>
    </tr>
    <tr>
      <th scope="row">Sarah</th>
      <td>JavaScript frameworks</td>
      <td>29</td>
    </tr>
    <tr>
      <th scope="row">Karen</th>
      <td>Web performance</td>
      <td>36</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <th scope="row" colspan="2">Average age</th>
      <td>33</td>
    </tr>
  </tfoot>
</table>
```

<table>
  <caption>
    Front-end web developer course 2021
  </caption>
  <thead>
    <tr>
      <th scope="col">Person</th>
      <th scope="col">Most interest in</th>
      <th scope="col">Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Chris</th>
      <td>HTML tables</td>
      <td>22</td>
    </tr>
    <tr>
      <th scope="row">Dennis</th>
      <td>Web accessibility</td>
      <td>45</td>
    </tr>
    <tr>
      <th scope="row">Sarah</th>
      <td>JavaScript frameworks</td>
      <td>29</td>
    </tr>
    <tr>
      <th scope="row">Karen</th>
      <td>Web performance</td>
      <td>36</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <th scope="row" colspan="2">Average age</th>
      <td>33</td>
    </tr>
  </tfoot>
</table>
