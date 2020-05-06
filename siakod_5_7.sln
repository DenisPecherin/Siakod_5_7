using System;
using System.Diagnostics;

namespace Siakod_5_7
{
    class Program
    {
        //Последовательный поиск
        public static int ConsistentSearch(int[] array, int value)
        {
            for (int i = 0; i < array.Length; i++)
                if (array[i] == value)
                    return i;
            return -1;
        }

        //Последовательный поиск с барьером
        public static int ConsistentSearchWithBarrier(int[] array, int value)
        {
            if (array.Length == 0)
                return -1;

            int i, last;
            last = array[array.Length - 1];
            array[array.Length - 1] = value;

            for (i = 0; array[i] != value; i++) ;

            array[array.Length - 1] = last;

            if (i != (array.Length - 1) || last == value)
                return i;
            return -1;
        }

        //Бинарный поиск
        public static int BinarySearch(int[] array, int value)
        {
            if (array.Length == 0)
                return -1;

            int mid, low, high;
            low = 0;
            high = array.Length - 1;

            while (low <= high)
            {
                mid = low + (high - low) / 2;

                if (array[mid] == value)
                    return mid;
                if (array[mid] < value)
                    low = mid + 1;
                else
                    high = mid - 1;
            }
            return -1;
        }

        //Интерполяционный поиск
        public static int InterpolationSearch(int[] array, int value)
        {
            if (array.Length == 0)
                return -1;

            int mid, low, high;
            low = 0;
            high = array.Length - 1;

            while (array[low] < value && value < array[high])
            {
                if (array[high] == array[low])
                    break;
                mid = low + ((value - array[low]) * (high - low)) / (array[high] - array[low]);
                if (array[mid] < value)
                    low = mid + 1;
                else if (value < array[mid])
                    high = mid - 1;
                else
                    return mid;
            }

            if (array[low] == value)
                return low;
            if (array[high] == value)
                return high;
            return -1;
        }

        static void Main(string[] args)
        {
            int[] CreateArray(int size)
            {
                int[] rez = new int[size];

                for (int i = 0; i < size; i++)
                    rez[i] = i;
                return rez;
            }
            Stopwatch stopwatch = new Stopwatch();
            int[] M = new int[] { 5_000, 10_000, 20_000 };
            int[] N = new int[] { 1_000, 2_000, 4_000, 8_000, 16_000 };
            Func<int[], int, int>[] funcs = new Func<int[], int, int>[]
            {
                ConsistentSearch,
                ConsistentSearchWithBarrier,
                BinarySearch,
                InterpolationSearch
            };
            foreach (int n in N)
            {
                int[] array = CreateArray(n);
                foreach (int m in M)
                {
                    Random random = new Random();
                    foreach (Func<int[], int, int> func in funcs)
                    {
                        stopwatch.Restart();
                        func(array, random.Next(-n, 2 * n));
                        stopwatch.Stop();
                        Console.WriteLine($"N: {n}; M: {m}; Algoritm: {func.Method.Name}; Time: {stopwatch.Elapsed.Ticks}; ");
                    }
                }
            }
        }
    }
}
