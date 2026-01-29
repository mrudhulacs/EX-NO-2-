## EX. NO:2 IMPLEMENTATION OF PLAYFAIR CIPHER

 

## AIM:
 

 

To write a C program to implement the Playfair Substitution technique.

## DESCRIPTION:

The Playfair cipher starts with creating a key table. The key table is a 5×5 grid of letters that will act as the key for encrypting your plaintext. Each of the 25 letters must be unique and one letter of the alphabet is omitted from the table (as there are 25 spots and 26 letters in the alphabet).

To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. The two letters of the diagram are considered as the opposite corners of a rectangle in the key table. Note the relative position of the corners of this rectangle. Then apply the following 4 rules, in order, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of corners of the rectangle defined by the original pair.
## EXAMPLE:
![image](https://github.com/Hemamanigandan/EX-NO-2-/assets/149653568/e6858d4f-b122-42ba-acdb-db18ec2e9675)

 

## ALGORITHM:

STEP-1: Read the plain text from the user.
STEP-2: Read the keyword from the user.
STEP-3: Arrange the keyword without duplicates in a 5*5 matrix in the row order and fill the remaining cells with missed out letters in alphabetical order. Note that ‘i’ and ‘j’ takes the same cell.
STEP-4: Group the plain text in pairs and match the corresponding corner letters by forming a rectangular grid.
STEP-5: Display the obtained cipher text.




Program:

```
key = input("Key: ").upper().replace(" ", "")
text = input("Text: ").upper().replace(" ", "").replace("J", "I")

matrix = ""
for c in key:
    if c not in matrix and c != 'J':
        matrix += c

for c in "ABCDEFGHIKLMNOPQRSTUVWXYZ":
    if c not in matrix:
        matrix += c

def playfair(msg, mode):
    result = ""
    i = 0
    while i < len(msg):
        a = msg[i]
        b = msg[i+1] if i+1 < len(msg) else 'X'

        r1, c1 = matrix.index(a)//5, matrix.index(a)%5
        r2, c2 = matrix.index(b)//5, matrix.index(b)%5

        if r1 == r2:   
            if mode == "E":
                result += matrix[r1*5 + (c1+1)%5]
                result += matrix[r2*5 + (c2+1)%5]
            else:
                result += matrix[r1*5 + (c1-1)%5]
                result += matrix[r2*5 + (c2-1)%5]

        elif c1 == c2: 
            if mode == "E":
                result += matrix[((r1+1)%5)*5 + c1]
                result += matrix[((r2+1)%5)*5 + c2]
            else:
                result += matrix[((r1-1)%5)*5 + c1]
                result += matrix[((r2-1)%5)*5 + c2]

        else:         
            result += matrix[r1*5 + c2]
            result += matrix[r2*5 + c1]

        i += 2
    return result

encrypted = playfair(text, "E")
print("Encrypted:", encrypted)

decrypted = playfair(encrypted, "D")
print("Decrypted:", decrypted)
```




Output:

<img width="1509" height="757" alt="image" src="https://github.com/user-attachments/assets/8fd8395f-af63-4a02-93eb-bccc37ee663c" />




Result :


Thus the implementation of Playfair Substitution technique had been executed successfully.




