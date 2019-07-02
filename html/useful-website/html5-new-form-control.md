# HTML5 new Form Control

## form

The accept-charset attribute, which converts the entered data to UTF-8 and sends it to the server.

The novalidate attribute, which does not validate input data for this form. \(Ex. if email is specified in the input, only email addresses can be sent, but if novalidate is specified, no such input restrictions apply.\)

```markup
<form action="#" method="POST" novalidate="novalidate" accept-charset="UTF-8">
    ~

    <form></form>
</form>
```



## fieldset

The disabled property, which disables the contents of this field set.

Form attributes that can be transferred even if the field set is not in a form.

```markup
<!-- form's id and fieldset's form attribute's value is same-->
<fieldset disabled="disabled" form="go">
    <legend>Address</legend>
    <p>
        <label>email : <input type="email"/></label>
    </p>
</fieldset>
<form method="post" action="#" id="go">
    <input type="submit" value="submit" />
</form>
```



## input text

placeholder: Specify input hint

autofocus: Assign to element that will have focus automatically

required: Specify required entries

autocomplete: autocomplete on / off

```markup
<form action="#" method="POST" accept-charset="UTF-8">
    <fieldset>
        <legend>HTML5 form</legend>
        <p>
            <!-- If input has autofocus, the cursor will blink -->
            <!--  automatically at the location you specified. -->

            <!-- autocomplete keep the information you have sent, -->
            <!-- and if you hit a similar word, it will automatically show you the previous value -->

            <!-- By default, autocomplete is on, so if you want to turn it off, -->
            <!-- you should set it to off. -->
            <label for="username">User Name</label>
            <input
                type="text"
                name="username"
                id="username"
                value=""
                placeholder="Your Name"
                autofocus="autofocus"
                required="required"
                autocomplete="off"
            />
        </p>
    </fieldset>
    <button type="submit">Submit</button>
</form>
```

