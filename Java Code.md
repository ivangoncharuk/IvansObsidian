
```java

public class Main{
	public static void main(String[] args) {
		System.out.println("Test");
	}
}
```


```

Plaintext: 0110 0110 0001 0001
Key (K): 1010
initial ctr (IV): 0001

Block 1: initial ctr = 0001
-  $\oplus$ ctr (0001) with Key (1010) = 1011
- S-BOX: 1011  $\rightarrow$ 0011
-  $\oplus$ with Plaintext Block 1 (0110): 0011  $\oplus$ 0110 = 0101

Block 2: Incremented ctr = 0010
-  $\oplus$ ctr (0010) with Key (1010) = 1000
- S-BOX: 1000  $\rightarrow$ 0110
-  $\oplus$ with Plaintext Block 2 (0110): 0110  $\oplus$ 0110 = 0000

Block 3: Incremented ctr = 0011
-  $\oplus$ ctr (0011) with Key (1010) = 1001
- S-BOX: 1001  $\rightarrow$ 0010
-  $\oplus$ with Plaintext Block 3 (0001): 0010  $\oplus$ 0001 = 0011

Block 4: Incremented ctr = 0100
-  $\oplus$ ctr (0100) with Key (1010) = 1110
- S-BOX: 1110  $\rightarrow$ 1111
-  $\oplus$ with Plaintext Block 4 (0001): 1111  $\oplus$ 0001 = 1110

Final Ciphertext: 0101 0000 0011 1110

```