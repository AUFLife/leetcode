### 463. Island Perimeter

Difficulty : **Easy**



you are given a map in form of a two-dimensional integer grid where 1 represents land and 0 represents water. Grid cells are connected horizontally/vertically \(not diagonally\). The grid is completely surrounded by water, and there is exactly one island \(i.e., one or more connected land cells\). The island doesn't have "lakes" \(water inside that isn't connected to the water around the island\). One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.

**Example:**

```
[[0,1,0,0],
 [1,1,1,0],
 [0,1,0,0],
 [1,1,0,0]]

Answer: 16
Explanation: The perimeter is the 16 yellow stripes in the image below:
```

![](/assets/import.png)

Python:

```py
    perim = 0
    for i in xrange(len(grid)):
        for j in xrange(len(grid[0])):
            if grid[i][j] == 1:
                perim += 4
                if (i >= 1) and grid[i - 1][j] == 1:
                    perim -= 2
                if (j >= 1) and grid[i][j-1] == 1:
                    perim -= 2
    return perim
```

Scala:

```Scala
/**
 * math tricky
 * 1. loop over the matrix and count the numbers of islands;
 * 2. if the current dot is an island,count if it has any right neighbour or down neighbour
 * 3. the result is islands * 4 - neighbour * 2
 */
 def islandPerimeter(grid: Array[Array[Int]]): Int = {
   var islands = 0
   var neighbours
   for (i <- grid.indices) {
     for (j <- grid(0).indices) {
       if (grid(i)(j) == 1) {
         islands += 1                                                        // count islands 
         if (j < grid(0).length - 1 && grid(i)(j + 1) == 1) neighbours += 1  // count right neighbours
         if (i < grid.length - 1 && grid(i + 1)(j) == 1) neighbours += 1     // count down neighbours
       }
     }
   }
 }
```

Java:

```java
 private static int islandPerimeter(int[][] grid) {
      int border = 0;
      for (int i = 0; i < grid.length; i++) {       // rows
          for (int j = 0; j < grid[i].length; j++) {    // columns
              // if the cell is land
              if (grid[i][j] == 1) {
                  if (i == 0 || grid[i-1][j] == 0) border++; // above water and first row
                  if (i+1 == grid.length || grid[i+1][j] == 0) border++;    // below water and last row
                  if (j == 0 || grid[i][j-1] == 0) border++;   // left water and first column
                  if (j+1 == grid[i].length || grid[i][j+1] == 0) border++; // right water and last column
              }
          }
      }
        return border;
 }
```



