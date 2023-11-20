using System.Reflection.Metadata.Ecma335;
using System.Threading.Channels;

namespace Laba_4
{
    internal class Program
    {
        //----------Функция 4 - Добавление элементов----------\\
        static int[] AddElems(int[] arr)
        {
            int K;
            bool isConvert;
            do
            {
                Console.WriteLine("Введите количество добавляемых элементов");
                isConvert = int.TryParse(Console.ReadLine(), out K);
                if (!isConvert || K < 0)
                    Console.WriteLine("Неправильно введено число.\nПопробуйте еще раз.\n");
            }
            while (!isConvert || K < 0);
            if (K == 0)
            {
                Console.WriteLine($"\nДобавлено {K} элементов");
                return arr;
            }
            else
            {
                int[] newArr = new int[arr.Length + K];
                for (int i = 0; i < arr.Length; i++)
                    newArr[i] = arr[i];

                newArr = Metods(newArr, K);
                Console.WriteLine($"\nДобавлено {K} элементов\n");
                return newArr;
            }
        }
        
        //----------Функция 4 - Добавление элементов----------\\
        //----------Вспомогательная функция выбор способа ввода новых элементов массива----------\\
        static int[] Metods(int[] arr, int K)
        {
            int value;
            bool isConvert;
            do
            {
                Console.WriteLine("Выберите способ ввода элементов");
                Console.WriteLine("1. С помощью ДСЧ");
                Console.WriteLine("2. С помощью личных значений");
                isConvert = int.TryParse(Console.ReadLine(), out value);
                switch (value)
                {
                    case 1:
                        {
                            Random rnd = new Random();
                            for (int i = 0; i < K; i++)
                                arr[arr.Length - K + i] = rnd.Next(-99, 99);
                            break;
                        }
                    case 2:
                        {
                            arr = Values(arr, K);
                            break;
                        }
                }
            }
            while (!isConvert || K < 0);
            return arr;
        }
        //----------Функция 4 - Добавление элементов----------\\
        //----------Вспомогательная функция выбор способа ввода новых элементов массива самим пользователем----------\\
        static int[] Values(int[] arr, int K)
        {
            int number = 0;
            int elem;
            bool isConvert;
            do
            {
                Console.WriteLine($"Введите элемент под номером {number + 1}");
                isConvert = int.TryParse(Console.ReadLine(), out elem);
                if (isConvert & K != 0)
                {
                    arr[arr.Length - K + number] = elem;
                    number++;
                }
                else
                {
                    Console.WriteLine("Неправильно введено число.\nПопробуйте еще раз.\n");
                    number--;
                }
            } while (!isConvert || number != K);
            return arr;
        }


