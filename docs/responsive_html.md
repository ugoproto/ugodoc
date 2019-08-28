# Initial grid looks

<center>
<img src="../img/HTML_CSS/CSS_1.png" hspace=2 vspace=2>
</center>

Here is the HTML:

~~~html
<div class="container">
  <div>1</div>
  <div>2</div>
  <div>3</div>
  <div>4</div>
  <div>5</div>
  <div>6</div>
</div>
~~~

And the CSS:

~~~css
.container {
    display: grid;
    grid-template-columns: 100px 100px 100px;
    grid-template-rows: 50px 50px;
}
~~~

# Basic responsiveness with the fraction unit

CSS Grid brings with it a whole new value called a fraction unit: written like `fr`. It splits the container into as many fractions.

~~~css
.container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 50px 50px;
}
~~~

<center>
<img src="../img/HTML_CSS/CSS_2.gif" hspace=2 vspace=2>
</center>

If we change the grid-template-columns value to `1fr 2fr 1fr`, the second column will now be twice as wide as the two other columns:

<center>
<img src="../img/HTML_CSS/CSS_3.gif" hspace=2 vspace=2>
</center>

# Advanced responsiveness

## `repeat()`

highlight line 3

~~~css hl_lines="3"
.container {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-template-rows: repeat(2, 50px);
}
~~~

In other words, `repeat(3, 100px)` is identical to `100px 100px 100px`:

<center>
<img src="../img/HTML_CSS/CSS_4.png" hspace=2 vspace=2>
</center>

## `auto-fit`


      
highlight line 4

~~~css hl_lines="4"
.container {
    display: grid;
    grid-gap: 5px;
    grid-template-columns: repeat(auto-fit, 100px);
    grid-template-rows: repeat(2, 100px);
}
~~~

<center>
<img src="../img/HTML_CSS/CSS_5.gif" hspace=2 vspace=2>
</center>

The grid now varies the amount of columns with the width of the container.

## `minmax()`

highlight line 4

~~~css hl_lines="4"
.container {
    display: grid;
    grid-gap: 5px;
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
    grid-template-rows: repeat(2, 100px);
}
~~~

<center>
<img src="../img/HTML_CSS/CSS_6.gif" hspace=2 vspace=2>
</center>

The `minmax()` function defines a size range greater than or equal to min and less than or equal to max.

So the columns will now always be at least 100px. However if there are more available space, the grid will simply distribute this equally to each of the columns, as the columns turn into a fraction unit instead of 100 px.

# Adding the images

Now the final step is to add the images.

~~~html
<div><img src="img/forest.jpg"/></div>
~~~

To make the image fit into the item, we’ll set the it to be as wide and tall as the item itself, and then use `object-fit: cover;`. This will make the image cover its entire container, and the browser will crop it if it’s needed.

~~~css
.container > div > img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}
~~~

<center>
<img src="../img/HTML_CSS/CSS_7.gif" hspace=2 vspace=2>
</center>

---
