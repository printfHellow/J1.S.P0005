# J1.S.P0005

package mergesort;

/**
 *
 * @author phina
 */
import java.util.*;
public class MergeSort {
    public static void main(String[] args) {
        int[] a = inputArray();
        System.out.println("Before sorted:");
        outputArray(a);
        if (!isSorted(a)) {
            mergeSort(a, 0, a.length - 1);
        } else {
            System.out.println("Array already sorted");
        }
        System.out.println("After sorted:");
        outputArray(a);
    }

    public static int[] inputArray() {
        Scanner sc = new Scanner(System.in);
        Random r = new Random();
        int n;
        int[] a = null;

        while (true) {
            try {
                System.out.println("Input the number of elements in the array:");
                n = sc.nextInt();
                if (n > 0) {
                    a = new int[n];
                    for (int i = 0; i < n; i++) {
                        a[i] = r.nextInt(n);
                    }
                    break;
                } else {
                    System.out.println("Number of elements should be greater than 0.");
                }
            } catch (Exception e) {
                System.out.println("Invalid input. Please enter a valid number.");
                sc.nextLine(); // Clear the input buffer
            }
        }

        return a;
    }

    public static void outputArray(int[] a) {
        for (int i = 0; i < a.length; i++) {
            System.out.print(a[i]);
            if (i < a.length - 1) {
                System.out.print(", ");
            }
        }
        System.out.println();
    }

    public static void mergeSort(int[] a, int left, int right) {
        if (left < right) {
            int mid = left + (right - left) / 2;
            mergeSort(a, left, mid);
            mergeSort(a, mid + 1, right);
            merge(a, left, mid, right);
        }
    }

    public static void merge(int[] a, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;

        int[] L = new int[n1];
        int[] R = new int[n2];

        System.arraycopy(a, left, L, 0, n1);
        System.arraycopy(a, mid + 1, R, 0, n2);

        int i = 0, j = 0, k = left;
        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                a[k] = L[i];
                i++;
            } else {
                a[k] = R[j];
                j++;
            }
            k++;
        }

        while (i < n1) {
            a[k] = L[i];
            i++;
            k++;
        }

        while (j < n2) {
            a[k] = R[j];
            j++;
            k++;
        }
    }

    public static boolean isSorted(int[] a) {
        for (int i = 0; i < a.length - 1; i++) {
            if (a[i] > a[i + 1]) {
                return false;
            }
        }
        return true;
    }
}
