<nav class="fusiondoc-api-breadcrumbs">
	<a href="..">Fusion</a>
</nav>

<h1 class="fusiondoc-api-header" markdown>
	<span class="fusiondoc-api-icon" markdown>:octicons-x-circle-24:</span>
	<span class="fusiondoc-api-name">Errors</span>
</h1>

Whenever Fusion outputs any errors or messages to the console, it will have a
short error ID at the end. This is used to uniquely identify what kind of error
or message you're seeing.

Use the search box below to paste in or type an error ID, and it will scroll to
the details for you.

<input
    class="md-input md-input--stretch"
    placeholder="Type or paste an error ID here..."
/>

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.2</span>
</p>

## applyPropsNilRef

```
`applyInstanceProps` got a nil ref! (this is an internal issue)
```

Internally in Fusion, the [New](../instances/new) and [Hydrate](../instances/hydrate)
functions call a helper function, `applyInstanceProps`, to do the work of
binding properties and applying special keys. 

If that function is given `nil` instead of an instance, this error is thrown.
This could occur if internal code accidentally destroys an instance via garbage
collection, which could have large implications for projects using Fusion. The
error and reproduction steps should be reported as soon as possible.

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.1</span>
</p>

## cannotAssignProperty

```
The class type 'Foo' has no assignable property 'Bar'.
```

This message shows if you try to assign a non-existent or locked property using
the [New](../instances/new) or [Hydrate](../instances/hydrate) functions:

```Lua
local folder = New "Folder" {
	DataCost = 12345,
	ThisPropertyDoesntExist = "Example"
}
```

!!! tip
	Different scripts may have different privileges - for example, plugins will
	be allowed more privileges than in-game scripts. Make sure you have the
	necessary privileges to assign to your properties!

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.1</span>
</p>

## cannotConnectChange

```
The Frame class doesn't have a property called 'Foo'.
```

This message shows if you try to connect a handler to a non-existent property
change event when using the [New](../instances/new) or [Hydrate](../instances/hydrate)
functions:

```Lua
local textBox = New "TextBox" {
	[OnChange "ThisPropertyDoesntExist"] = function()
		...
	end)
}
```

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.1</span>
</p>

## cannotConnectEvent

```
The Frame class doesn't have an event called 'Foo'.
```

This message shows if you try to connect a handler to a non-existent event when
using the [New](../instances/new) or [Hydrate](../instances/hydrate) functions:

```Lua
local button = New "TextButton" {
	[OnEvent "ThisEventDoesntExist"] = function()
		...
	end)
}
```

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.1</span>
</p>

## cannotCreateClass

```
Can't create a new instance of class 'Foo'.
```

This message shows when using the [New](../instances/new) function with an
invalid class type:

```Lua
local instance = New "ThisClassTypeIsInvalid" {
	...
}
```

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.1</span>
</p>

## computedCallbackError

```
Computed callback error: attempt to index a nil value
```

This message shows when the callback of a [computed object](../computed)
encounters an error:

```Lua
local example = Computed(function()
	local badMath = 2 + "fish"
end)
```

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.2</span>
</p>

## duplicatePropertyKey

```
Can't assign to 'Name' twice.
```

This message shows if you try to declare the same property more than once when
using the [New](../instances/new) or [Hydrate](../instances/hydrate) functions:

```Lua
local button = New "TextButton" {
	Name = "Joseph"
}

Hydrate(button) {
	Name = "Simon" -- ambiguous! Is the name supposed to be Joseph or Simon?
}
```

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.2</span>
</p>

## invalidChangeHandler

```
The change handler for the 'Text' property must be a function.
```

This message shows if you try to give [OnChange](../instances/onchange)
something other than a function:

```Lua
local input = New "TextBox" {
	[OnChange "Text"] = "lemons"
}
```

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.2</span>
</p>

## invalidEventHandler

```
The handler for the 'Activated' event must be a function.
```

This message shows if you try to give [OnEvent](../instances/onevent)
something other than a function:

```Lua
local button = New "TextButton" {
	[OnEvent "Activated"] = "limes"
}
```

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.2</span>
</p>

## invalidPropertyType

```
'Frame.Size' expected a 'UDim2' type, but got a 'Color3' type.
```

When using the [New](../instances/new) or [Hydrate](../instances/hydrate)
functions, you can pass values to properties. If you pass a value of the wrong
type for that property, and Roblox can't convert it, this error will be shown.

```Lua
local ui = New "Frame" {
	Size = Computed(function()
        return Color3.new(1, 0, 0)
	end)
}
```

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.2</span>
</p>

## invalidRefType

```
Instance refs must be Value objects.
```

The [Ref](../instances/ref) key expects a [Value](../state/value) object so it
can store the instance reference inside of it. This error is thrown if it
receives something that is not a Value object.

```Lua
local thing = New "Part" {
	[Ref] = 2
}
```

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.2</span>
</p>

## invalidOutType

```
[Out] properties must be given Value objects.
```

Keys made using [Out](../instances/out) expect a [Value](../state/value) object
so they can store property values inside of it. This error is thrown if it
receives something that is not a Value object.

```Lua
local thing = New "Part" {
	[Out "Color"] = true
}
```

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.2</span>
</p>

## invalidOutProperty

```
The Part class doesn't have a property called 'Flobulator'.
```

This error is thrown if a property name is used with [Out](../instances/out)
which doesn't exist or can't be accessed.

