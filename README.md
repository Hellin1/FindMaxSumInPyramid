# FindMaxSumInPyramid


## Question
Write code for below problem. The input below is just an example and you should implement independent from the input. Please paste the link to the answer shared using pastebin, dotnetfiddle, jsfiddle, or any other similar web-site.
You will have an orthogonal triangle input from a file and you need to find the maximum sum of the numbers according to given rules below;

1. You will start from the top and move downwards to an adjacent number as in below.
2. You are only allowed to walk downwards and diagonally.
3. You can only walk over NON PRIME NUMBERS.
4. You have to reach at the end of the pyramid as much as possible.
5. You have to treat the input as pyramid.

According to above rules the maximum sum of the numbers from top to bottom in below example is 24.

      *1
     *8 4
    2 *6 9
   8 5 *9 3

As you can see this has several paths that fits the rule of NOT PRIME NUMBERS; 1>8>6>9, 1>4>6>9, 1>4>9>9
1 + 8 + 6 + 9 = 24.  As you see 1, 8, 6, 9 are all NOT PRIME NUMBERS and walking over these yields the maximum sum.

Paste the link to your code.

## Answer : 


        static void Main(string[] args)
        {

            string arr = @" 215
                            193 124
                            117 237 442
                            218 935 347 235
                            320 804 522 417 345
                            229 601 723 835 133 124
                            248 202 277 433 207 263 257
                            359 464 504 528 516 716 871 182
                            461 441 426 656 863 560 380 171 923
                            381 348 573 533 447 632 387 176 975 449
                            223 711 445 645 245 543 931 532 937 541 444
                            330 131 333 928 377 733 017 778 839 168 197 197
                            131 171 522 137 217 224 291 413 528 520 227 229 928
                            223 626 034 683 839 053 627 310 713 999 629 817 410 121
                            924 622 911 233 325 139 721 218 253 223 107 233 230 124 233";



            string[] lines = arr.Split(new string[] { "\r\n", "\r", "\n", "\t" }, StringSplitOptions.None);

            foreach (var item in lines)
            {
                Console.WriteLine(item.Trim());
            }


            List<string[]> newArr = new();
            foreach (var item in lines)
            {
                newArr.Add((item.Trim().Split()));
            }
            // list control
            foreach (var item in newArr)
            {
                Console.WriteLine(item);
            }


            // [0, 0, 0, 0]
            List<int> zeros = new();
            for (int i = 0; i < newArr.Count - 1; i++)
            {
                zeros.Add(0);
            }

            int zerosPoint = 0;

            int maxSum = 0;


            // [1, 1, 1, 1]
            List<int> ListDecimal = new();
            for (int i = 0; i < newArr.Count - 1; i++)
            {
                ListDecimal.Add(1);
            }
            int ListDecimalDegeri = CalculateNumberFrBinary(ListDecimal) + 1;


            List<int> maxSumList = new();

            // algo start
            int sayac = 0;
            while (zerosPoint < ListDecimalDegeri)
            {
                sayac++;
                List<int> anlikSonuc = new();
                int sonuc = 0;
                int secilenIndex = 0;
                int atlanacakDeger = 1;

                int j = 0;
                for (int i = 0; i < newArr.Count; i++)
                {
                    if (i == 0)
                    {
                        sonuc += int.Parse(newArr[0][0]);
                        anlikSonuc.Add(int.Parse(newArr[0][0]));
                    }
                    else
                    {
                        bool isPrime = PrimeCheck(int.Parse(newArr[i][secilenIndex]));
                        if (isPrime)
                        {
                            atlanacakDeger = AtlamaHesapla(i, newArr);
                            break;
                        }
                        else
                        {
                            sonuc += int.Parse(newArr[i][secilenIndex]);
                            anlikSonuc.Add(int.Parse(newArr[i][secilenIndex]));
                        }
                    }
                    if (j > newArr.Count - 3)
                    {
                        j = newArr.Count - 3;
                    }

                    if (zeros[j] == 0)
                    {
                    }
                    else
                    {
                        secilenIndex += 1;
                    }

                    j++;
                    Console.WriteLine("Sum : " + sonuc);
                    Console.WriteLine("Max Sum : " + maxSum);
                } // for loop end
                if (maxSumList.Count < anlikSonuc.Count)
                {
                    maxSumList = anlikSonuc;
                    maxSum = sonuc;
                }
                else if (maxSumList.Count == anlikSonuc.Count)
                {
                    if (maxSum < sonuc)
                    {
                        maxSum = sonuc;
                        maxSumList = anlikSonuc;
                    }
                }


                List<int> myList = new();
                zerosPoint += atlanacakDeger;
                zeros = DecimalToBinaryPy(zerosPoint, myList);
                while (zeros.Count < ListDecimal.Count)
                {
                    zeros.Insert(0, 0);
                }
            }

            Console.WriteLine("Max Sum :"+ maxSum);
            Console.WriteLine("Max Liste : "+ maxSumList);
            Console.WriteLine("sayaç: "+ sayac);
            Console.WriteLine("everything is done");
        }

        public static List<int> DecimalToBinaryPy(int num, List<int> myList)
        {
            Console.WriteLine(num); // 4 2 1 0.5
            if (num >= 1)
            {
                DecimalToBinaryPy(Decimal.ToInt32(num / 2), myList);
                myList.Add(num % 2);
            }
            return myList;

        }
        public static int CalculateNumberFrBinary(List<int> myList)
        {
            int sonuc = 0;
            for (int i = myList.Count - 1; i > -1; i--)
            {  // arr[i]*2**i
                Console.WriteLine(i);
                sonuc += (int)Math.Pow(myList[i] * 2, i);
            }
            Console.WriteLine("*********");
            return sonuc;
        }

        public static bool PrimeCheck(int sayi)
        {

            for (int i = 2; i < sayi; i++)
            {
                if (sayi % i == 0)
                {
                    return false;
                }
            }
            return true;
        }

        public static int AtlamaHesapla(int i, List<string[]> myList)
        {
            return (int)Math.Pow(2, myList.Count - 1 - i);
        }
    }


## Question 2: 
According to previous assignment (24) that you implemented what is the maximum sum of below input? It means please take this input (as file or constants directly inside the code) for your implementation and solve by using it.
215
193 124
117 237 442
218 935 347 235
320 804 522 417 345
229 601 723 835 133 124
248 202 277 433 207 263 257
359 464 504 528 516 716 871 182
461 441 426 656 863 560 380 171 923
381 348 573 533 447 632 387 176 975 449
223 711 445 645 245 543 931 532 937 541 444
330 131 333 928 377 733 017 778 839 168 197 197
131 171 522 137 217 224 291 413 528 520 227 229 928
223 626 034 683 839 053 627 310 713 999 629 817 410 121
924 622 911 233 325 139 721 218 253 223 107 233 230 124 233

## Answer 2 :
8186
