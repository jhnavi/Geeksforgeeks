# Sum of all substrings of a number
class Solution {
    public int sumSubstrings(String s) {
        int totalSum = 0;
        for (int i = 0; i < s.length(); i++) {
            for (int j = i + 1; j <= s.length(); j++) {
                String substring = s.substring(i, j);
                totalSum += Integer.parseInt(substring);
            }
        }
        return totalSum;
    }
    public static void main(String[] args) {
        String s = "6759";
        Solution ob = new Solution();
        System.out.println("Output: " + ob.sumSubstrings(s)); // Output: 8421
    }
}
# Quick sort

class Solution {
    static void quickSort(int arr[], int low, int high) {
        if (low < high) {
            int pivotIndex = partition(arr, low, high);
            quickSort(arr, low, pivotIndex - 1);
            quickSort(arr, pivotIndex + 1, high);
        }
    }

    static int partition(int arr[], int low, int high) {
        int pivot = arr[high];
        int i = low - 1;

        for (int j = low; j < high; j++) {
            if (arr[j] < pivot) {
                i++;
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        int temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;

        return i + 1;
    }
}

# Selection sort
class Solution {
    void selectionSort(int[] arr) {
        // code here
        for(int i=0;i<arr.length;i++){
            int a=i;
            for(int j=i+1;j<arr.length;j++){
                if(arr[j]<arr[a]){
                    a=j;
                }
            }
            int temp=arr[i];
            arr[i]=arr[a];
            arr[a]=temp;
        }
    }
}
# Insertion sort

class Solution {
    // Please change the array in-place
    public void insertionSort(int arr[]) {
        // code here
        for(int i=1;i<arr.length;i++){
            int temp=arr[i];
            int j=i-1;
            while(j>=0 && temp<arr[j]){
                arr[j+1]=arr[j];
                j--;
            }
            arr[j+1]=temp;
        }
    }
}

# Bubble sort
class Solution {
    // Function to sort the array using bubble sort algorithm.
    public static void bubbleSort(int arr[]) {
        // code here
        for(int i=0;i<arr.length;i++){
            for(int j=i+1;j<arr.length;j++){
                if(arr[j]<arr[i]){
                    int temp=arr[i];
                    arr[i]=arr[j];
                    arr[j]=temp;
                }
            }
        }
    }
}

# Binary search
class Solution{
    public int binarysearch(int[] arr, int k) {
        int l=0,r=arr.length-1;
        while(l<=r){
            int mid=(l+r)/2;
            if(arr[mid]==k){
                while(mid-1>-1 && arr[mid-1]==k){
                    mid=mid-1;
                }
                return mid;
            }
            else if(k<arr[mid]){
                r=mid-1;
            }
            else{
                l=mid+1;
            }
        }
        return -1;
    }
}
# Array sort
class Solution {

    static int search(int arr[], int x) {
        for(int i=0;i<arr.length;i++){
            if(x==arr[i]){
                return i;
            }
        }
        return -1;
        
    }
}

# Merge sort

class Solution {
    void merge(int[] arr, int l,int mid, int r) {
        int n1=mid-l+1;
        int n2=r-mid;
        int k=l;
        int[] L=new int[n1];
        int[] R=new int[n2];
        for(int i=0;i<n1;i++){
            L[i]=arr[k++];
        }
        for(int i=0;i<n2;i++){
            R[i]=arr[k++];
        }
        int i=0,j=0;
        k=l;
        while(i<n1 && j<n2){
            if(L[i]<R[j]){
                arr[k++]=L[i++];
            }
            else{
                arr[k++]=R[j++];
            }
        }
        while(i<n1){
            arr[k++]=L[i++];
        }
        while(j<n2){
            arr[k++]=R[j++];
        }
        
    }
    void mergeSort(int arr[], int l,int r){
        if(l<r){
            int mid=(l+r)/2;
            mergeSort(arr,l,mid);
            mergeSort(arr,mid+1,r);
            merge(arr,l,mid,r);
            
            
        }
    }
}

# Insert in sorted circular linked list

class Node1 {
    int data;
    Node next;

    Node1(int data) {
        this.data = data;
        this.next = null;
    }
}

class Solution {
    public Node sortedInsert(Node head, int data) {
        Node newNode = new Node(data);
        if (head == null) {
            newNode.next = newNode;
            return newNode;
        }

        Node current = head;
        while (true) {
            if (current.data <= data && data <= current.next.data) {
                // Insert between current and current.next
                break;
            }
            if (current.data > current.next.data) {
                if (data >= current.data || data <= current.next.data) {
                    break;
                }
            }

            current = current.next;
            if (current == head) {
                break;
            }
        }

        newNode.next = current.next;
        current.next = newNode;
        return (data < head.data) ? newNode : head;
    }

    public void printList(Node head) {
        if (head == null) return;

        Node temp = head;
        do {
            System.out.print(temp.data);
            temp = temp.next;
            if (temp != head) System.out.print("->");
        } while (temp != head);
        System.out.println();
    }
}

 class Main {
    public static void main(String[] args) {
        Solution list = new Solution();
        Node head = new Node(1);
        Node second = new Node(2);
        Node third = new Node(4);
        head.next = second;
        second.next = third;
        third.next = head;

        System.out.print("Original List: ");
        list.printList(head);

        int data = 2;
        head = list.sortedInsert(head, data);

        System.out.print("After Inserting " + data + ": ");
        list.printList(head);
    }
}

# Perfect Sum Problem

class Solution {
        public int helper(int[] nums,int idx,int target,int sum){
            if(idx==nums.length){
                return sum==target ? 1:0;
            }
            int include=helper(nums,idx+1,target,sum+nums[idx]);
            int exclude=helper(nums,idx+1,target,sum);
            return include+exclude;
        }
        public int perfectSum(int[] nums, int target) {
            return helper(nums,0,target,0);
        }
    }

# Find rectangle with corners as 1

class Solution {
    public boolean ValidCorner(int mat[][]) {
        // Code here
        int n=mat.length;
        int m=mat[0].length;
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(mat[i][j]==1){
                    for(int c=j+1;c<m;c++){
                        if(mat[i][c]==1){
                            for(int r=i+1;r<n;r++){
                                if(mat[r][c]==1 && mat[r][j]==1){
                                    return true;
                                }
                            }
                        }
                    }
                }
            }
        }
        return false;
    }
}

