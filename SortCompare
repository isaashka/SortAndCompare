//Sasha Ilinskaya 10/12/2021
//SortCompare is a program that creates a random list of numbers (size indicated by the user) and then gives 5 options for how to sort them.
//The options include Insertion Sort, Merge Sort, Quick Sort, Radix Sort, or all of them at once. It then prints the unsorted and sorted numbers
//as well as how many comparisons the sort made, using the sorting method chosen by user.
import java.util.Scanner;
import java.util.Arrays;
import java.util.LinkedList;
import java.util.Queue;

public class SortCompare {
//Four global counters are declared below for the sorts to add to every time they compare numbers to each other.
    static int COUNTER1 = 0;
    static int COUNTER2 = 0;
    static int COUNTER3 = 0;
    static int COUNTER4 = 0;

    //The next two global integers are specifically for radix sort. MAX_DIGIT keeps track of the maximum amount of digits a number in an array will have.
    //DIVIDE_INDEX tracks which iteration radix sort is on, since the function radixSort is recursive it needs a value outside to track that.
    static int MAX_DIGIT = 0;
    static int DIVIDE_INDEX = 0;

    //The main function starts up the program and asks the user for input to create a random number array. 
    //It then invokes the whichSort which is train station of the program.
    public static void main(String args[]){
        //A scanner is created to read user input. Once user enter an integer, a random array is created using the function random.
        Scanner scan = new Scanner(System.in);
        System.out.print("How many entries? ");
        int numOfEntries = scan.nextInt();
        int[] intArray = random(numOfEntries);

        //User gets to choose which sort method to use. User input is then sent through to whichSort method along with the random array.
        System.out.print("Which sort [m, q, i, r, all]? ");
        String input = scan.next();
        System.out.println();
        whichSort(input, intArray);
    }

    //whichSort is the hub from where all the sorts are invoked, then they are neatly printed out in this function.
    public static void whichSort(String input, int[] array){
        //The first if statement deals with merge sort. Array is printed, then sent through the mergeSort method, and then printed sorted. 
        //Between that the number of comparisons is printed.
        if(input.equals("m")){
            System.out.println("MERGE SORT");
            System.out.println("===============");
            printUnsorted(array);
            mergeSort(array, 0, array.length-1);
            System.out.println("Number of Comparisons: "+ COUNTER1);
            printSorted(array);
        }
        //The next if statement deals with quick sort. Array is printed, then sent through the quickSort method, and then printed sorted. 
        //Between that the number of comparisons is printed.
        else if(input.equals("q")){
             System.out.println("QUICK SORT");
             System.out.println("===============");
             printUnsorted(array);
             quickSort(array, 0, array.length-1);
             System.out.println("Number of Comparisons: "+ COUNTER2);
             printSorted(array);
        }
        //The next if statement deals with insertion sort. Array is printed, then sent through the insertionSort method, and then printed sorted. 
        //Between that the number of comparisons is printed.
        else if (input.equals("i")){
            System.out.println("INSERTION SORT");
            System.out.println("===============");
            printUnsorted(array);
            insertionSort(array);
            System.out.println("Number of Comparisons: "+ COUNTER3);
            printSorted(array);
        }
        //The next if statement deals with radix sort. Array is printed, then sent through the radixSort method, and then printed sorted. 
        //Between that the number of comparisons is printed.
        else if (input.equals("r")){
            System.out.println("RADIX SORT");
            System.out.println("===============");
            printUnsorted(array);

            //maxDigits is called to calculate what the maximum amount of digits a number in the array can have. Since the radixSort
            //is recursive, this is done outside of the function and it's saved as a global value.
            maxDigits(array);

            radixSort(array);
            System.out.println("Number of Comparisons: "+ COUNTER4);
            printSorted(array);
        }
        //The last if statement is the combination of all the above.
        else if (input.equals("all")){
            //To account for the fact that it's the original array that gets sorted. When we call all 4 sorts at once we need to make
            //sure they all start out with the same unsorted array. So for each sort a copy of the array is created. 
            int[] arrayMerge = array.clone();
            System.out.println("MERGE SORT");
            System.out.println("===============");
            printUnsorted(arrayMerge);
            mergeSort(arrayMerge, 0, arrayMerge.length-1);
            System.out.println("Number of Comparisons: "+ COUNTER1);
            printSorted(arrayMerge);
            System.out.println();
//
            int[] arrayQuick = array.clone();
            System.out.println("QUICK SORT");
            System.out.println("===============");
            printUnsorted(arrayQuick);
            quickSort(arrayQuick, 0, arrayQuick.length-1);
            System.out.println("Number of Comparisons: "+ COUNTER2);
            printSorted(arrayQuick);
            System.out.println();
//
            int[] arrayInsertion = array.clone();
            System.out.println("INSERTION SORT");
            System.out.println("===============");
            printUnsorted(arrayInsertion);
            insertionSort(arrayInsertion);
            System.out.println("Number of Comparisons: "+ COUNTER3);
            printSorted(arrayInsertion);
            System.out.println();
//
            int[] arrayRadix = array.clone();
            System.out.println("RADIX SORT");
            System.out.println("===============");
            printUnsorted(arrayRadix);

            maxDigits(arrayRadix);

            radixSort(arrayRadix);
            System.out.println("Number of Comparisons: "+ COUNTER4);
            printSorted(arrayRadix);
            System.out.println();
        }
    }

