// Задача№1.Внутри класса MergeSort напишите метод mergeSort, 
// который принимает массив целых чисел a и реализует алгоритм сортировки слиянием. 
// Метод должен возвращать отсортированный массив.


// 1е решение
import java.util.ArrayList;
import java.util.Random;

class MergeSort{
    public static void main(String[] args) {
        Random rnd = new Random();
        ArrayList<Integer> arrlst = new ArrayList<Integer>();
        for (int i=0;i<6;i++){
            arrlst.add(rnd.nextInt(0, 6));
        }
        System.out.println(arrlst.toString());
        sort(arrlst);
        System.out.println(arrlst.toString());

    }
    static void sort(ArrayList<Integer> arr){
        if (arr.size()>1){
            ArrayList<Integer> arr1 = new ArrayList<Integer>(arr.size()/2);
            ArrayList<Integer> arr2 = new ArrayList<Integer>(arr.size()-arr.size()/2);
            for (int i=0;i<arr.size()/2;i++){
                arr1.add(arr.get(i));
            }
            for (int i=arr.size()/2;i<arr.size();i++){
                arr2.add(arr.get(i));
            }
            sort(arr1);
            sort(arr2);
            merge(arr,arr1,arr2);

        }
    }
    static void merge(ArrayList<Integer> arr, ArrayList<Integer>  arr1,ArrayList<Integer>  arr2){
        int i1 = 0;
        int i2 = 0;
        ArrayList<Integer> narr = new ArrayList<>();
        for(int i=0;i<arr1.size()+arr2.size();i++){
            if(i1<arr1.size() && i2<arr2.size()){
                if (arr1.get(i1)<arr2.get(i2)){
                    narr.add(arr1.get(i1));
                    i1++;
                }
                else{
                    narr.add(i, arr2.get(i2));
                    i2++;
                }
            }
            else{
                if(i1>=arr1.size() & i2<arr2.size()){
                    narr.add(arr2.get(i2));
                    i2++;
                }
                if(i2>=arr2.size() & i1<arr1.size()){
                    narr.add(arr1.get(i1));
                    i1++;
                }

            }
        }
        arr.clear();
        for(int i=0;i<narr.size();i++){
            arr.add(narr.get(i));
        }
    }
}


// 2е решение
import java.util.Arrays;

class MergeSort {
    public static int[] mergeSort(int[] sortArr) {
        int[] buffer1 = Arrays.copyOf(sortArr, sortArr.length);
        int[] buffer2 = new int[sortArr.length];
        int[] result = mergeSortInner(buffer1, buffer2, 0, sortArr.length);
        return result;
    }

    public static int[] mergeSortInner(int[] buffer1, int[] buffer2, int startIndex, int endIndex) {
        if (startIndex >= endIndex - 1) {
            return buffer1;
        }

    
        int middle = startIndex + (endIndex - startIndex) / 2;
        int[] sorted1 = mergeSortInner(buffer1, buffer2, startIndex, middle);
        int[] sorted2 = mergeSortInner(buffer1, buffer2, middle, endIndex);

        
        int index1 = startIndex;
        int index2 = middle;
        int destIndex = startIndex;
        int[] result = sorted1 == buffer1 ? buffer2 : buffer1;
        while (index1 < middle && index2 < endIndex) {
            result[destIndex++] = sorted1[index1] < sorted2[index2]
                    ? sorted1[index1++] : sorted2[index2++];
        }
        while (index1 < middle) {
            result[destIndex++] = sorted1[index1++];
        }
        while (index2 < endIndex) {
            result[destIndex++] = sorted2[index2++];
        }
        return result;
    }
    public static void main(String args[]) {
        int[] sortArr = {5, 1, 6, 2, 3, 4};
        int[] result = mergeSort(sortArr);
        System.out.println(Arrays.toString(result));
    }
}


// Эталонное решение от автора
import java.util.Arrays;

class MergeSort {
    public static int[] mergeSort(int[] a) {
        int n = a.length;
        if (n < 2) {
            return a;
        }
        int mid = n / 2;
        int[] l = new int[mid];
        int[] r = new int[n - mid];

        for (int i = 0; i < mid; i++) {
            l[i] = a[i];
        }
        for (int i = mid; i < n; i++) {
            r[i - mid] = a[i];
        }
        l = mergeSort(l);
        r = mergeSort(r);

        return merge(l, r);
    }

    public static int[] merge(int[] l, int[] r) {

        int left = l.length;
        int right = r.length;
        int[] a = new int[left + right];
        int i = 0, j = 0, k = 0;

        while (i < left && j < right) {
            if (l[i] <= r[j]) {
                a[k++] = l[i++];
            }
            else {
                a[k++] = r[j++];
            }
        }
        while (i < left) {
            a[k++] = l[i++];
        }
        while (j < right) {
            a[k++] = r[j++];
        }

        return a;
    }
}

class Printer{ 
    public static void main(String[] args) { 
        int[] a;

        if (args.length == 0) {
            a = new int[]{5, 1, 6, 2, 3, 4};
        } else {
            a = Arrays.stream(args[0].split(", ")).mapToInt(Integer::parseInt).toArray();
        }

        MergeSort answer = new MergeSort();
        String itresume_res = Arrays.toString(answer.mergeSort(a));
        System.out.println(itresume_res);
    }
}




// Задача№2.Напишите функцию removeEvenNumbers, которая принимала бы произвольный список целых чисел, 
// удаляла бы из него четные числа и выводила список без четных чисел.
// Напишите свой код в методе removeEvenNumbers класса Answer. 
// Метод removeEvenNumbers принимает на вход один параметр:

// Integer[] arr - список целых чисел

// Пример


