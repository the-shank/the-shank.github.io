---
layout: default
title: "Eight Queens problem in Go"
date: 2016-05-24
tags:
  - go
  - algo-ds 
---

# Solution to Eight Queens problem in Go

We shall use the **recursive backtracking** technique for getting all the solutions to the **Eight Queens** Problem.

We shall use two 8x8 arrays, one to store the position of the queens and the other to store the counts of the queens that are attacking a particular position.

```go 
var hasQueen [8][8]bool
var inAttack [8][8]int
```

Next is the helper function that we call to place a queen at a position `(i, j)`.
```go
func placeQueen(i, j int) {
	hasQueen[i][j] = true
	// update attack counts
	// row
	for c := 0; c < 8; c++ {
		inAttack[i][c]++
	}
	// col
	for r := 0; r < 8; r++ {
		inAttack[r][j]++
	}
	inAttack[i][j] -= 2  // the (i,j) cell has been counted twice in the above iterations
	// diagonals
	for r := 0; r < 8; r++ {
		for c := 0; c < 8; c++ {
			if r == i && c == j {
				inAttack[r][c]++
				continue
			}
			if r-i == c-j || r-i == -(c-j) {
				inAttack[r][c]++
			}
		}
	}
}
```
Next, we write the function to remove a queen form a position `(i, j)`. This shall be used when we are *backtracking* due to some reason and need to remove a queen.
```go
func removeQueen(i, j int) {
	hasQueen[i][j] = false
	// update attack counts
	// row
	for c := 0; c < 8; c++ {
		inAttack[i][c]--
	}
	// col
	for r := 0; r < 8; r++ {
		inAttack[r][j]--
	}
	inAttack[i][j] += 2
	// diagonals
	for r := 0; r < 8; r++ {
		for c := 0; c < 8; c++ {
			if r == i && c == j {
				inAttack[r][c]--
				continue
			}
			if r-i == c-j || r-i == -(c-j) {
				inAttack[r][c]--
			}
		}
	}
}
```
This function is just the inverse of the `place_queen()` function.

Next we use a global variable to hold he counts of the solutions discovered.
```go
var solNo int
```

Next is the actual function that does the recursive backtracking to solve the problem.
```go
func solve(r int) {
	if r == 7 {
		// can we place the queen somewhere
		for c, cnt := range inAttack[7] {
			if cnt == 0 {
				placeQueen(r, c)
				solNo++
				fmt.Println("Solution No.", solNo)
				pp2DBoolArr(hasQueen)
				removeQueen(r, c)
			}
		}

	} else {
		for c, cnt := range inAttack[r] {
			if cnt == 0 {
				placeQueen(r, c)
				solve(r + 1)  // solve the next row (recursive)
				removeQueen(r, c)  // remove this queen (backtrack)
			}
		}
	}
}
```
I also use a simple utility function to print the positions of the queens.
```go
// `pp2DBoolArr` pretty prints a 2D int array
func pp2DBoolArr(data [8][8]bool) {
	for i := 0; i < 8; i++ {
		row := make([]string, 8)
		for j := 0; j < 8; j++ {
			if data[i][j] {
				row[j] = "Q"
			} else {
				row[j] = "+"
			}
		}
		fmt.Println(strings.Join(row, " "))
	}
}
```
And the `main` function that is the entry point of the code.
```go
func main() {
	solve(0)
}
```
The **complete code** is available [here](https://gitlab.com/shank-algo/utils-go/blob/6953ea191d3319373b4b7fb6f75816b36ea393b5/ref/eight_queens_all.go). The **generated output** is available [here](https://gitlab.com/shank-algo/utils-go/blob/6953ea191d3319373b4b7fb6f75816b36ea393b5/ref/eight_queens_all.out).