        //----------Функция 3 - Удаление элементов под четными индексами----------\\
        static int[] RemElems(int[] arr)
        {
            int[] newArr = new int[arr.Length / 2];
            int j = 0;
            for (int i = 0; i < arr.Length; i++)
            {
                if (i % 2 != 0)
                    newArr[j++] = arr[i];
            }
            arr = newArr;
            Console.WriteLine("\nУдаление завершено\n");
            return arr;
        }
        //----------Функция 5 - Перестановка максимального и минимального элемента----------\\
        static int[] Swap(int[] arr)
        {
            int Minimum = int.MaxValue;
            int Maximum = int.MinValue;
            int MaxIndex = 0;
            int MinIndex = 0;
            int[] newArr = arr;
            for (int i = 0; i < arr.Length; i++)
            {
                if (arr[i] <= Minimum)
                {
                    Minimum = arr[i];
                    MinIndex = i;
                }

                if (arr[i] >= Maximum)
                {
                    Maximum = arr[i];
                    MaxIndex = i;
                }
            }
            newArr[MaxIndex] = Minimum;
            arr[MinIndex] = Maximum;
            arr[MaxIndex] = newArr[MaxIndex];
            Console.WriteLine("\nПерестановка выполнена\n");
            return arr;
        }
        static void Main(string[] args)
        {
            int[] arr = new int[0];
            int answer;
            bool isConvertAnsw;
            int lenght;
            do
            {  //Выбор номера в меню
                Console.WriteLine("1.Сформировать массив из n элементов");
                Console.WriteLine("2.Распечатать массив");
                Console.WriteLine("3.Выполнить удаление всех элементов с четными индексами");
                Console.WriteLine("4.Добавить K элементов в конец массива");
                Console.WriteLine("5.Выполнить перестановку минимального и максимального элемента в массиве");
                Console.WriteLine("6.Найти первый отрицательный элемент и подсчитать кол-во сравнений");
                Console.WriteLine("7.Выполнить сортировку простым включением");
                Console.WriteLine("8.Поиск элемента по массиву");
                Console.WriteLine("9.Выход");
                //Проверка корректности ввода номера в меню
                do
                {
                    isConvertAnsw=int.TryParse(Console.ReadLine(), out answer);
                    if (!isConvertAnsw ||  answer>=10 || answer<=0)
                    {
                        Console.WriteLine("Неправильно введено число.\nПопробуйте еще раз.\n");
                    }
                }
                while (!isConvertAnsw & answer>=10 & answer<=0) ;
                //Функции 1-8
                switch (answer)
                {   //----------Функция 1 - формирования массива----------\\
                    case 1:
                        {
                            bool isCorrect;
                            int sposob;
                            //Выбор способа формирования массива
                            do
                            {
                                Console.WriteLine("Выберите способо формирования массива");
                                Console.WriteLine("1.С помощью датчика случайных чисел");
                                Console.WriteLine("2.Личные значения ");
                                isCorrect = int.TryParse(Console.ReadLine(), out sposob);
                                if (!isCorrect)
                                    Console.WriteLine("Введено некорректное значение");
                            } while (!isCorrect);

                            //Проверка корректного ввода элементов массива
                            bool isNumber;
                            do
                            {
                                Console.WriteLine("Укажите количество элементов в массиве массива");
                                isNumber = int.TryParse(Console.ReadLine(), out lenght);
                                if (!isNumber)
                                    Console.WriteLine("Введено некорректное значение");
                                if (lenght == 0)
                                {
                                    Console.WriteLine("\nСформирован пустой массив \n");

                                }
                            }
                            while (!isNumber);
                            //Формирование массива
                            if (lenght != 0) 
                            {
                                switch (sposob)
                                {
                                    //Формирование массива ДСЧ
                                    case 1:
                                        {
                                            arr = new int[lenght];
                                            Random a = new Random();
                                            for (int i = 0; i < arr.Length; i++)
                                                arr[i] = a.Next(-100, 100);
                                            Console.WriteLine("\nМассив сформирован\n");
                                            break;
                                        }
                                    //Формирование массива из элементов пользователя
                                    case 2:
                                        {
                                            int elem;
                                            bool isConvert;
                                            int number = 1;
                                            arr = new int[lenght];
                                            do
                                            {
                                                Console.WriteLine($"Введите элемент массива под номером {number}");
                                                isConvert = int.TryParse(Console.ReadLine(), out elem);
                                                if (!isConvert)
                                                    Console.WriteLine("Введено некорректное значение");
                                                else
                                                {
                                                    arr[number - 1] = elem;
                                                    number++;
                                                }
                                            } while (!isConvert || number - 1 < arr.Length);
                                            Console.WriteLine("\nМассив сформирован\n");
                                            break;
                                        }
                                }
                            }
                            break;
                        }
                    //----------Функция 2 - Вывод массива----------\\
                    case 2:
                        {
                            if (arr.Length != 0)
                            {
                                Console.Write("\nМассив имеет вид: ");
                                for (int i = 0; i < arr.Length; i++)
                                    Console.Write(arr[i] + " ");
                                Console.WriteLine("");
                            }
                            else Console.WriteLine("\nМассив пуст\n");
                            Console.WriteLine();
                            break;
                        }
                    //----------Функция 3 - Удаление элементов под четными индексами----------\\
                    case 3:
                        {
                            if (arr.Length != 0)
                            {
                                arr = RemElems(arr);
                                break;
                            }
                            else
                            {
                                Console.WriteLine("\nМассив пуст\n");
                                break;
                            }
                        }
                    //----------Функция 4 - Добавление элементов----------\\
                    case 4:
                        {
                            if (arr.Length != 0)
                            {
                                arr = AddElems(arr);
                                break;
                            }
                            else
                            {
                                Console.WriteLine("\nМассив пуст\n");
                                break;
                            }
                        }
                    case 5:
                        {
                            if (arr.Length != 0)
                            {
                                arr = Swap(arr);
                                break;
                            }
                            else
                            {
                                Console.WriteLine("\nМассив пуст\n");
                                break;
                            }
                        }
                    case 6:
                        {
                            break;
                        }
                    case 7:
                        {
                            break;
                        }
                    case 8:
                        {
                            break;
                        }
                    case 9:
                        {
                            Console.WriteLine("Работа завершена");
                            break;
                        }
                }   
            }
            while (answer != 9);
        }
    }
}