// arr = new Integer[]{1, 2, 3, 4, 5, 6, 7, 8, 9};
// removeEvenNumbers(arr);

// // [1, 3, 5, 7, 9]

// arr = new Integer[]{2, 4, 6, 8};
// removeEvenNumbers(arr);

// // []

import java.util.Arrays;
import java.util.ArrayList;

class Answer {
    public static void removeEvenNumbers(Integer[] arr) {
        
        ArrayList<Integer> a = new ArrayList<>(Arrays.asList(arr));
        a.removeIf(n -> (n % 2 == 0));
        System.out.println(a);


    }
}

class Printer{
    public static void main(String[] args) {
        Integer[] arr = {};

        if (args.length == 0) {
            
            arr = new Integer[]{1, 2, 3, 4, 5, 6, 7, 8, 9};
        }
        else{
            arr = Arrays.stream(args[0].split(", "))
                    .map(Integer::parseInt)
                    .toArray(Integer[]::new);
        }

        Answer ans = new Answer();
        ans.removeEvenNumbers(arr);
    }
}


// Эталонное решение от автора

import java.util.Arrays;

class MergeSort {
    public static int[] mergeSort(int[] a) {
        int n = a.length;
        if (n < 2) {
            return a;
        }
        int mid = n / 2;
        int[] l = new int[mid];
        int[] r = new int[n - mid];

        for (int i = 0; i < mid; i++) {
            l[i] = a[i];
        }
        for (int i = mid; i < n; i++) {
            r[i - mid] = a[i];
        }
        l = mergeSort(l);
        r = mergeSort(r);

        return merge(l, r);
    }

    public static int[] merge(int[] l, int[] r) {

        int left = l.length;
        int right = r.length;
        int[] a = new int[left + right];
        int i = 0, j = 0, k = 0;

        while (i < left && j < right) {
            if (l[i] <= r[j]) {
                a[k++] = l[i++];
            }
            else {
                a[k++] = r[j++];
            }
        }
        while (i < left) {
            a[k++] = l[i++];
        }
        while (j < right) {
            a[k++] = r[j++];
        }

        return a;
    }
}

class Printer{ 
    public static void main(String[] args) { 
        int[] a;

        if (args.length == 0) {
            a = new int[]{5, 1, 6, 2, 3, 4};
        } else {
            a = Arrays.stream(args[0].split(", ")).mapToInt(Integer::parseInt).toArray();
        }

        MergeSort answer = new MergeSort();
        String itresume_res = Arrays.toString(answer.mergeSort(a));
        System.out.println(itresume_res);
    }
}




// Задача№3.Напишите функцию analyzeNumbers, которая принимает на вход целочисленный список arr и:

// Сортирует его по возрастанию и выводит на экран
// Находит минимальное значение в списке и выводит на экран - Minimum is {число}
// Находит максимальное значение в списке и выводит на экран - Maximum is {число}
// Находит среднее арифметическое значений списка и выводит на экран - Average is =  {число}
// Напишите свой код в методе analyzeNumbers класса Answer. Метод analyzeNumbers принимает на вход один параметр:

// Integer[] arr - список целых чисел

// Пример


// arr = new Integer[]{4, 2, 7, 5, 1, 3, 8, 6, 9};
// analyzeNumbers(arr)

// [1, 2, 3, 4, 5, 6, 7, 8, 9]
// Minimum is 1
// Maximum is 9
// Average is = 5

import java.util.Arrays;
import java.util.ArrayList;

class Answer {
    public static void analyzeNumbers(Integer[] arr) {

        Arrays.sort(arr);
        System.out.println(Arrays.toString(arr));
        System.out.println("Minimum is " + Arrays.stream(arr).min(Integer::compareTo).get());
        System.out.println("Maximum is " + Arrays.stream(arr).max(Integer::compareTo).get());
        System.out.println("Average is = " + (int) (Arrays.stream(arr).mapToInt(value -> value).sum() / Arrays.stream(arr).count()));

    }
}

class Printer{
    public static void main(String[] args) {
        Integer[] arr = {};

        if (args.length == 0) {
            arr = new Integer[]{4, 2, 7, 5, 1, 3, 8, 6, 9};
        }
        else{
            arr = Arrays.stream(args[0].split(", "))
                    .map(Integer::parseInt)
                    .toArray(Integer[]::new);
        }

        Answer ans = new Answer();
        ans.analyzeNumbers(arr);
    }
}


// Эталонное решение от автора


import java.util.Arrays;
import java.util.ArrayList;

class Answer {
    public static void analyzeNumbers(Integer[] arr) {
        ArrayList<Integer> ints = new ArrayList<>(Arrays.asList(arr));
        ints.sort(Integer::compareTo); // сортировка списка по возрастанию
        System.out.println(ints); // вывод списка на экран
        System.out.println("Minimum is " + ints.get(0)); // нахождение минимального значения в списке и вывод на экран
        System.out.println("Maximum is " + ints.get(ints.size()-1)); // нахождение максимального значения в списке и вывод на экран

        int sum = 0;
        for(int i : ints){ // вычисление суммы всех элементов списка
            sum += i;
        }
        System.out.println("Average is = " + sum / ints.size()); // вычисление среднего арифметического значений списка и вывод на экран
    }
}

class Printer{ 
    public static void main(String[] args) { 
      Integer[] arr = {};

      if (args.length == 0) {
        arr = new Integer[]{4, 2, 7, 5, 1, 3, 8, 6, 9};
      }
      else{
        arr = Arrays.stream(args[0].split(", "))
                        .map(Integer::parseInt)
                        .toArray(Integer[]::new);
      }     

      Answer ans = new Answer();      
      ans.analyzeNumbers(arr);
    }
}