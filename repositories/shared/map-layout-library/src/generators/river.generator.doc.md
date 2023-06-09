# `generateRivers`

The `generateRivers` function is a part of the Map Layout Library. It is responsible for generating river layout
coordinates on a given grid. The generated rivers do not interact with other elements of the layout. The main purpose of
this function is to provide a diverse and reproducible way to generate river layouts.

## Parameters

The `generateRivers` function accepts the following parameters:

1. `rows`: A number representing the number of rows in the grid.
2. `columns`: A number representing the number of columns in the grid.
3. `_layout`: An object representing the current layout of the grid. It contains arrays for different types of elements
   such as roads, rivers, buildings, and parks. This parameter is ignored in the current implementation.
4. `randomGenerator`: An object which has a `next` method that returns a random number between 0 and 1. It is used to
   determine the starting point and the direction of the river.

## Return Value

The `generateRivers` function returns an array of `Coordinate` objects which represent the layout of the river on the
grid. Each `Coordinate` object has `x` and `y` properties that represent the column and row index in the grid,
respectively.

## Behaviour

The function starts generating the river from one of the grid's edges (top, right, bottom, or left) and continues in a
randomly chosen direction until it hits another edge of the grid.

The initial direction and starting point are chosen randomly based on the `randomGenerator.next` method. Once the
direction is set, the river is generated by iterating over the grid and creating a `Coordinate` at each step.

At each step, the function also recalculates the possible directions to continue generating the river. It ensures that
the river stays within the grid boundaries and doesn't loop back on itself.

## Example

```typescript
const mockRandomGenerator = {
  next: jest.fn()
    .mockReturnValueOnce(0.1) // Starting direction (UP)
    .mockReturnValueOnce(0.1) // Starting x coordinate when going DOWN
    .mockReturnValue(0.1) // Keep going DOWN
};

const result = generateRivers(5, 5, { roads: [], rivers: [], buildings: [], parks: [] }, mockRandomGenerator);

console.log(result);
//  [
//    { x: 0, y: 0 },
//    { x: 0, y: 1 },
//    { x: 0, y: 2 },
//    { x: 0, y: 3 },
//    { x: 0, y: 4 }
//  ]
```

In the example above, the `generateRivers` function is called with a 5x5 grid and a `randomGenerator` that makes the
river start from the top and keep going down. The `result` will be an array representing the coordinates of the river.

## Tests

This function is covered by unit tests that check if:

1. All generated rivers are within the grid boundaries.
2. The function generates rivers irrespective of other elements in the layout.
3. The function ends the river at the expected edge of the grid based on the direction and starting point.

## Notes

1. The generation of rivers is deterministic and depends on the `randomGenerator`. For the same seed, the function will
    always generate the same river layout.
2. The generated river layout can vary widely for different seeds provided to the `randomGenerator`.
3. The generated rivers do not have to respect or avoid other existing elements on the layout.
