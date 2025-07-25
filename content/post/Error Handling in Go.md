---
# Common-Defined
title: "Error Handling in Go"
date: 2025-07-14T00:00:00+07:00
lastmod: 2025-07-14T00:00:00+07:00
draft: false
tags: ["go"]
categories: ["Programming", "index"]
author: "Duken Marga"

# User-Defined
# You can close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: true
toc: true
# You can also define another contentCopyright
contentCopyright: '<a rel="license noopener" href="https://creativecommons.org/licenses/by-nc-nd/4.0/" target="_blank">CC BY-NC-ND 4.0</a>'
reward: false
mathjax: true
---

### Error As Value

Error is treated as value in Go. No `try/catch`, but there is `panic/recover`.
Other programming languages is using `try/catch` for regular error,
while Go use `panic/recover` for fatal or unrecoverable condition such 
as nil pointer dereference and so on.
Hence, `panic/recover` is not a direct replacement for `try/catch`.

For regular error, we need to return it like we return a variable.
Some people are alright with this decision, but some are not because
it makes the code verbose and you will find `if err != nil` are everywhere.

This article will summarise several ways of how we can handle error
in Go and what are the options that we can use to make the error
usable and traceable.


### Basic Method is Just Return

Here is an example of basic error. You just return it as value and
check it just after calling the function.
The idiomatic way is to check it outside the function, not inside the
function itself.

```go
import ...

func main() {
	// Check the error just after calling the function
	file, err := openFile("my_log.txt")
	if err != nil {
		fmt.Println(err)
		return
	}
	defer file.Close()
}

func openFile(filename string) (*os.File, error) {
	// Open the file for reading
	file, err := os.Open(filename)
	if err != nil {
		// return the error like a value
		return nil, err
	}

	return file, nil
}
```

### Wrap and Return

Rather than just return the plain error, we can wrap it.
This can be pretty useful especially when we have several level of functions.
Wrapping error means adding more context or information to the error
that we want to return. This way the caller can extract (unwrap) and
can locate the source and cause of the error.

To wrap an error, use `fmt.Errof` and verb `%w`. This will preserve
the original error. Usually we are adding the operation when wrapping the
original error such as `open CSV`. My other best practice is to add more
context like filename when we are sure that the original error comes from
third party or standard library that usually will not include such details.
Even if the external package includes them (details), it's still a good practice,
since we can't control what the external package will return to our function.
As additional tips, we add colon (`:`) to separate context.

```go
import ...

func main() {
	records, err := readCSV("my_file.csv")
	if err != nil {
		fmt.Printf("read CSV: %v", err)
		return
	}
	_ = records
	// continue..
}

func readCSV(filename string) ([][]string, error) {
	// Open CSV file
	file, err := openCSV(filename)
	if err != nil {
		// wrap error
		return [][]string{}, fmt.Errorf("open CSV: %w", err)
	}
	defer file.Close()

	// Read file
	reader := csv.NewReader(file)
	records, err := reader.ReadAll()
	if err != nil {
		// wrap error
		return [][]string{}, fmt.Errorf("parse CSV %v: %w", filename, err)
	}

	return records, nil
}

func openCSV(filename string) (*os.File, error) {
	// Check the CSV extension (has .csv)
	if len(filename) < 4 || filename[len(filename)-3:] != "csv" {
		return nil, fmt.Errorf("not a CSV file: %v", filename)
	}
	// Open the file for reading
	file, err := os.Open(filename)
	if err != nil {
		// wrap error, add some context
		return nil, fmt.Errorf("open file %v: %w", filename, err)
	}

	return file, nil
}

// Example error
- read CSV: open CSV: open file my_file.csv: open my_file.csv: no such file or directory
- read CSV: open CSV: not a CSV file: my_file.pdf
```

### New, Unwrap, and Compare Error

Another way to create an error sentence is by using `errors.New()` and save it into a variable. Later, we can check or assert the error compared with the
variable. The downside is `errors.New()` can only be used to create a
sentence without being able to wrap other error. That's why in my opinion
it is suitable to be used for the root cause of error (the first time it introduce
error).
Otherwise, I still recommend `fmt.Errorf` most of the time, since we usually
work with 3rd party.

The order of function call from example below is
`main() -> readCSV() -> openCSV()`. We will introduce the error by mistyping
the filename (wrong format).
Function `openCSV` return `errNotCSV`
which is the root of the error. Notice that there are 2 ways to return the error,
dependes on how we will handle it later: wrapping or no wrapping.

There are at least 2 ways to check error:
- First method: Using `errors.Unwrap` will unwrap (extract) an error from the underlying errors in a wrapped error chain.
  - At `main` level after calling `readCSV`, `err` is now contains `open CSV: not a CSV file`
  - If we call `Unwrap` to `err`, we will get `not a CSV file`.
The unwrap can be compared directly to the error variable, for example
`errors.Unwrap(err) == errNotCSV`.
  - If we unwrap it again, we will get `nil`.
  - But, remember that to call multiple-unwrap, we need to assign the error again, for example `err = errors.Unwrap(err)`. This example below doesn't
  have such error assignment, since we don't want to check one by one.
