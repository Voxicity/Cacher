# Cacher
Cacher is a simple, easy to use, caching library for any instance.

## Installation
You can either download from the releases tab or get it from the [Creator Store](https://create.roblox.com/store/asset/103695025817225/Cacher). No wally sorry!

## API
### Types
```luau
type reference = {
	item: Instance,
	starterAmount: number?,
	replenishAmount: number?,
	onBorrow: ((item: Instance) -> ())?,
	onReturn: ((item: Instance) -> ())?,
	onCreate: ((item: Instance) -> ())?
}
```

### Creation
Create a cacher object
```luau
local Cacher = require(ReplicatedStorage.Cacher)
local cacher = Cacher.New()
```

#### ```CreateStarterBatch(references: {[string]: reference}): ()```
Creates a starter batch
```lua
cacher:CreateStarterBatch({
  --Cache 1
	Part = {
		item = script.Part,
		starterAmount = 10,
		replenishAmount = 5,
		onBorrow = function(item: Part)
			print("Borrowing!")
		end,
	},

  --Cache 2
	Sound = {
		item = script.Sound,
		onReturn = function(item: Sound)
			print("Returning!")
		end,
	}
})
```

#### ```Borrow(name: string): Instance```
Borrows an item from the cache
```luau
local part = cacher:Borrow("Part")
```
> [!WARNING]
> Items that get borrowed from the cache will no longer be controlled by the cacher. When a cacher is destroyed, any parts that are borrowed will not be destroyed.

#### ```Return(name: string, instance: Instance, delayReturn: number?): ()```
Returns the instance back to the cacher with an optional delay
```luau
cacher:Return("Part", part, 1)
```

#### ```ReduceCache(name: string, reduceTo: number): ()```
Reduces a cache's size to a desired amount
```luau
cacher:ReduceCache("Part", 5)
```

#### ```DeleteCache(name: string): ()```
Deletes a cache
```luau
cacher:DeleteCache("Part")
```

#### ```GetCacheSize(name: string): number```
Gets the size of a cache
```luau
cacher:GetCacheSize("Part")
```

#### ```CleanUp(): ()```
Deletes the cacher object and clean ups destroys caches
```luau
cacher:CleanUp()
```