![](https://i.postimg.cc/qRHJk1Cr/HTML5-input.png)

alert "Fill out this field"



## input type = "email"

If type is email, it will be submitted when you do not enter @ value.

```markup
<form action="#" method="POST" accept-charset="UTF-8">
    <fieldset>
        <legend>HTML5 form</legend>
        <p>
            <!-- If input has autofocus, the cursor will blink -->
            <!--  automatically at the location you specified. -->

            <!-- autocomplete keep the information you have sent, -->
            <!-- and if you hit a similar word, it will automatically show you the previous value -->

            <!-- By default, autocomplete is on, so if you want to turn it off, -->
            <!-- you should set it to off. -->
            <label for="username">User Name</label>
            <input
                type="text"
                name="username"
                id="username"
                value=""
                placeholder="Your Name"
                autofocus="autofocus"
                required="required"
                autocomplete="off"
            />
        </p>
        <p>
            <label for="useremail">email</label>
            <input type="email" name="useremail" id="useremail" value="" />
        </p>
    </fieldset>
    <button type="submit">Submit</button>
</form>
```

![](https://i.postimg.cc/v8z0tDhL/HTML5-input-email.png)

alert "Please include '@' in your email address 'abc.com' does not have '@'."



## input type = "url"

If type is email, http:// or https:// required to transfer

```markup
<form action="#" method="POST" accept-charset="UTF-8">
    <fieldset>
        <legend>HTML5 form</legend>
        <p>
            <!-- If input has autofocus, the cursor will blink -->
            <!--  automatically at the location you specified. -->

            <!-- autocomplete keep the information you have sent, -->
            <!-- and if you hit a similar word, it will automatically show you the previous value -->

            <!-- By default, autocomplete is on, so if you want to turn it off, -->
            <!-- you should set it to off. -->
            <label for="username">User Name</label>
            <input
                type="text"
                name="username"
                id="username"
                value=""
                placeholder="Your Name"
                autofocus="autofocus"
                required="required"
                autocomplete="off"
            />
        </p>
        <p>
            <label for="useremail">email</label>
            <input type="email" name="useremail" id="useremail" value="" />
        </p>
        <p>
            <label for="userurl">Website</label>
            <input type="url" name="userurl" id="userurl" value="" />
        </p>
    </fieldset>
    <button type="submit">Submit</button>
</form>
```

![](https://i.postimg.cc/R0pPK0BV/HTML5-input-url.png)

alert "Please enter url"



## input type = "number"

The up and down arrows appear on the right of the input window and the quantity is adjustable.

min and max value can be set, initial value can be set by value, step can be set to change the range by one click.

```markup
<form action="#" method="POST" accept-charset="UTF-8">
    <fieldset>
        <legend>HTML5 form</legend>
        <p>
            <!-- If input has autofocus, the cursor will blink -->
            <!--  automatically at the location you specified. -->

            <!-- autocomplete keep the information you have sent, -->
            <!-- and if you hit a similar word, it will automatically show you the previous value -->

            <!-- By default, autocomplete is on, so if you want to turn it off, -->
            <!-- you should set it to off. -->
            <label for="username">User Name</label>
            <input
                type="text"
                name="username"
                id="username"
                value=""
                placeholder="Your Name"
                autofocus="autofocus"
                required="required"
                autocomplete="off"
            />
        </p>
        <p>
            <label for="useremail">email</label>
            <input type="email" name="useremail" id="useremail" value="" />
        </p>
        <p>
            <label for="userurl">Website</label>
            <input type="url" name="userurl" id="userurl" value="" />
        </p>
        <p>
            <label for="order">Order Quantity</label>
            <input
                type="number"
                name="order"
                id="order"
                min="1"
                max="20"
                value="3"
            />
        </p>
    </fieldset>
    <button type="submit">Submit</button>
</form>
```

![](https://i.postimg.cc/zBBG206F/HTML5-input-number.png)



## input type = "range"

If min is 0, max is 100, and step is 100, the bar does not move smoothly but moves by 10 units.

Value sets initial value.

```markup
<form action="#" method="POST" accept-charset="UTF-8">
    <fieldset>
        <legend>HTML5 form</legend>
        <p>
            <!-- If input has autofocus, the cursor will blink -->
            <!--  automatically at the location you specified. -->

            <!-- autocomplete keep the information you have sent, -->
            <!-- and if you hit a similar word, it will automatically show you the previous value -->

            <!-- By default, autocomplete is on, so if you want to turn it off, -->
            <!-- you should set it to off. -->
            <label for="username">User Name</label>
            <input
                type="text"
                name="username"
                id="username"
                value=""
                placeholder="Your Name"
                autofocus="autofocus"
                required="required"
                autocomplete="off"
            />
        </p>
        <p>
            <label for="useremail">email</label>
            <input type="email" name="useremail" id="useremail" value="" />
        </p>
        <p>
            <label for="userurl">Website</label>
            <input type="url" name="userurl" id="userurl" value="" />
        </p>
        <p>
            <label for="order">Order Quantity</label>
            <input
                type="number"
                name="order"
                id="order"
                min="1"
                max="20"
                value="3"
            />
        </p>
        <p>
            <label for="userrange">Length</label>
            <input
                type="range"
                name="userrange"
                id="userrange"
                min="0"
                max="100"
                step="10"
                value="30"
            />
        </p>
    </fieldset>
    <button type="submit">Submit</button>
</form>
```

![](https://i.postimg.cc/6p4HNKJ8/HTML5-input-range.png)



## input type = "tel"

tel does not check for validity and does not automatically put "-". It's because the standards are different in each country.

tel does not check for validity, but when you type tel on a mobile device, the number pad appears automatically.

```markup
<form action="#" method="POST" accept-charset="UTF-8">
    <fieldset>
        <legend>HTML5 form</legend>
        <p>
            <!-- If input has autofocus, the cursor will blink -->
            <!--  automatically at the location you specified. -->

            <!-- autocomplete keep the information you have sent, -->
            <!-- and if you hit a similar word, it will automatically show you the previous value -->

            <!-- By default, autocomplete is on, so if you want to turn it off, -->
            <!-- you should set it to off. -->
            <label for="username">User Name</label>
            <input
                type="text"
                name="username"
                id="username"
                value=""
                placeholder="Your Name"
                autofocus="autofocus"
                required="required"
                autocomplete="off"
            />
        </p>
        <p>
            <label for="useremail">email</label>
            <input type="email" name="useremail" id="useremail" value="" />
        </p>
        <p>
            <label for="userurl">Website</label>
            <input type="url" name="userurl" id="userurl" value="" />
        </p>
        <p>
            <label for="order">Order Quantity</label>
            <input
                type="number"
                name="order"
                id="order"
                min="1"
                max="20"
                value="3"
            />
        </p>
        <p>
            <label for="userrange">Length</label>
            <input
                type="range"
                name="userrange"
                id="userrange"
                min="0"
                max="100"
                step="10"
                value="30"
            />
        </p>
        <p>
            <label for="userTel">Tel Num</label>
            <input type="tel" name="userTel" id="userTel" value="" />
        </p>
    </fieldset>
    <button type="submit">Submit</button>
</form>
```

![](https://i.postimg.cc/XqvRfPZ9/HTML5-input-tel.png)



## input type = "date"

It may not work in other browsers other than Chrome

```markup
<form action="#" method="POST" accept-charset="UTF-8">
    <fieldset>
        <legend>HTML5 form</legend>
        <p>
            <!-- If input has autofocus, the cursor will blink -->
            <!--  automatically at the location you specified. -->

            <!-- autocomplete keep the information you have sent, -->
            <!-- and if you hit a similar word, it will automatically show you the previous value -->

            <!-- By default, autocomplete is on, so if you want to turn it off, -->
            <!-- you should set it to off. -->
            <label for="username">User Name</label>
            <input
                type="text"
                name="username"
                id="username"
                value=""
                placeholder="Your Name"
                autofocus="autofocus"
                required="required"
                autocomplete="off"
            />
        </p>
        <p>
            <label for="useremail">email</label>
            <input type="email" name="useremail" id="useremail" value="" />
        </p>
        <p>
            <label for="userurl">Website</label>
            <input type="url" name="userurl" id="userurl" value="" />
        </p>
        <p>
            <label for="order">Order Quantity</label>
            <input
                type="number"
                name="order"
                id="order"
                min="1"
                max="20"
                value="3"
            />
        </p>
        <p>
            <label for="userrange">Length</label>
            <input
                type="range"
                name="userrange"
                id="userrange"
                min="0"
                max="100"
                step="10"
                value="30"
            />
        </p>
        <p>
            <label for="userTel">Tel Num</label>
            <input type="tel" name="userTel" id="userTel" value="" />
        </p>
        <p>
            <label for="userdate">Date</label>
            <input
                type="date"
                name="userdate"
                id="userdate"
                min="2017-09-10"
                max="2019-12-31"
                value=""
            />
        </p>
    </fieldset>
    <button type="submit">Submit</button>
</form>
```

![](https://i.postimg.cc/hvLqPm75/HTML5-input-date.png)

Year-Month-Day



## input type = "color"

When you specify an initially visible value, place it in the value.

The code you are using is a hexadecimal number, starting with \#.

```markup
<form action="#" method="POST" accept-charset="UTF-8">
    <fieldset>
        <legend>HTML5 form</legend>
        <p>
            <!-- If input has autofocus, the cursor will blink -->
            <!--  automatically at the location you specified. -->

            <!-- autocomplete keep the information you have sent, -->
            <!-- and if you hit a similar word, it will automatically show you the previous value -->

            <!-- By default, autocomplete is on, so if you want to turn it off, -->
            <!-- you should set it to off. -->
            <label for="username">User Name</label>
            <input
                type="text"
                name="username"
                id="username"
                value=""
                placeholder="Your Name"
                autofocus="autofocus"
                required="required"
                autocomplete="off"
            />
        </p>
        <p>
            <label for="useremail">email</label>
            <input type="email" name="useremail" id="useremail" value="" />
        </p>
        <p>
            <label for="userurl">Website</label>
            <input type="url" name="userurl" id="userurl" value="" />
        </p>
        <p>
            <label for="order">Order Quantity</label>
            <input
                type="number"
                name="order"
                id="order"
                min="1"
                max="20"
                value="3"
            />
        </p>
        <p>
            <label for="userrange">Length</label>
            <input
                type="range"
                name="userrange"
                id="userrange"
                min="0"
                max="100"
                step="10"
                value="30"
            />
        </p>
        <p>
            <label for="userTel">Tel Num</label>
            <input type="tel" name="userTel" id="userTel" value="" />
        </p>
        <p>
            <label for="userdate">Date</label>
            <input
                type="date"
                name="userdate"
                id="userdate"
                min="2017-09-10"
                max="2019-12-31"
                value=""
            />
        </p>
        <p>
            <label for="usercolor">Color</label>
            <input type="color" name="usercolor" id="usercolor" value="" />
        </p>
    </fieldset>
    <button type="submit">Submit</button>
</form>
```

![](https://i.postimg.cc/52R26Z0d/HTML5-input-color.png)