    //mergeSort takes in an array and the start and end values. This method recursively divides the array by creating a middle variable
    //which becomes the new end or start value for the next iteration. The base case is if the start value is the same as the end value,
    //at that point the function returns to a previous iteration and finishes it up with merge before moving further back.
    public static void mergeSort(int[] array, int start, int end){
        //Base case for the recursion to stop.
        if(start == end){
            return;
        }
        //New start or end value for the next iteration.
        int mid = (end + start)/2;
        
        //Recursive call, mergeSort calls mergeSort with new start and end values. 
        mergeSort(array, start, mid);
        mergeSort(array, mid+1, end);
        merge(array, start, mid, end);
        
    }
    //merge function works with mergeSort, it takes in the array and three values for the start, middle, and end. It creates two arrays
    //whose size is based on start, mid, and end. Both arrays are filled with numbers from the input array. Then it compares the values
    //of both arrays and puts them back in order into the original array. 
    public static void merge(int[] array, int start, int mid, int end){
        //Sizes for arrays are calculated using input values (we find our place on the array), then the arrays are initiated and filled 
        //with values from the original array.
        int arraySizeA = mid - start + 1;
        int arraySizeB = end - mid;

        int[] arrayA = new int[arraySizeA];
        int[] arrayB = new int[arraySizeB];

        for (int i = 0; i < arraySizeA; i ++){
            arrayA[i] = array[start + i];
        }
        for (int j = 0; j < arraySizeB; j++){
            arrayB[j] = array[mid + j + 1];
        }

        //Since I'm using a while loop, I created integers before the loop to keep track of which index the loop is on.
        //These indices are used for the following two while loops as well, so if one array runs out of values, the index won't be lost.
        //The first while loop only runs when both arrays have values. It compares values in both arrays and based on which one is larger
        //puts them back in the original array, incrementing the index of the array from which the value was taken.
        int indexOfA = 0, indexOfB = 0;
        int indexOfOriginal = start;
        while(indexOfA < arraySizeA && indexOfB < arraySizeB){
            if(arrayA[indexOfA] <= arrayB[indexOfB]){
                array[indexOfOriginal] = arrayA[indexOfA];
                indexOfA++;
            }
            else {
                array[indexOfOriginal] = arrayB[indexOfB];
                indexOfB++;
            }
            indexOfOriginal++;
            COUNTER1++;
        }
        //The next two loops only work if all the values in either array have been used up and we're only left with values in the other.
        //The loop just goes through the remaining values and adds them to the original array.
        while(indexOfA < arraySizeA){
            array[indexOfOriginal] = arrayA[indexOfA];
            indexOfA++; indexOfOriginal++;
        }
        while(indexOfB < arraySizeB){
            array[indexOfOriginal] = arrayB[indexOfB];
            indexOfB++; indexOfOriginal++;
        }
    }

