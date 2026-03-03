*This project has been created as part of the 42 curriculum by brouane.*

# push_swap

## Description

**push_swap** is an algorithmic project from the 42 curriculum. The goal is to sort a list of integers using **two stacks** and a **restricted instruction set**, while minimizing the total number of operations.

Only specific stack operations are allowed, forcing the implementation of **optimized sorting strategies**, **careful memory management**, and **efficient algorithmic design**.

This project strengthens understanding of:
- Sorting algorithms
- Stack-based computation
- Algorithmic optimization
- Linked list manipulation
- Memory management
- Error handling

---

## Instructions

### Compilation

make

This produces the executable:

./push_swap

Clean object files:

make clean

Full cleanup:

make fclean

Recompile:

make re

---

### Execution

./push_swap 4 67 3 87 23

Or:

./push_swap "4 67 3 87 23"

Or:

./push_swap "4 67 3 87 23" -95 -651

The program outputs the sequence of operations required to sort the stack.

---

### Bonus — Checker

Compile the checker:

make bonus

This produces the checker executable:

./checker 3 2 1

The checker reads operations from stdin and outputs OK if the stack is correctly sorted, or KO otherwise. It prints Error for any invalid instructions.

---

## Usage Example

$ ./push_swap 3 2 1
sa
rra

---

## Algorithm Overview

The algorithm dynamically selects a sorting strategy based on input size in order to minimize the total number of operations.

* **2 elements:**  
  A single rotation is applied if the elements are not already sorted.

* **3 elements:**  
  A direct case-based sorting algorithm is used, covering all possible permutations with the minimal number of operations.

* **4–5 elements:**  
  The smallest indexed elements are progressively pushed to stack **B**, the remaining three elements in stack **A** are sorted using the optimized three-element algorithm, and finally the stored elements are reinserted into stack **A** in their correct positions.

* **More than 5 elements:**  
  A chunk-based strategy is applied. Elements are distributed into stack **B** in indexed ranges (chunks), reducing disorder progressively. Then, elements are pushed back into stack **A** in descending index order using optimized rotations, ensuring minimal instruction count.

---

## File & Function Documentation

---

### `error_checker.c`

Handles **input validation and error detection**.

* `ft_isdigit(char d)`
  Checks whether a character is a digit.

* `ft_issign(char s)`
  Checks if a character is a sign (`+` or `-`).

* `dig_sign_checker(char *str)`
  Verifies correct numeric format and valid sign placement.

* `dup_errors(int count, long *original_numbers)`
  Detects duplicate numbers.

* `check_for_errors(char ***array, long **original_numbers, int count)`
  Global input validation: checks formatting, conversion errors, and duplicates.

---

### `extended_functions.c`

Utility functions extending core logic.

* `assign_to_stack(...)`
  Builds stack A by assigning each value its sorted index.

* `initialize_data(...)`
  Handles argument parsing, allocation, and validation. Shared by both push_swap and checker.

---

### `external_functions.c`

General helper functions.

* `ft_count_words(...)`
  Counts words separated by a delimiter.

* `find_index(...)`
  Finds the index of a value in the sorted array.

* `ft_strlen(...)`
  Computes string length.

---

### `freedom.c`

Handles **memory management and cleanup**.

* `free_array(...)`
  Frees a 2D character array.

* `free_pointers(...)`
  Frees all allocated arrays.

* `free_stack(...)`
  Frees a stack.

* `free_all_stacks(...)`
  Frees both stacks.

---

### `ft_atoi.c`

* `ft_atoi(...)`
  Converts string to integer with overflow protection.

---

### `ft_lstadd_back.c`

Stack construction utilities.

* `ft_lstnew(...)`
  Creates a new stack node.

* `ft_lstadd_back(...)`
  Appends a node to the stack.

---

### `ft_print.c`

* `ft_print(char *str)`
  Outputs operations to stdout.

---

### `internal_functions.c`

Core input and preprocessing logic.

* `count_all_nums(...)`
  Counts total numbers from input.

* `array_manager(...)`
  Builds argument array.

* `numbers_manager(...)`
  Allocates numeric arrays.

* `numbers_copy(...)`
  Copies original → sorted array.

* `sort_numbers(...)`
  Sorts numeric array and detects sorted input.

---

### `operations_manager.c`

Controls **sorting strategy selection**.

* `two_sorter(...)`
  Sorts 2 elements.

* `five_sorter(...)`
  Sorts up to 5 elements.

* `chunk_sorter(...)`
  Handles large input using chunk-based logic.

* `operations_manager(...)`
  Chooses best strategy based on input size.

---

### `push_back_to_a.c`

Handles **reinsertion from stack B → A**.

* `which_position(...)`
  Locates a target index in stack.