```Lua
local value = Value()

local thing = New "Part" {
	[Out "Flobulator"] = value
}
```

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.1</span>
</p>

## invalidSpringDamping

```
The damping ratio for a spring must be >= 0. (damping was -0.50)
```

This message shows if you try to provide a damping ratio to a [spring](../animation/spring)
which is less than 0:

```Lua
local speed = 10
local damping = -12345
local spring = Spring(state, speed, damping)
```

Damping ratio must always be between 0 and infinity for a spring to be
physically simulatable.

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.1</span>
</p>

## invalidSpringSpeed

```
The speed of a spring must be >= 0. (speed was -2.00)
```

This message shows if you try to provide a speed to a [spring](../animation/spring) which
is less than 0:

```Lua
local speed = -12345
local spring = Spring(state, speed)
```

Since a speed of 0 is equivalent to a spring that doesn't move, any slower speed
is not simulatable or physically sensible.

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.1</span>
</p>

## mistypedSpringDamping

```
The damping ratio for a spring must be a number. (got a boolean)
```

This message shows if you try to provide a damping ratio to a [spring](../animation/spring)
which isn't a number:

```Lua
local speed = 10
local damping = true
local spring = Spring(state, speed, damping)
```

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.1</span>
</p>

## mistypedSpringSpeed

```
The speed of a spring must be a number. (got a boolean)
```

This message shows if you try to provide a speed to a [spring](../animation/spring) which
isn't a number:

```Lua
local speed = true
local spring = Spring(state, speed)
```

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.2</span>
</p>

## onDestroyNilRef

```
`onDestroy` got a nil ref! (this is an internal issue, was the instance lost too early?)
```

In order to track when an instance is destroyed by Roblox, Fusion uses an
internal function called `onDestroy`. If this function receives `nil` instead of
an instance, this error will be thrown. 

This may indicate that cleanup code is not getting registered properly
internally, which can lead to large memory leaks. For that reason, this should
be reported as soon as possible.

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.1</span>
</p>

## mistypedTweenInfo

```
The tween info of a tween must be a TweenInfo. (got a boolean)
```

This message shows if you try to provide a tween info to a [tween](../animation/tween)
which isn't a TweenInfo:

```Lua
local tweenInfo = true
local tween = Tween(state, tweenInfo)
```

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.2</span>
</p>

## springTypeMismatch

```
The type 'number' doesn't match the spring's type 'Color3'.
```

Some methods on [spring](../animation/spring) objects require incoming values to
match the types previously being used on the spring.

This message shows when an incoming value doesn't have the same type as values
used previously on the spring:

```Lua
local colour = State(Color3.new(1, 0, 0))
local colourSpring = Spring(colour)

colourSpring:addVelocity(Vector2.new(2, 3))
```

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.1</span>
</p>

## strictReadError

```
'Foo' is not a valid member of 'Bar'.
```

In Fusion, some tables may have strict reading rules. This is typically used on
public APIs as a defense against typos.

This message shows when trying to read a non-existent member of these tables.

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.1</span>
</p>

## unknownMessage

```
Unknown error: attempt to index a nil value
```

If you see this message, it's almost certainly an internal bug, so make sure to
get in contact so the issue can be fixed.

When Fusion code attempts to log a message, warning or error, it needs to
provide an ID. This ID is used to show the correct message, and serves as a
simple, memorable identifier if you need to look up the message later.
However, if that code provides an invalid ID, then the message will be replaced
with this one.

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.1</span>
</p>

## unrecognisedChildType

```
'number' type children aren't accepted as children in `New`.
```

This message shows when attempting to pass something as a child which isn't an
instance, table of instances, or state object containing an instance (when using
the [New](../new.md) function):

```Lua
local instance = New "Folder" {
	[Children] = {
		1, 2, 3, 4, 5,

		{true, false},

		State(Enum.Material.Grass)
	}
}
```

!!! note
	Note that state objects are allowed to store `nil` to represent the absence
	of an instance, as an exception to these rules.

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.1</span>
</p>

## unrecognisedPropertyKey

```
'number' keys aren't accepted in the property table of `New`.
```

When you create an instance in Fusion using [New](../new),
you can pass in a 'property table' containing properties, children, event and
property change handlers, etc.

This table is only expected to contain keys of two types:

- string keys, e.g. `#!Lua Name = "Example"`
- a few symbol keys, e.g. `#!Lua [OnEvent "Foo"] = ...`

This message shows if Fusion finds a key of a different type, or if the key
isn't one of the few symbol keys used in New:

```Lua
local folder = New "Folder" {
	[Vector3.new()] = "Example",

	"This", "Shouldn't", "Be", "Here"
}
```

-----

<p class="fusiondoc-api-pills">
	<span class="fusiondoc-api-pill-since">since v0.2</span>
</p>

## unrecognisedPropertyStage

```
'discombobulate' isn't a valid stage for a special key to be applied at.
```

Fusion provides a standard interface for defining [special keys](../instances/specialkey.md)
which can be used to extend the functionality of [New](../instances/new.md) or
[Hydrate](../instances/hydrate.md).

Within this interface, keys can select when they run using the `stage` field.
If an unexpected value is passed as the stage, then this error will be thrown
when attempting to use the key.

```Lua
local Example = {
	type = "SpecialKey",
	kind = "Example",
	stage = "discombobulate",
	apply = function() ... end
}

local folder = New "Folder" {
	[Example] = "foo"
}
```