#package com.company;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {

        int encrypt_key;
        String plaintext, ciphertext;
        plaintext = user_text();
        encrypt_key = encryption_key();
        ciphertext= encode(plaintext, encrypt_key);
        System.out.print("Ciphertext: " + ciphertext);
    }

    static int encryption_key(){
        Scanner input = new Scanner(System.in);
        int encrypt_key;
        do{
            System.out.print("Rotation: ");
            encrypt_key = input.nextInt();
            if(encrypt_key<1){
                System.out.println("Too low. Enter higher number");
            }
            else if(encrypt_key>25){
                System.out.println("Too high. Enter lower number");
            }
        } while (encrypt_key >25 || encrypt_key<1);
        System.out.println("Success");
        return encrypt_key;
    }

    static String user_text(){
        Scanner input = new Scanner(System.in);
        String plaintext;
        System.out.print("Plaintext: ");
        plaintext = input.nextLine();
        plaintext = plaintext.toLowerCase();
        return plaintext;
    }

    static String encode (String plaintext, int encrypt_key){
        String cipher = "";
        int old_ascii=0;
        int new_ascii=0;

        for(int i=0; i < plaintext.length(); i++){
            old_ascii= 0 + plaintext.charAt(i);
            if(old_ascii>=97  && old_ascii<=122){
                new_ascii= old_ascii + encrypt_key;
            }
            else{
                new_ascii=old_ascii;
            }
            if(new_ascii>122){
                new_ascii= (new_ascii -97) % 26 + 97;
            }
            char cipher_character = (char) new_ascii;
            cipher = cipher + cipher_character;
        }
        return cipher;
    }
}
