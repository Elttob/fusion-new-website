Up until this point, we have been creating and parenting instances directly to
the data model without much organisation or code reuse. However, those two
factors will become increasingly important as you start building more game-ready
UIs.

These next few pages won't introduce new features of Fusion, but instead will
focus on techniques for making your UI more modular, portable and easy to
maintain.

-----

## The Component Pattern

One of the greatest advantages of libraries like Fusion is that UI and code are
the same thing. Any tool that we can use on one, we can use on the other.

To reduce repetition in our codebases, we often use functions to run small
reusable blocks of code, sometimes with parameters we can change. We can use
functions to organise our UI code, too.

For example, consider this function, which generates a button based on some
`props` the user passes in:

```Lua
local function Button(props)
    return New "TextButton" {
        BackgroundColor3 = Color3.new(0, 0.25, 1),
        Position = props.Position,
        AnchorPoint = props.AnchorPoint,
        Size = props.Size,
        LayoutOrder = props.LayoutOrder,

        Text = props.ButtonText,
        TextSize = 28,
        TextColor3 = Color3.new(1, 1, 1),

        [Children] = UICorner { CornerRadius = UDim2.new(0, 8) }
    }
end
```

We can call this function later to generate as many buttons as we need:

```Lua
-- this is just a regular Lua function call!
local helloBtn = Button {
    ButtonText = "Hello",
    Size = UDim2.fromOffset(200, 50)
}

helloBtn.Parent = Players.LocalPlayer.PlayerGui.ScreenGui
```

This is the primary way UI is reused in Fusion, and it's significant enough to
have it's own name. Any function that takes in `props` and returns instances is
called a **component** (because it often represents a reusable *component* of an
interface).

!!! tip
    They're so significant, in fact, that you've already been using components
    without knowing it! 

    ```Lua
    local makeTextLabel = New("TextLabel")

    print(typeof(makeTextLabel)) --> function

    local myLabel = makeTextLabel {
        Text = "Hello, world!"
    }
    ```

    When you call `New` with a class name, it returns a component. Calling the
    component will create a new instance of that class type, using the `props` as
    properties to apply to the instance. 