## 1. CSS Specificity

#### Usage

```js
var a = document.querySelector("h1"); // selects one h1

var h = document.querySelectorAll("h1"); // node list
h.forEach(function (e) {
  console.log(e);
}) >> document.getElementByID(""),
  document.getElementByClass("");
```

## 2. Changing HTML

```js
a.innerHTML = "<h5>text<h5>";
```

- a.textContent = "`<h5>`text`<h5>`"

## 3. Changing CSS

```js
a.style.color = "red";
a.style.backgroundColor = "black"; // use camel case
```

## 4. Event Listener

```js
a.addEventListener("click", function () {
  console.log("Hey");
  a.innnerHTML("new text");
});
```

## Injecting custom js on runtime/compiletime

### Template Literals

- use backtick to define html inside strings

```js
    var clutter = `<h1>This is injected text<h1>`

    document.querySelector(".heading") = clutter
```

- Template literals provide an easy way to interpolate variables and expressions into strings. The method is called **string interpolation**

```js
    var clutter = `<h1>The number is ${num}<h1>`

    document.querySelector(".heading") = clutter
```
