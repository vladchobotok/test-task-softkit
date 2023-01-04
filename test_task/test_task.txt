package com.company;

import java.util.ArrayList;
import java.util.List;
import java.util.Random;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        List<String> strings = new ArrayList<>();
        int columnCount;
        int stringCount;
        int minStringLength = 5;
        int maxStringLength = 15;
        StringBuilder stringBuilder = new StringBuilder();

        Scanner scanner = new Scanner(System.in);
        System.out.print("Input number of columns >> ");
        columnCount = scanner.nextInt();
        System.out.print("Input number of strings >> ");
        stringCount = scanner.nextInt();

        createStrings(strings, stringBuilder, stringCount, minStringLength, maxStringLength);
        printTable(strings, columnCount);
    }

    public static void printTable(List<String> strings, int columnCount){

        System.out.println("--------" + columnCount + " COLUMNS--------");

        int stringsInRow = strings.size() / columnCount;
        int stringsInLastRow = strings.size() % columnCount;
        int iter = 0;

        for (int i = 0; i < stringsInRow; ++i) {
            for (int j = 0; j < columnCount; ++j) {
                System.out.print(strings.get(iter));
                ++iter;
            }
            System.out.println();
        }
        for (int i = 0; i < stringsInLastRow; i++) {
            System.out.print(strings.get(iter));
            ++iter;
        }
    }

    public static List<String> createStrings(List<String> strings, StringBuilder stringBuilder, int stringCount, int minStringLength, int maxStringLength){
        int stringLength;
        int spaceAmount;
        int maxLength = 0;
        Random random = new Random();

        for (int i = 0; i < stringCount; ++i) {

            stringLength = random.nextInt(maxStringLength - minStringLength + 1);
            stringLength += minStringLength;

            if(maxLength < stringLength){
                maxLength = stringLength;
            }

            for (int j = 0; j < stringLength; ++j) {
                char symbol = (char)(random.nextInt(26) + 'a');;
                stringBuilder.append(symbol);
            }

            strings.add(stringBuilder.toString());
            stringBuilder.setLength(0);
        }

        for (int i = 0; i < stringCount; ++i) {
            spaceAmount = maxLength - strings.get(i).length() + 5;

            stringBuilder.append(strings.get(i));

            for (int j = 0; j < spaceAmount; j++) {
                stringBuilder.append(' ');
            }
            strings.set(i, stringBuilder.toString());
            stringBuilder.setLength(0);
        }

        return strings;
    }
}