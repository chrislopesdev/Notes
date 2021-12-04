# THE DOM (Document Object Model)

## querySelector and query SelectorAll

There is a simple method to get elements on the page:

```javascript
document.querySelector("#id-name"); // grab item by id
document.querySelector(".class-name"); // grab item by class
document.querySelector("p"); // grab item by tag name

document.querySelectorAll(".blue"); // this will grab all elements with a class of blue
```

</br>

## The methods below are older

```javascript
document.getElementById("identifier");
document.getElementsByTagName("p");
document.getElementsByClassName("class-name");
```

</br>

## Finding an Element by its ID

```html
<p id="unique-id-name">This paragraph is unique.</p>
```

To find something by its `id` attribute use:

```javascript
document.getElementById("unique-id-name");
```

</br>

## Finding Elements by their Tag Name

When you want to find a set of elements that use the same HTML tag.

```html
<p>The 'Tag Name' of this element is 'p'</p>
```

We can find elements by their Tag Name in javascript using:

```javascript
document.getElementsByTagName("p");
```

</br>

## Finding Elements by their Class Name

When you want to find a set of elements that have the same class attribute.

```html
<p class="blue">This is a blue paragraph.</p>
```

We can find these by using the class name selector:

```javascript
document.getElementsByClassName("blue");
```
