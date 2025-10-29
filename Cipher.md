```java
import java.util.Scanner; 
 
public class ProductCipherColumnarTransposition { 
    public static void main(String[] args) { 
        Scanner scanner = new Scanner(System.in); 
 
        // Fixed key for simplicity (you can modify this for a secret key) 
        String key = "SECRETKEY"; 
         
        System.out.print("Enter the plaintext: "); 
        String plaintext = scanner.nextLine(); 
 
        // Encryption 
        String ciphertext = encrypt(plaintext, key); 
        System.out.println("Encrypted ciphertext: " + ciphertext); 
 
        // Decryption 
        String decryptedText = decrypt(ciphertext, key); 
        System.out.println("Decrypted plaintext: " + decryptedText); 
 
        scanner.close(); 
    } 
 
    // Encryption using Columnar Transposition Cipher 
    public static String encrypt(String plaintext, String key) { 
        int keyLength = key.length(); 
        int plainTextLength = plaintext.length(); 
        int rowCount = (int) Math.ceil((double) plainTextLength / keyLength); 
 
        char[][] grid = new char[rowCount][keyLength]; 
 
        int charIndex = 0; 
        for (int row = 0; row < rowCount; row++) { 
            for (int col = 0; col < keyLength; col++) { 
                if (charIndex < plainTextLength) { 
                    grid[row][col] = plaintext.charAt(charIndex); 
                    charIndex++; 
                } else { 
                    grid[row][col] = 'X'; // Fill empty cells with 'X' 
                } 
            } 
        } 
 
        StringBuilder encryptedText = new StringBuilder(); 
        for (char c : key.toCharArray()) { 
            int colIndex = key.indexOf(c); 
            for (int row = 0; row < rowCount; row++) { 
                encryptedText.append(grid[row][colIndex]); 
            } 
        } 
 
        return encryptedText.toString(); 
    } 
 
    // Decryption using Columnar Transposition Cipher 
    public static String decrypt(String ciphertext, String key) { 
        int keyLength = key.length(); 
        int cipherTextLength = ciphertext.length(); 
        int rowCount = cipherTextLength / keyLength; 
 
        char[][] grid = new char[rowCount][keyLength]; 
 
        int charIndex = 0; 
        for (char c : key.toCharArray()) { 
            int colIndex = key.indexOf(c); 
            for (int row = 0; row < rowCount; row++) { 
                grid[row][colIndex] = ciphertext.charAt(charIndex); 
                charIndex++; 
            } 
        } 
 
        StringBuilder decryptedText = new StringBuilder(); 
        for (int row = 0; row < rowCount; row++) { 
            for (int col = 0; col < keyLength; col++) { 
                if (grid[row][col] != 'X') { 
                    decryptedText.append(grid[row][col]); 
                } 
            } 
        } 
 
        return decryptedText.toString(); 
    } 
} 

```