- Second method: Using `errors.Is` is the recommended method to check if a specific
error is contained within the chain. It will check if a specific error value is on
the error tree, no need to unwrap multiple times.


```go
import (
	"errors"
	...
)

var (
	errNotCSV = errors.New("not a CSV file")
)

func main() {
	records, err := readCSV("my_file.cs1v") // error in file naming

	// 1st method is by using Unwrap
	if errors.Unwrap(err) == errNotCSV {
		...
	}

	// 2nd method is by using Is
	if errors.Is(err, errNotCSV) {
		fmt.Printf("error: %v", err)
		return
	} else if err != nil {
		fmt.Printf("read CSV: %v", err)
		return
	}

	_ = records
	// continue..
}

func readCSV(filename string) ([][]string, error) {
	// Open CSV file
	file, err := openCSV(filename)
	if err != nil {
		// wrap error
		return [][]string{}, fmt.Errorf("open CSV: %w", err)
	}
	defer file.Close()

	// Read file
	reader := csv.NewReader(file)
	records, err := reader.ReadAll()
	if err != nil {
		// wrap error
		return [][]string{}, fmt.Errorf("parse CSV %v: %w", filename, err)
	}

	return records, nil
}

func openCSV(filename string) (*os.File, error) {
	// Check the CSV extension (has .csv)
	if len(filename) < 4 || filename[len(filename)-3:] != "csv" {
		// 1st method (direct value comparison) can only be used
		// if we return the err directly
		return nil, errNotCSV

		// 2nd method (by using errors.Is), we cran wrap it using %w 
		// and add some context
		return nil, fmt.Errorf("%w: %v", errNotCSV, filename)
	}
	// Open the file for reading
	file, err := os.Open(filename)
	if err != nil {
		// wrap error, add some context
		return nil, fmt.Errorf("open file %v: %w", filename, err)
	}

	return file, nil
}
```

### Include Error Stack

All the methods above doesn't include error stack. It's just returning the
error as string (technically as interface).
But, that's the core idea right? Error as value.

But, if you want to include the error stack, you can you errors package from
`github.com/pkg/errors`. Let's modify the above example and instead of using
`fmt.Errorf`, we use `errors.Wrap`. Don't forget to print the error as `%+v`.
Basically, this will print the error including the function name, filename,
line numbers, and it's stack.

Notice that if you are the first one who introduce error (such as the filename
doesn't have valid CSV extension), you still use `fmt.Errorf` since this is
the first item on the stack.

```go
import (
	//...
	"github.com/pkg/errors"
)

func main() {
	records, err := readCSV("my_file.csv")
	if err != nil {
		fmt.Printf("read CSV: %+v", err)
		return
	}
	_ = records
	// continue..
}

func readCSV(filename string) ([][]string, error) {
	// Open CSV file
	file, err := openCSV(filename)
	if err != nil {
		// wrap error
		return [][]string{}, errors.Wrap(err, "open CSV")
	}
	defer file.Close()

	// Read file
	reader := csv.NewReader(file)
	records, err := reader.ReadAll()
	if err != nil {
		// wrap error
		return [][]string{}, errors.Wrap(err, "parse CSV")
	}

	return records, nil
}

func openCSV(filename string) (*os.File, error) {
	// Check the CSV extension (has .csv)
	if len(filename) < 4 || filename[len(filename)-3:] != "csv" {
		return nil, fmt.Errorf("not a CSV file: %v", filename)
	}
	// Open the file for reading
	file, err := os.Open(filename)
	if err != nil {
		// wrap error, add some context
		return nil, errors.Wrap(err, "open file")
	}

	return file, nil
}

// Example error
read CSV: open my_file.csv: no such file or directory
open file
main.openCSV
	/tmp/sandbox1048947168/prog.go:52
main.readCSV
	/tmp/sandbox1048947168/prog.go:25
main.main
	/tmp/sandbox1048947168/prog.go:14
runtime.main
	/usr/local/go-faketime/src/runtime/proc.go:283
runtime.goexit
	/usr/local/go-faketime/src/runtime/asm_amd64.s:1700
open CSV
main.readCSV
	/tmp/sandbox1048947168/prog.go:28
main.main
	/tmp/sandbox1048947168/prog.go:14
runtime.main
	/usr/local/go-faketime/src/runtime/proc.go:283
runtime.goexit
	/usr/local/go-faketime/src/runtime/asm_amd64.s:1700
```

### Summary

In my experience, you don't need the whole stack to debug an issue.
Most of the time, print or use logger to show the error that has been wrapped
is sufficient enough for production use.

My best practice usually:
- Wrap the error by using `fmt.Errorf`
- Check `if err != nil`: if true then handle it by wrapping it again and return;
or make an action for example quit the program if it is on the `main` level.
- I rarely use `errors.New` or save errors into variables since I consider my program
is not that big, but you can consider to create error variables if you want
to track and check everything precisely.