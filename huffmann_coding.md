# Huffman Coding

## Theory
- This is also known as **Optimal Prefix Notation** (Needs to be verified)
- It is a data encoding technique.
- It is a data encryption mechanism.
- It is a lossless data compression technique.

## Example 1
We have a file of 105 characters where frequency of each distinct character is as below.

|      |      |      |     |     |     |
| ---- | ---- | ---- | --- | --- | --- |
|  A   |  B   |  C   |  D  |  E  |  F  |
| $35$ | $12$ | $45$ | $3$ | $2$ | $8$ |

We have to figure out a way by which we can encrypt this with minimum number of 0's and 1's.


### Encoding Approach 1 (ASCII Encoding)
- As per ASCII encoding, each character can be encoded with 8 digits.
- So we can encrypt the file of 105 characters by $105 * 8 = 840$ bits.

### Encoding Approach 2
- The idea here is, we know we have 6 distinct character.
- To represent 6 characters, 3 bits are sufficient. Something as below.

    |   |       |
    | - | ----- |
    | A | $000$ |
    | B | $001$ |
    | C | $010$ |
    | D | $011$ |
    | E | $100$ |
    | F | $101$ |

- So we can encrypt the file of 105 characters by $105 * 3 = 315$ bits. This is better than the previous approach. But we can still improve.

### Encoding Approach 3
- In the above 2 approach, we are encoding every character with equal number of bits.
- If we consider approach 2, we can see 276 $(i.e. 87\%)$ bits are used only for 3 characters (A, B and C).
- This is happening because we are doing uniform encoding.
- So we can improve this, if we assign less bits to more frequent characters and more bits to less frequent characters, and by that we can have overall bits improved.
- Huffman coding takes the advantage of non-uniform coding and hence be able to reduce the number of bits required to compress the file.

#### Huffman Encoding Technique

- **STEP 1 :** Build the huffman tree.

    - **Create node for every distinct character**

        ```mermaid
        graph
            A((A = 35))
            B((B = 12))
            C((C = 45))
            D((D = 3))
            E((E = 2))
            F((F = 8))
        ```
    - **Merge 2 minimum D and E**

        ```mermaid
        graph
            A((A = 35))
            B((B = 12))
            C((C = 45))
            DE(DE = 5) --> E((E = 2))
            DE(DE = 5) --> D((D = 3))
            F((F = 8))
        ```

    - **Merge 2 minimum DE and F**

        ```mermaid
        graph
            A((A = 35))
            B((B = 12))
            C((C = 45))
            DEF(DEF = 13) --> DE(DE = 5)
            DEF(DEF = 13) --> F((F = 8))
            DE(DE = 5) --> E((E = 2))
            DE(DE = 5) --> D((D = 3))
        ```

    - **Merge 2 minimum DEF and B**

        ```mermaid
        graph
            A((A = 35))
            BDEF(BDEF=25) --> B((B = 12))
            BDEF(BDEF=25) --> DEF(DEF = 13)
            C((C = 45))
            DEF(DEF = 13) --> DE(DE = 5)
            DEF(DEF = 13) --> F((F = 8))
            DE(DE = 5) --> E((E = 2))
            DE(DE = 5) --> D((D = 3))
        ```

    - **Merge 2 minimum BDEF and A**

        ```mermaid
        graph
            ABDEF(ABDEF = 60) --> BDEF(BDEF=25)
            ABDEF(ABDEF = 60) --> A((A = 35))
            BDEF(BDEF=25) --> B((B = 12))
            BDEF(BDEF=25) --> DEF(DEF = 13)
            C((C = 45))
            DEF(DEF = 13) --> DE(DE = 5)
            DEF(DEF = 13) --> F((F = 8))
            DE(DE = 5) --> E((E = 2))
            DE(DE = 5) --> D((D = 3))
        ```

    - **Merge 2 minimum ABDEF and C**

        ```mermaid
        graph
            ABCDEF(ABCDEF = 105) --> C((C = 45))
            ABCDEF(ABCDEF = 105) --> ABDEF(ABDEF = 60)
            ABDEF(ABDEF = 60) --> BDEF(BDEF=25)
            ABDEF(ABDEF = 60) --> A((A = 35))
            BDEF(BDEF=25) --> B((B = 12))
            BDEF(BDEF=25) --> DEF(DEF = 13)
            DEF(DEF = 13) --> DE(DE = 5)
            DEF(DEF = 13) --> F((F = 8))
            DE(DE = 5) --> E((E = 2))
            DE(DE = 5) --> D((D = 3))
        ```

- **STEP 2 :** Assign the code

    ```mermaid
    graph
        ABCDEF(ABCDEF = 105) --0--> C((C = 45))
        ABCDEF(ABCDEF = 105) --1--> ABDEF(ABDEF = 60)
        ABDEF(ABDEF = 60) --0--> BDEF(BDEF=25)
        ABDEF(ABDEF = 60) --1--> A((A = 35))
        BDEF(BDEF=25) --0--> B((B = 12))
        BDEF(BDEF=25) --1--> DEF(DEF = 13)
        DEF(DEF = 13) --0--> DE(DE = 5)
        DEF(DEF = 13) --1--> F((F = 8))
        DE(DE = 5) --0--> E((E = 2))
        DE(DE = 5) --1--> D((D = 3))
    ```

- **STEP 3 :** The Huffman Code for each character is as below

    |   |         |
    | - | ------- |
    | A | $11$    |
    | B | $100$   |
    | C | $0$     |
    | D | $10101$ |
    | E | $10100$ |
    | F | $1011$  |

- If we compress the file with the Huffman code, then number of bits required is $(2*35) + (3*12) + (1*45) + (3*5) + (2*5) + (8*4) = 208$

- Average bits per character would be $\frac{208}{105} = 1.98$

## Example 2


## Ambiguity Issue


## Implementation

## Analysis

### Time Complexity

### Space Complexity

## Note
- Huffman code, produces 2 Way Encoded Tree.
- Here, it is not necessary that the left nodes in the huffman tree will be encoded with 0 and right will be encoded by 1. If nothing is given, then try out with both and see which one match the option.
- But it is important that whatever convention you follow, follow the same through out all the nodes in the tree.
- The only difference between the [Optimal Merge Pattern]() and the Huffman Coding is, in Huffman Coding, we need the encoding in the tree(0 and 1).
- While Decoding a string, Use the Tree. Do not go with the Codes for each character.