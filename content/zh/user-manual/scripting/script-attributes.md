---
title: Script Attributes
template: usermanual-page.tmpl.html
position: 4
---

Script Attributes are a powerful feature that lets you expose values from your script files so that they appear in the PlayCanvas Editor. This means you can write code once, and then tweak values on different instances of an Entity to give them different properties. This is perfect for exposing properties for artists, designers or other non-programmer team members so that they are able to adjust and modify values without writing code.

## Declaring Script Attributes

Script Attributes are declared at the top of your script file using this format:

```javascript
var MyScript = pc.createScript("myscript");

MyScript.attributes.add("speed", "number", 80);
```

In this example, we're declaring a property called `speed` which is a `number` and has a default value of `80`:

## Getting Attributes into Editor

<img src="/images/user-manual/scripting/script-attributes.jpg" style="width: 300px; float: right; padding: 20px; padding-top: 0px;"/>

Once you've declared your attributes the Editor needs to parse the code in order to expose the script attributes. The code is parsed automatically when you add a script to an entity. However, if you ever need to manually refresh the attributes you can click the parse <img src="/images/user-manual/scripting/parse-button.jpg" style="display: inline; vertical-align: middle;" /> button.

## Accessing attributes in your code

When you declare an attribute in your script it will be available as a member variable on your script instance. For example, the `speed` property declared above is available as `this.speed`.

```javascript
MyScript.prototype.update = function (dt) {
    this.entity.translate(this.speed * dt, 0, 0);
}
```

## Updating attributes

When you modify an attribute in the editor the changes are sent to any copies of the application launched from the editor. This means you can live edit your attributes without reloading your application. If you need to apply special behaviour when an attribute changes. Use the `attr` and `attr:[name]` events to respond to changes

```javascript
MyScript.prototype.initialize = function () {
    // fires only for `speed` attribute
    this.on("attr:speed", function (value, prev) {
        // new value for speed
    });

    // fires for all attribute changes
    this.on("attr", name, value, prev) {
        // new attribute value
    }
}
```

## Attribute types

When you declare an attribute you also declare the type of the attribute. This allows the editor to show the relevant controls for you to edit the attribute. Most types are self-explanatory, for example, "boolean", number" or "string". But some require some further explanation in the below examples. See the [full attribute reference][1] for more details.

### Entity attribute

```javascript
MyScript.attributes.add("target", {type: "entity"})
```

The Entity type lets your reference another entity in your hierarchy. A great way to link two entities together.

### Asset attribute

```javascript
MyScript.attributes.add("texture", {type: "asset", assetType: "texture", array: true});
```

The Asset attribute let's you reference a project asset in your script. The asset attribute also supports the `array` property to let you specify a list of assets, and the `assetType` property which limits the attribute to assets of a particular type, e.g. "texture", "material", "model".

### Color attribute

```javascript
MyScript.attributes.add("color", {type: "rgba"});
```

The color attribute shows a color picker when exposed in the editor. There are two options `rgb` and `rgba` depending on whether you wish to expose the alpha channel as well.

### Curve attribute

```javascript
MyScript.attributes.add("wave", {type: "curve"}); // one curve
MyScript.attributes.add("wave", {type: "curve", curves: ['x', 'y', 'z']}); // three curves: x, y, z
MyScript.attributes.add("wave", {type: "curve", color: 'r'}); // one curve for red channel
MyScript.attributes.add("wave", {type: "curve", color: 'rgba'}); // four curves for full color including alpha
```

The curve attribute is used to express a value that changes over a time period. All curves are defined over the period 0.0 - 1.0. You can define multiple curves, for example if you wish to have a 3D position from a curve defined three curves for x,y,z using the `curves` property. There is also a special curve editor for modifying colors using the `color` property.

### Enumeration attribute

The last special attribute type is the Enumeration attribute

```javascript
MyScript.attributes.add("value", {
    type: "number",
    enum: [
        {'valueOne': 1},
        {'valueTwo': 2},
        {'valueThree': 3}
    ]
});
```

Use the enum property to declare the list of possible values for your enumeration.

[1]: /api/pc.ScriptAttributes.html