* `push_using_rb(...)`
  Push using forward rotation.

* `push_using_rrb(...)`
  Push using reverse rotation.

* `push_back_to_a(...)`
  Main reinsertion algorithm.

---

### `push.c`

Stack push operations.

* `push(...)`
  Core push operation.

* `pb(...)`
  Push from A → B.

* `pa(...)`
  Push from B → A.

---

### `push_from_a.c`

Handles **initial distribution from A → B**.

* `which_position_in_a(...)`
  Locates element position in stack A.

* `push_using_ra(...)`
  Forward rotation push.

* `push_using_rra(...)`
  Reverse rotation push.

* `push_from_a(...)`
  Main extraction algorithm.

---

### `push_to_b.c`

Chunk-based sorting logic.

* `set_max_range(...)`
  Determines chunk size.

* `push_to_b(...)`
  Pushes elements into B using chunk strategy.

---

### `rotate.c`

Rotation operations.

* `rotate(...)`
  Core rotate logic.

* `ra(...)`
  Rotate A.

* `rb(...)`
  Rotate B.

* `rr(...)`
  Simultaneously rotates both A and B.

---

### `reverse_rotate.c`

Reverse rotation operations.

* `reverse_rotate(...)`
  Core reverse rotation logic.

* `rra(...)`
  Reverse rotate A.

* `rrb(...)`
  Reverse rotate B.

* `rrr(...)`
  Simultaneously reverse rotates both A and B.

---

### `swap.c`

Swap operations.

* `swap(...)`
  Core swap logic.

* `sa(...)`
  Swap A.

* `sb(...)`
  Swap B.

* `ss(...)`
  Simultaneously swaps both A and B.

---

### `split_them.c`

Argument splitting.

* `ft_putword(...)`
  Copies extracted word.

* `ft_split_words(...)`
  Splits string into words.

* `split_them(...)`
  Main argument splitter.

---

### `three_sorter.c`

Optimized sorting for **exactly 3 elements**.

* `three_sorter_cases(...)`
  Contains all sorting permutations.

* `three_sorter(...)`
  Applies correct sorting case.

---

### `push_swap.c`

Main program control.

* `initialize_data(...)`
  Handles argument parsing, allocation, and validation.

* `push_swap(...)`
  Main sorting pipeline.

* `main(...)`
  Program entry point.

---

## Bonus — Checker Files

---

### `checker.c`

Bonus checker main program.

* `is_sorted_stack(...)`
  Checks whether stack A is fully sorted by index.

* `exec_instruction(...)`
  Reads a single instruction string and executes the matching stack operation.

* `read_and_execute(...)`
  Reads all instructions from stdin line by line using get_next_line and executes each one.

* `checker(...)`
  Main checker pipeline: initializes data, reads and executes instructions, then outputs OK or KO.

* `main(...)`
  Checker program entry point.

---

### `checker_utils.c`

Utility functions for the checker.

* `ft_strcmp(...)`
  Compares two strings. Used to match instruction names read from stdin.

---

### `get_next_line.c`

Reads input line by line from a file descriptor.

* `next_line(...)`
  Extracts the next line from the working buffer.

* `read_line(...)`
  Reads from the file descriptor into the working buffer until a newline is found.

* `new_line(...)`
  Trims the already-extracted line from the working buffer.

* `get_next_line(...)`
  Main function: returns the next line from the given file descriptor.

---

### `get_next_line_utils.c`

Helper functions for get_next_line.

* `ft_strchr(...)`
  Checks whether the working buffer contains a newline character.

* `ft_strjoin_copy(...)`
  Copies two strings into a pre-allocated joined buffer.

* `ft_strjoin(...)`
  Concatenates two strings into a newly allocated string.

---

## Resources

### Documentation & References

* 42 Cursus Guide - push_swap
  [https://42-cursus.gitbook.io/guide/2-rank-02/push_swap](https://42-cursus.gitbook.io/guide/2-rank-02/push_swap)

* push_swap Visualizer
  [https://push-swap42-visualizer.vercel.app/](https://push-swap42-visualizer.vercel.app/)

* push_swap Tutorial (Video)
  [https://www.youtube.com/watch?v=OaG81sDEpVk](https://www.youtube.com/watch?v=OaG81sDEpVk)

* Linked Lists Explained (Video)
  [https://www.youtube.com/watch?v=uBZHMkpsTfg](https://www.youtube.com/watch?v=uBZHMkpsTfg)

---

### AI Usage Disclosure

AI tools were used for:

* Debugging memory errors and segmentation faults
* Algorithmic optimization brainstorming
* Documentation structuring and clarity improvements

All algorithm design, logic implementation, and debugging decisions were fully understood and verified by the author.