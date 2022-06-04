TODO

-----

## Returning Children

As we saw in the previous section, components can return instances:

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