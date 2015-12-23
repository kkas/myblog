---
layout: post
title: How To Improve Forms (SWND course note)
---
This is my note for the following article.
[developers.google.com/web/fundamentals/design-and-ui/input/forms/](https://developers.google.com/web/fundamentals/design-and-ui/input/forms/?hl=en)

This note focuses on forms on mobiles.
This note is taken on my way to pursue my SWND at Udacity.

# Forms
* Fewest inputs is the best.
  * Forms with many inputs are hard to use, especially on mobile devices.
* The rate of Mobile shopping carts not being used is about 97%.

## TIPS for form improvement

* Reduce the number of questions

* Use `label` and name your input properly
  * [developers.google.com/web/fundamentals/design-and-ui/input/forms/label-and-name-inputs#use-metadata-to-enable-auto-complete](https://developers.google.com/web/fundamentals/design-and-ui/input/forms/label-and-name-inputs#use-metadata-to-enable-auto-complete)

* `label` element or `for` attributes for providing direction to the users.
  * using labels helps **touch target sizes**
    * Users able to touch labels and inputs

```html
<!-- Using input inside -->
<label>
  <input type="checkbox"> Remember me
</label>
```
```html
<!-- Using the 'for' attribute -->
<label for="frmAddressS">Address</label>
```

* Use `placeholder` attributes

```html
<label for="frmAddressS">Address</label>
<input id="frmAddressS" type="text" name="ship-address" placeholder="123 Any Street" autocomplete="shipping street-address"></input>
```

* Use standard naming conventions.
  * Do not use random values for input names or IDs
  * e.g. 'fname' for user's first name

* Have large tap targets

* Use correct input type, so that browser will know which keyboard fits the most useful.
  * e.g. type=`"datatime-local"`, `"email"`, `"url"`, `"number"`
  * [developers.google.com/web/fundamentals/design-and-ui/input/forms/choose-the-best-input-type](https://developers.google.com/web/fundamentals/design-and-ui/input/forms/choose-the-best-input-type?hl=en)
  * [developer.mozilla.org/en-US/docs/Web/HTML/Element/input#attr-type](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#attr-type)

* Good to use `datalist` element for a list of suggested input values to associated with a form filed
  * [developer.mozilla.org/en-US/docs/Web/HTML/Element/datalist](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/datalist)
  * `list` attribute in `input` tags needs to be matched with the id of `datalist` element.

```html
<label for="frmFavChocolate">Favorite Type of Chocolate</label>
<input type="text" name="fav-choc" id="frmFavChocolate" list="chocType">
<datalist id="chocType">
  <option value="white">
  <option value="milk">
  <option value="dark">
</datalist>
```

* Provide the users a lot of feedback
  * Let the users know immediately what needs to be changed by providing the client-side validation
  * [developers.google.com/web/fundamentals/design-and-ui/input/forms/provide-real-time-validation](https://developers.google.com/web/fundamentals/design-and-ui/input/forms/provide-real-time-validation?hl=en)
  * `pattern` attribute
    * regular expression for validation

```html
<input type="text" pattern"^\d{5,6}(?:[-\s]\d{4})?$" ...
```

  * `required` attribute
    * the users must input the value before the form can be submitted

```html
<input id="frmAddressS" type="text" required name="ship-address" placeholder="123 Any Street" autocomplete="shipping street-addres">
```

  * 'numeric' input types: e.g `min`, `max`, `step` attributes
    * these are adjusted by the sliders or spinners

```html
<input type="number" min="1" max="13" step="0.5">
```

  * `maxlength` attribute
    * limit the max length of inputs

```html
<input type="text" maxlength="12" ...
```

* Use the constraint validation API if these above validations are not enough.
  * catch the `submit` event and add the checkValidity method to make sure that everything is ok.
  * **requestAutocomplete**
    * Tutorial: [goo.gl/7In2Np](http://goo.gl/7In2Np)
    * Demo: [goo.gl/8zOt9R](http://goo.gl/8zOt9R)

```javascript
(form.js)
form.addEventListener("submit", function(evt) {
  if (form.checkValidity() === false) {
    evt.preventDefault();
    // Notify the user the form is incorrect here..
    return false;
  }
});
```

## Wrapup

* Minimize repeated actions and fields
  * Use existing data to pre-populate fields and be sure to enable auto-fill.
* Show users how far along they are
  * Use clearly-labeled progress bars to help users get through multi-part forms.
* Provide visual calendars when selecting dates
  * Provide visual calendar so users don’t have to leave your site and jump to the calendar app on their smartphones.


## Other Links
* Geolocation API
  * Ido's Geolocaiton example
    * [codepen.io](http://codepen.io/greenido/pen/qOEbGp)
  * HTML5Rocks Geolocation example
    * [www.html5rocks.com/en/tutorials/geolocation/trip_meter/](http://www.html5rocks.com/en/tutorials/geolocation/trip_meter/)
