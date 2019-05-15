# Form Control

### form

You can apply actions and methods attributes in `<form>`. action is the URI of the program that will process the contents of the field.

The method defines the way in which it is sent, with get and post methods.

The get method sends the contents of the form to the URI specified in action by adding '?' usually we specify a post method that does not appear in the URI because of security issues.

```markup
<form action="action.jsp" method="post">
    ~
</form>
```

get

![](https://i.postimg.cc/T3GMgrhd/form-get-url.png)

### fieldset

To group forms, you can apply a `<fieldset>` and name it as a `<legend>`, and it can only come once in a fieldset.

```markup
<form action="action.jsp" method="post">
    <fieldset>
        <legend>name of form</legend>
    </fieldset>
</form>
```

![](https://i.postimg.cc/pL7SkzL5/fieldset.png)

### input

`<input>` is an empty element and you can create various kinds of controls with the type attribute. Enter the title of each control with the label element.

Specify an id for the control, and specify the same name on `<label>`'s "for" attribute to set explicit name.

The name attribute of the input is the key value when the data is transmitted.

If you write a label, you can also click on the "User Name" in the label to go to the associated input.

If you enter value, it will be displayed in input area before user enter\(you do not have to write\)

The "value" is the value that the user entered and it will be transmitted as a value.

```markup
<form action="action.jsp" method="post">
    <fieldset>
        <legend>name of form</legend>
        <label for="name">User Name</label>
        <input type="text" name="name" id="name" value="" />
    </fieldset>
</form>
```

![](https://i.postimg.cc/4dWHhrtz/input-label.png)

### input type = "text"

One-line text input, ID, name, e-mail, address and so on.

size = "size": Size of how many characters can fit.

maxlength = "number": maximum number of characters that can be entered.

```markup
<form action="action.jsp" method="post">
    <fieldset>
        <legend>name of form</legend>
        <label for="name">User Name</label>
        <input
            type="text"
            name="name"
            id="name"
            value=""
            size="10"
            maxlength="8"
            title="put your name here"
            placeholder="Your Name"
        />
    </fieldset>
</form>
```

![](https://i.postimg.cc/G2tgYnVR/input-text.png)

### input type = "password"

```markup
<form action="action.jsp" method="post">
    <fieldset>
        <legend>name of form</legend>
        <!--  Each item can be wrapped with p div ul or li -->
        <p>
            <label for="name">User Name</label>
            <input
                type="text"
                name="name"
                id="name"
                value=""
                size="10"
                maxlength="8"
                title="put your name here"
                placeholder="Your Name"
            />
        </p>
        <p>
            <label for="userpass">Password</label>
            <input type="password" name="userpass" id="userpass" value="" />
        </p>
    </fieldset>
</form>
```

![](https://i.postimg.cc/gjFYBsvx/input-password.png)

### input type = "checkbox"

Multiple selection possible

```markup
<form action="action.jsp" method="post">
    <fieldset>
        <legend>name of form</legend>
        <!--  Each item can be wrapped with p div ul or li -->
        <p>
            <label for="name">User Name</label>
            <input
                type="text"
                name="name"
                id="name"
                value=""
                size="10"
                maxlength="8"
                title="put your name here"
                placeholder="Your Name"
            />
        </p>
        <p>
            <label for="userpass">Password</label>
            <input type="password" name="userpass" id="userpass" value="" />
        </p>
        <p>
            <!-- checkbox must have different name values. -->
            <span>Hobby?</span>
            <label for="trip">trip</label>
            <input type="checkbox" name="trip" id="trip" value="trip" />
            <label for="read">read</label>
            <input type="checkbox" name="read" id="read" value="read" />
            <label for="movie">movie</label>
            <input type="checkbox" name="movie" id="movie" value="movie" />
        </p>
        <p>
            <!-- Here lets make it simpler -->
            <!--  Inside the label, remove the for in <label> and id in <input> -->
            <!--  then put the <input> into the <label> -->

            <span>Hobby?</span>
            <label>trip<input type="checkbox" name="trip" value="trip"/></label>

            <label>read<input type="checkbox" name="read" value="read"/></label>

            <label
                >movie<input type="checkbox" name="movie" value="movie"
            /></label>
        </p>
    </fieldset>
</form>
```

![](https://i.postimg.cc/fbbmwcJ2/input-checkbox.png)



### input type = "radio"

Multiple selection impossible

```markup
<form action="action.jsp" method="post">
    <fieldset>
        <legend>name of form</legend>
        <!--  Each item can be wrapped with p div ul or li -->
        <p>
            <label for="name">User Name</label>
            <input
                type="text"
                name="name"
                id="name"
                value=""
                size="10"
                maxlength="8"
                title="put your name here"
                placeholder="Your Name"
            />
        </p>
        <p>
            <label for="userpass">Password</label>
            <input type="password" name="userpass" id="userpass" value="" />
        </p>
        <p>
            <!-- checkbox must have different name values -->
            <span>Hobby?</span>
            <label for="trip">trip</label>
            <input type="checkbox" name="trip" id="trip" value="trip" />
            <label for="read">read</label>
            <input type="checkbox" name="read" id="read" value="read" />
            <label for="movie">movie</label>
            <input type="checkbox" name="movie" id="movie" value="movie" />
        </p>
        <p>
            <!-- Here lets make it simpler -->
            <!--  Inside the label, remove the for in <label> and id in <input> -->
            <!--  then put the <input> into the <label> -->

            <span>Hobby?</span>
            <label>trip<input type="checkbox" name="trip" value="trip"/></label>

            <label>read<input type="checkbox" name="read" value="read"/></label>

            <label
                >movie<input type="checkbox" name="movie" value="movie"
            /></label>
        </p>
        <p>
            <!-- radio must have same name values -->
            <!-- to connect all options so that only one can be selected -->
            <!-- You can easily create it simpler with same way as above(checkbox) -->
            <span>Sex</span>
            <label for="male">Man</label>
            <input type="radio" name="choice" id="male" value="male" />
            <label for="female">Woman</label>
            <input type="radio" name="choice" id="female" value="female" />
        </p>
    </fieldset>
</form>
```

![](https://i.postimg.cc/v86QJ4HW/input-radio.png)

### Other input types

* `<input type="submit">` submit button
* `<input type="reset">` reset button
* `<input type="button">`is not working on ISO-HTML
  * `<button type="button"></button>` is recommended
* `<input type="image" src="button.gif" alt="submit">` is not working on ISO-HTML
  * `<button type="submit"><img src="image.gif" alt="submit"></button>` is recommended
* `<input type="file">` Transfer file selection field, attachment
* `<input type="hidden">` Create hidden fields. Specify data to be transferred to the program without displaying it on the screen

### textarea

Inline element that produces a multiline text field. Textarea element: cols = "width" rows = "lines" attributes are required.

```markup
<form action="action.jsp" method="post">
    <fieldset>
        <legend>name of form</legend>
        <!--  Each item can be wrapped with p div ul or li -->
        <p>
            <label for="name">User Name</label>
            <input
                type="text"
                name="name"
                id="name"
                value=""
                size="10"
                maxlength="8"
                title="put your name here"
                placeholder="Your Name"
            />
        </p>
        <p>
            <label for="userpass">Password</label>
            <input type="password" name="userpass" id="userpass" value="" />
        </p>
        <p>
            <!-- checkbox must have different name values -->
            <span>Hobby?</span>
            <label for="trip">trip</label>
            <input type="checkbox" name="trip" id="trip" value="trip" />
            <label for="read">read</label>
            <input type="checkbox" name="read" id="read" value="read" />
            <label for="movie">movie</label>
            <input type="checkbox" name="movie" id="movie" value="movie" />
        </p>
        <p>
            <!-- Here lets make it simpler -->
            <!--  Inside the label, remove the for in <label> and id in <input> -->
            <!--  then put the <input> into the <label> -->

            <span>Hobby?</span>
            <label>trip<input type="checkbox" name="trip" value="trip"/></label>

            <label>read<input type="checkbox" name="read" value="read"/></label>

            <label
                >movie<input type="checkbox" name="movie" value="movie"
            /></label>
        </p>
        <p>
            <!-- radio must have same name values -->
            <!-- to connect all options so that only one can be selected -->
            <!-- You can easily create it simpler with same way as above(checkbox) -->
            <span>Sex</span>
            <label for="male">Man</label>
            <input type="radio" name="choice" id="male" value="male" />
            <label for="female">Woman</label>
            <input type="radio" name="choice" id="female" value="female" />
        </p>
        <p>
            <label for="usercomm">Opinion</label>
            <textarea
                name="usercomm"
                id="usercomm"
                cols="30"
                rows="10"
            ></textarea>
            <!-- Do not line-break when textarea tag is closed. -->
            <!-- Must be in same line <textarea></textarea> -->
        </p>
    </fieldset>
</form>
```

![](https://i.postimg.cc/SQ9twvJx/form-textarea.png)

### select, option

`<select>` that selects arbitrary items from multiple items. Used with the `<option>`

If you specify a value for an `<option>`, the value is sent to the server.

```markup
<form action="action.jsp" method="post">
    <fieldset>
        <legend>name of form</legend>
        <!--  Each item can be wrapped with p div ul or li -->
        <p>
            <label for="name">User Name</label>
            <input
                type="text"
                name="name"
                id="name"
                value=""
                size="10"
                maxlength="8"
                title="put your name here"
                placeholder="Your Name"
            />
        </p>
        <p>
            <label for="userpass">Password</label>
            <input type="password" name="userpass" id="userpass" value="" />
        </p>
        <p>
            <!-- checkbox must have different name values -->
            <span>Hobby?</span>
            <label for="trip">trip</label>
            <input type="checkbox" name="trip" id="trip" value="trip" />
            <label for="read">read</label>
            <input type="checkbox" name="read" id="read" value="read" />
            <label for="movie">movie</label>
            <input type="checkbox" name="movie" id="movie" value="movie" />
        </p>
        <p>
            <!-- Here lets make it simpler -->
            <!--  Inside the label, remove the for in <label> and id in <input> -->
            <!--  then put the <input> into the <label> -->

            <span>Hobby?</span>
            <label>trip<input type="checkbox" name="trip" value="trip"/></label>

            <label>read<input type="checkbox" name="read" value="read"/></label>

            <label
                >movie<input type="checkbox" name="movie" value="movie"
            /></label>
        </p>
        <p>
            <!-- radio must have same name values -->
            <!-- to connect all options so that only one can be selected -->
            <!-- You can easily create it simpler with same way as above(checkbox) -->
            <span>Sex</span>
            <label for="male">Man</label>
            <input type="radio" name="choice" id="male" value="male" />
            <label for="female">Woman</label>
            <input type="radio" name="choice" id="female" value="female" />
        </p>
        <p>
            <label for="usercomm">Opinion</label>
            <textarea
                name="usercomm"
                id="usercomm"
                cols="30"
                rows="10"
            ></textarea>
            <!-- Do not line-break when textarea tag is closed. -->
            <!-- Must be in same line <textarea></textarea> -->
        </p>
        <p>
            <label for="usersel">Location</label>

            <!-- In the above, the value entered by the user is value -->
            <!-- but here, for example, the value of Seoul may be given as the value of Seoul -->
            <!-- However, it is easier to simply use values such as 1, 2, 3, and 4  -->
            <!-- if you have specific values you have created for interoperability with the server  -->
            <select name="usersel" id="usersel">
                <option value="1">Seoul</option>
                <option value="2">Daejeon</option>
                <option value="3">Daegu</option>
                <option value="4">Busan</option>
            </select>
        </p>
    </fieldset>
</form>
```

![](https://i.postimg.cc/WpMthsdL/form-select-and-option.png)

### button

The submit does not have to be in the fieldset.

You can also make the same function with the `<button>`.

It has the same performance and function with `<input>`, but the `<input>` has no closing tag and `<button>` has the closing tag, so for example, we can put an icon between `<button>` tags, but `<input>` must use CSS to do the same work.

```markup
<form action="action.jsp" method="post">
    <fieldset>
        <legend>name of form</legend>
        <!--  Each item can be wrapped with p div ul or li -->
        <p>
            <label for="name">User Name</label>
            <input
                type="text"
                name="name"
                id="name"
                value=""
                size="10"
                maxlength="8"
                title="put your name here"
                placeholder="Your Name"
            />
        </p>
        <p>
            <label for="userpass">Password</label>
            <input type="password" name="userpass" id="userpass" value="" />
        </p>
        <p>
            <!-- checkbox must have different name values -->
            <span>Hobby?</span>
            <label for="trip">trip</label>
            <input type="checkbox" name="trip" id="trip" value="trip" />
            <label for="read">read</label>
            <input type="checkbox" name="read" id="read" value="read" />
            <label for="movie">movie</label>
            <input type="checkbox" name="movie" id="movie" value="movie" />
        </p>
        <p>
            <!-- Here lets make it simpler -->
            <!--  Inside the label, remove the for in <label> and id in <input> -->
            <!--  then put the <input> into the <label> -->

            <span>Hobby?</span>
            <label>trip<input type="checkbox" name="trip" value="trip"/></label>

            <label>read<input type="checkbox" name="read" value="read"/></label>

            <label
                >movie<input type="checkbox" name="movie" value="movie"
            /></label>
        </p>
        <p>
            <!-- radio must have same name values -->
            <!-- to connect all options so that only one can be selected -->
            <!-- You can easily create it simpler with same way as above(checkbox) -->
            <span>Sex</span>
            <label for="male">Man</label>
            <input type="radio" name="choice" id="male" value="male" />
            <label for="female">Woman</label>
            <input type="radio" name="choice" id="female" value="female" />
        </p>
        <p>
            <label for="usercomm">Opinion</label>
            <textarea
                name="usercomm"
                id="usercomm"
                cols="30"
                rows="10"
            ></textarea>
            <!-- Do not line-break when textarea tag is closed. -->
            <!-- Must be in same line <textarea></textarea> -->
        </p>
        <p>
            <label for="usersel">Location</label>

            <!-- In the above, the value entered by the user is value -->
            <!-- but here, for example, the value of Seoul may be given as the value of Seoul -->
            <!-- However, it is easier to simply use values such as 1, 2, 3, and 4  -->
            <!-- if you have specific values you have created for interoperability with the server  -->
            <select name="usersel" id="usersel">
                <option value="1">Seoul</option>
                <option value="2">Daejeon</option>
                <option value="3">Daegu</option>
                <option value="4">Busan</option>
            </select>
        </p>
    </fieldset>
    <p>
        <input type="submit" value="submit" />
        <button type="submit">submit1</button>
        <input type="reset" value="reset" />
        <button type="reset">reset1</button>
    </p>
</form>
```

![](https://i.postimg.cc/HkQCtLCd/form-button.png)