    //quickSort is a recursive method whose base case is if end becomes less than start. So that it'se easier to see, I just reversed
    //the base case to a case under which the function will work -- as long as the start value is less than the end value.
    //The idea of this sort method is to use a pivot and sort the array based on their relation to the pivot value. By the time the 
    //length of the segment of the array is 1 the array is already sorted.
    public static void quickSort(int[] array, int start, int end){
        //As long as the if statement is true, the partition function will be called to create a middle pivot.
        //Then the function will call itself twice, one for the array before the middle value and the other for after.
        if(start < end){
            int mid = partition(array, start, end);
            quickSort(array, start, mid - 1);
            quickSort(array, mid + 1, end);
        }   
    }
    //partition function helps quickSort to find the index of a pivot as well as sorts the values of an array based on if they're
    //less than or more than the pivot.
    public static int partition(int[] array, int start, int end){
        //pivot is found using median3 function.
        int pivot = median3(array, start, (end-start)/2, end);

        //The following two integer values support the for loop. The first one keeps track of the index of the last value that was smaller
        //than the pivot. The second one keeps track of a value while its being switched positions with another.
        //The for loop checks the values of an array, if those values are smaller than the pivot then they are switched with a value one
        //before them. 
        int smallValueIndex = -1;
        int tempValue = 0;

        for(int j = 0; j < end; j++){
            if(array[j] <= pivot){
                COUNTER2++;
                smallValueIndex++;
                tempValue = array[j];
                array[j] = array[smallValueIndex];
                array[smallValueIndex] = tempValue; 
            }   
        }
        //The position of the pivot is found by using the smallValueIndex and adding 1 (since everything before it is less than the pivot 
        //and everything after is bigger). Using this index we call insertPivot to put the pivot at that index. Then the pivotIndex is returned
        //to quickSort.
        int pivotIndex = smallValueIndex+1;
        insertPivot(array, pivot, pivotIndex, end);

        return pivotIndex;
    }
    //insertPivot inserts a pivot at the spot it should be at in the array.
    public static void insertPivot(int[] array, int pivot, int index, int end){  
        //Two temporary value ints are made to accomodate for switching positions in an array.
        int tempValue1 = 0;
        int tempValue2 = 0;
        
        //Since we already know what the pivot value is, the following for loop gets rid of it by incrementing all the values to a previous value.
        //In median3 the pivot is placed at the end of the current segment, so by starting this loop at the end the pivot value is written over
        //the following one.
        for(int j = end; j < array.length-1; j++){
            array[j] = array[j+1];
        }

        //The current value at the index where pivot should be is saved and pivot is inserted into it.
        tempValue1 = array[index];
        array[index] = pivot;
        
        //All the following values in the array are shifted one over, using the temporary value ints to store the current value in for the next
        //one to take.
        for(int i = index+1; i < array.length; i++){
            tempValue2 = array[i];
            array[i] = tempValue1;
            tempValue1=tempValue2;
        }
    }
    //median3 takes in the array and indices for where the first, middle, and last values are in the current iteration of the array.
    //It then compares the values and chooses the median of the three and switches its place with the last value's place, before
    //returning the value of the median.
    public static int median3(int[] array, int firstIndex, int midIndex, int lastIndex){
        int first = array[firstIndex];
        int med = array[midIndex];
        int last = array[lastIndex];
        //In order to see which value is median, the if statement sees if the first value is less than one of the other two and bigger
        //than the other one of the two. If so then it's the median. It is then switched places with last and returned.
        if(first <= med && first >= last || first >= med && first <= last){
            int k = array[firstIndex];
            array[firstIndex] = array[lastIndex];
            array[lastIndex] = k;
            return first;
        }
        //If the first value didn't happen to be the median, then we check if the med value is the same way. If it fits the if
        //statement then med is median. And if it's not then we're left with the last value, so that's returned.
        else if(med <= first && med >= last || med >= first && med <= last){
            int k = array[midIndex];
            array[midIndex] = array[lastIndex];
            array[lastIndex] = k;
            return med;
        }
        else return last;
        
    }

    //insertionSort takes in an array and uses two loops to shift the values in an array to their correct place.
    public static void insertionSort(int[] array){
        //The first while loop goes through every value in the array. The while loop inside the first one only initiates
        //if the value of the previous object is bigger than the value of the current object. If it is then they switch places
        //until the loop statement is no longer true. 
        int currentIndex = 1;
        while(currentIndex < array.length){
            int previousIndex = currentIndex-1;
            int currentValue = array[currentIndex];
            while(previousIndex >= 0 && array[previousIndex] > currentValue){
                array[previousIndex+1] = array[previousIndex];
                previousIndex--;
                COUNTER3++;
            }
            //The current value is placed at where the previousIndex stopped decrementing. And the currentIndex then goes up by one
            //to move on to the next value.
            array[previousIndex+1] = currentValue; 
            currentIndex++;
            COUNTER3++;
        }
    }
    