# Prime Number

class Solution {
    public static void main(String[] args) {
        int n = 7;
        boolean isPrime = isPrime(n);
        System.out.println("Input: n = " + n);
        System.out.println("Output: " + isPrime);
        if (isPrime) {
            System.out.println("Explanation: " + n + " has exactly two divisors: 1 and " + n + ", making it a prime number.");
        } else {
            System.out.println("Explanation: " + n + " is not a prime number.");
        }
    }

    static boolean isPrime(int n) {
        if (n <= 1) {
            return false;
        }
        for (int i = 2; i <= Math.sqrt(n); i++) {
            if (n % i == 0) {
                return false;
            }
        }
        return true;
    }
}

# Sieve of Eratosthenes

// User function Template for Java
class Solution {
    static ArrayList<Integer> sieveOfEratosthenes(int n) {
        // code here
        boolean []primes=new boolean[n+1];
        ArrayList<Integer> res=new ArrayList<>();
        Arrays.fill(primes,true);
        primes[0]=primes[1]=false;
        for(int i=2;i<=n;i++){
            if(primes[i]==true){
                for(int j=2*i;j<=n;j+=i){
                    primes[j]=false;
                }
            }
        }
        for(int i=0;i<n+1;i++){
            if(primes[i]==true){
                res.add(i);
            }
        }
        return res;
    }
}

# GCD of two numbers


class Solution {
    public static int gcd(int a, int b) {
        // code here
        while(b!=0){
            int temp=a%b;
            a=b;
            b=temp;
        }
        return a;
    }
}

# LCM And GCD

class Solution {
    public static int[] lcmAndGcd(int a, int b) {
        // code here
        int prod=a*b;
        while(b!=0){
            int temp=a%b;
            a=b;b=temp;
        }
        int gcd=a;
        int lcm=prod/gcd;
        return new int[] {lcm,gcd};
    }
}

# Pascal Triangle

// User function Template for Java

class Solution {

    ArrayList<Integer> nthRowOfPascalTriangle(int n) {
        // code here
        ArrayList<Integer> prev=new ArrayList<>();
        ArrayList<Integer> cur=new ArrayList<>();
        prev.add(1);
        for(int i=1;i<n;i++){
            cur=new ArrayList<>();
            cur.add(1);
            for(int j=1;j<i;j++){
                cur.add(prev.get(j-1)+prev.get(j));
            }
            cur.add(1);
            prev=cur;
        }
        return prev;
    }
}
