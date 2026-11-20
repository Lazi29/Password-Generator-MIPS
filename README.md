# Password-Generator-MIPS
Create a simple password generator

.data

    prompt: .asciiz "Welcome to your Password Generator"
    promt:  .ascizz "\nWrite your password"
    result: .asciiz "\nGenerated password: "
    input:  .space 256

.text
.globl main

main:

    # Ask the user for a string
    li $v0, 4
    la $a0, prompt
    syscall

    # Read the complete string
    li $v0, 8
    la $a0, input
    li $a1, 256
    syscall

    # Start processing the string
    la $t0, input

loop:

    # Load the current character
    lb $t1, 0($t0)

    # Stop at the end of the string
    beq $t1, $zero, done

    # Stop at the newline character
    li $t2, 10
    beq $t1, $t2, done

    # Check for lowercase 'a'
    li $t2, 'a'
    beq $t1, $t2, replace_a

    # Check for lowercase 'e'
    li $t2, 'e'
    beq $t1, $t2, replace_e

    # Check for lowercase 'i'
    li $t2, 'i'
    beq $t1, $t2, replace_i

    # Check for lowercase 'o'
    li $t2, 'o'
    beq $t1, $t2, replace_o

    # Check for lowercase 's'
    li $t2, 's'
    beq $t1, $t2, replace_s

    # Keep all other characters unchanged
    j next_character

replace_a:
    li $t1, '@'
    j store_character

replace_e:
    li $t1, '3'
    j store_character

replace_i:
    li $t1, '!'
    j store_character

replace_o:
    li $t1, '0'
    j store_character

replace_s:
    li $t1, '$'
    j store_character

store_character:

    # Save the converted character
    sb $t1, 0($t0)

next_character:

    # Move to the next character
    addi $t0, $t0, 1
    j loop

done:

    # Display the result message
    li $v0, 4
    la $a0, result
    syscall

    # Display the converted string
    li $v0, 4
    la $a0, input
    syscall

    # Exit the program
    li $v0, 10
    syscall