    //radixSort is a recursive function that takes in a array. The base case for this function is if the global value MAX_DIGIT
    //is equal to 0. If it's not then it creates 19 queues into which every value in the array is sorted based on the current
    //digit's value for each. At the end all the queues are added back into the array in order from least to greatest (by current value).
    public static void radixSort(int[] array){
        //Every iteration will reduce the current digit we're working through, so the global value MAX_DIGIT is decremented at the start.
        //The base case checks if the MAX_DIGIT is 0.
        MAX_DIGIT--;
        if(MAX_DIGIT == 0){
            return;
        }
        //19 queues are created. 9 for positive numbers, 9 for negative numbers, and 1 for 0s.
        Queue<Integer> q0 = new LinkedList<>();
        Queue<Integer> q1 = new LinkedList<>();
        Queue<Integer> q2 = new LinkedList<>();
        Queue<Integer> q3 = new LinkedList<>();
        Queue<Integer> q4 = new LinkedList<>();
        Queue<Integer> q5 = new LinkedList<>();
        Queue<Integer> q6 = new LinkedList<>();
        Queue<Integer> q7 = new LinkedList<>();
        Queue<Integer> q8 = new LinkedList<>();
        Queue<Integer> q9 = new LinkedList<>();
        Queue<Integer> qn1 = new LinkedList<>();
        Queue<Integer> qn2 = new LinkedList<>();
        Queue<Integer> qn3 = new LinkedList<>();
        Queue<Integer> qn4 = new LinkedList<>();
        Queue<Integer> qn5 = new LinkedList<>();
        Queue<Integer> qn6 = new LinkedList<>();
        Queue<Integer> qn7 = new LinkedList<>();
        Queue<Integer> qn8 = new LinkedList<>();
        Queue<Integer> qn9 = new LinkedList<>();
        
        //The following loop goes through the entire array. It starts out by separating the current digit of the value,
        //then it checks what value out 19 it corresponds to and it's added to the queue that holds those values.
        for(int i = 0; i < array.length; i++){
            
            int currentDigit = (int)((array[i]/(Math.pow(10, DIVIDE_INDEX))) % 10);

            //The 0 queue checks if the absolute value of the current digit is equal to 0. It came up as a problem for
            //numbers like -10 or negative numbers that had less digits than the maximum (such as -7 with maximum digits
            //being 2).
            if(Math.abs(currentDigit) == 0){
                q0.add(array[i]);
            }
            if(currentDigit == 1){
                q1.add(array[i]);
            }
            if(currentDigit == 2){
                q2.add(array[i]);
            }
            if(currentDigit == 3){
                q3.add(array[i]);
            }
            if(currentDigit == 4){
                q4.add(array[i]);
            }
            if(currentDigit == 5){
                q5.add(array[i]);
            }
            if(currentDigit == 6){
                q6.add(array[i]);
            }
            if(currentDigit == 7){
                q7.add(array[i]);
            }
            if(currentDigit == 8){
                q8.add(array[i]);
            }
            if(currentDigit == 9){
                q9.add(array[i]);
            }
            if(currentDigit == -1){
                qn1.add(array[i]);
            }
            if(currentDigit == -2){
                qn2.add(array[i]);
            }
            if(currentDigit == -3){
                qn3.add(array[i]);
            }
            if(currentDigit == -4){
                qn4.add(array[i]);
            }
            if(currentDigit == -5){
                qn5.add(array[i]);
            }
            if(currentDigit == -6){
                qn6.add(array[i]);
            }
            if(currentDigit == -7){
                qn7.add(array[i]);
            }
            if(currentDigit == -8){
                qn8.add(array[i]);
            }
            if(currentDigit == -9){
                qn9.add(array[i]);
            }
        }

        DIVIDE_INDEX++;

        //currentIndex acts as the current place in the original array we're at. Since there's multiples queues being
        //added, we need a value outside the loop.
        //Each while loop adds its value to the array, deleting them from the queue as each one is added. 
        int currentIndex = 0;
        while(qn9.size() != 0){
            array[currentIndex] = qn9.peek();
            qn9.remove();
            currentIndex++;
        }
        while(qn8.size() != 0){
            array[currentIndex] = qn8.peek();
            qn8.remove();
            currentIndex++;
        }
        while(qn7.size() != 0){
            array[currentIndex] = qn7.peek();
            qn7.remove();
            currentIndex++;
        }
        while(qn6.size() != 0){
            array[currentIndex] = qn6.peek();
            qn6.remove();
            currentIndex++;
        }
        while(qn5.size() != 0){
            array[currentIndex] = qn5.peek();
            qn5.remove();
            currentIndex++;
        }
        while(qn4.size() != 0){
            array[currentIndex] = qn4.peek();
            qn4.remove();
            currentIndex++;
        }
        while(qn3.size() != 0){
            array[currentIndex] = qn3.peek();
            qn3.remove();
            currentIndex++;
        }
        while(qn2.size() != 0){
            array[currentIndex] = qn2.peek();
            qn2.remove();
            currentIndex++;
        }
        while(qn1.size() != 0){
            array[currentIndex] = qn1.peek();
            qn1.remove();
            currentIndex++;
        }
        while(q0.size() != 0){
            array[currentIndex] = q0.peek();
            q0.remove();
            currentIndex++;
        }
        while(q1.size() != 0){
            array[currentIndex] = q1.peek();
            q1.remove();
            currentIndex++;
        }
        while(q2.size() != 0){
            array[currentIndex] = q2.peek();
            q2.remove();
            currentIndex++;
        }
        while(q3.size() != 0){
            array[currentIndex] = q3.peek();
            q3.remove();
            currentIndex++;
        }
        while(q4.size() != 0){
            array[currentIndex] = q4.peek();
            q4.remove();
            currentIndex++;
        }
        while(q5.size() != 0){
            array[currentIndex] = q5.peek();
            q5.remove();
            currentIndex++;
        }
        while(q6.size() != 0){
            array[currentIndex] = q6.peek();
            q6.remove();
            currentIndex++;
        }
        while(q7.size() != 0){
            array[currentIndex] = q7.peek();
            q7.remove();
            currentIndex++;
        }
        while(q8.size() != 0){
            array[currentIndex] = q8.peek();
            q8.remove();
            currentIndex++;
        }
        while(q9.size() != 0){
            array[currentIndex] = q9.peek();
            q9.remove();
            currentIndex++;
        }

        //Recursive call.
        radixSort(array); 
    }
    //maxDigits calculates what the maximum amount of digits is in a given array.
    public static void maxDigits(int[] array){
        int maxNum = array.length;
        //The loop divides the biggest number in the array by 10 until it's 0. Every time it adds 1 to the global value MAX_DIGIT.
        while(maxNum != 0){
            maxNum /= 10;
            MAX_DIGIT++;
        } 
        //This addition accounts for the first call of radixSort where the MAX_DIGIT is decremented by 1.
        MAX_DIGIT++;
    }

    //The random function takes in the int for the length of an array. It then creates the array and fills it with random 
    //numbers from the value of negative size to positive size. The finished array is returned.
    public static int[] random(int size){
        int min = size * -1;
        int max = size;
        int[] randomArray = new int[size];
        //The loop fills each slot of randomArray with a randomly generated number from min to max.
        for(int i = 0; i < size; i++){
            int randomNum = (int) (Math.random() * ((max - min + 1)) + min);
            randomArray[i] = randomNum;
        }    
        return randomArray;
    }
   
    //printUnsorted takes an array and calls printArray if the length of the array is less than 20.
    public static void printUnsorted(int[] array){
        if(array.length < 20){
            System.out.print("unsorted array: ");
            printArray(array);
        }
    }
    //printSorted takes an array and calls printArray if the length of the array is less than 20.
    public static void printSorted(int[] array){
        if(array.length < 20){
            System.out.print("sorted array: ");
            printArray(array);
        }
    }
    //printArray takes in an array and using a loop prints out each individual value of the array with spaces between.
    public static void printArray(int[] array){
        int len = array.length;
        for(int i = 0; i < len; i++){              
            int j = array[i];
            System.out.print(j + " ");
        }
        System.out.println();
    }
}
