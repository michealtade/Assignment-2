# Assignment-2
Cesearcipher
package micheal;

import java.util.Scanner;

public class CaesarCipher{
    public static void main(String[] args) {

        Scanner input = new Scanner(System.in);
        String plainText;
        int shiftKey;

        System.out.println("Please enter message to be encrypted: ");
        plainText = input.nextLine();

        System.out.println("Please enter shift key ");
        shiftKey = input.nextInt();
        String encryptedText = EncryptText(plainText,shiftKey);

        System.out.println("The Encrypted Text: "+ encryptedText);

        System.out.println("The Decrypted Text: "+ DecryptText(encryptedText,shiftKey));
    }

    public static String EncryptText(String message, int shiftKey) {
        //c(x) =  x + shiftKey Mod(%) 26;
        final String ALPAHABETS = "abcdefghijklmnopqrstuvwxyz";
        message = message.toLowerCase();

        StringBuilder cyperText = new StringBuilder();

        for(int counter = 0;counter < message.length();counter++) {
            if(!Character.isLetter(message.charAt(counter))) {
                cyperText.append(message.charAt(counter));
            }
            else {
                int charPosition = ALPAHABETS.indexOf(message.charAt(counter));
                int keyValue = (charPosition + shiftKey) % 26;

                char cyperValue = ALPAHABETS.charAt(keyValue);

                cyperText.append(cyperValue);
            }
        }

        return cyperText.toString();
    }

    public static String DecryptText(String message, int shiftKey) {
        //c(x) =  x - shiftKey Mod(%) 26;
        final String ALPAHABETS = "abcdefghijklmnopqrstuvwxyz";

        message = message.toLowerCase();

        StringBuilder plainText = new StringBuilder();

        for(int counter = 0;counter < message.length();counter++) {

            if(!Character.isLetter(message.charAt(counter))) {
                plainText.append(message.charAt(counter));
            }

            else {
                int charPosition = ALPAHABETS.indexOf(message.charAt(counter));
                int keyValue = (charPosition - shiftKey) % 26;

                if (keyValue < 0) {

                    keyValue = ALPAHABETS.length() + keyValue;
                }

                char plainValue = ALPAHABETS.charAt(keyValue);

                plainText.append(plainValue);
            }
        }

        return plainText.toString();

    }

}
