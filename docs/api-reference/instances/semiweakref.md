<nav class="fusiondoc-api-breadcrumbs">
	<a href="../..">Fusion</a>
	<a href="..">Instances</a>
</nav>

<h1 class="fusiondoc-api-header" markdown>
	<span class="fusiondoc-api-icon" markdown>:octicons-checklist-24:</span>
	<span class="fusiondoc-api-name">SemiWeakRef</span>
	<span class="fusiondoc-api-pills">
		<span class="fusiondoc-api-pill-type">type</span>
		<span class="fusiondoc-api-pill-since">since v0.2</span>
	</span>
</h1>

A reference to an instance, which is strong only while the instance can be
accessed via the data model, and is weak at all other times. This is useful to
make weak references to instances stable.

```Lua
{
    type: "SemiWeakRef",
    instance: Instance?
}
```

-----

## Fields

- `type` - identifies this table as a semi-weak reference
- `instance` - the reference to the instance; this may disappear at any time

-----

## Example Usage

```Lua
local ref = semiWeakRef(workspace.Part)
workspace.Part.Parent = nil

while ref.instance ~= nil do
    task.wait(1)
end

print("Part has been garbage collected")
```

-----

## Garbage Collection

The reason why semi-weak references are needed is because the default garbage
collection behaviour of instances is not useful. Instance references in Lua do
not share the same lifetime as the instances they represent, meaning the
instance reference can be cleaned up separately from the instance being
destroyed.

By ensuring a strong reference is held to the instance while it is in the data
model, `SemiWeakRef` makes sure the instance reference is not cleaned up until
the instance is in a place where the only way to reference it is by going
through an existing Lua reference, and not via the data model. At this point,
it is sensible to keep a weak reference, so if there are no other strong
references, the instance and it's reference may be garbage collected.