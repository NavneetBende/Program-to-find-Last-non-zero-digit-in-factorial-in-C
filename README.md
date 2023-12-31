# Program-to-find-Last-non-zero-digit-in-factorial-in-C

Last Non-Zero digit in Factorial in C
Here, in this page we will discuss the program to find the last non-zero digit in factorial in C Programming language. We are given with an integer value and need to return the last non-zero digit in its factorial.

Last Non-Zero digit in Factorial in C
Method Discussed :
Method 1 : Recursive way, without handeling overflow condition
Method 2 : Recursive way, handeling overflow condition
Method 1 :
Simple approach is to calculate the factorial of the number then, track its unit digit until the non-zero digit found.

Create a recursive function say fact(int n) to calculate the factorial,
Base condition: if(n<=1) return 1
Otherwise return n*fact(n-1).
After getting the factorial, and store it in variable say factorial.
Run a loop till (factorial % 10 != 0)
After that, print(factorial % 10)
Method 1 : Code in C
Run
#include <stdio.h>
//Recursive function to calculate the factorial
int fact(int n){

   if(n <= 1) //Base Condition
   return 1;

   return n*fact(n-1);
}

//Driver Code
int main(){

   int n=5;
   int factorial = fact(n);

   while(factorial%10==0)
   {
        factorial /= 10;
   }

   printf("%d",factorial%10);
}
Output :
2
Note
The above method is not suitable to find the factorial of slightly large numbers due to arithmetic overflow. So below given method will handle the arithmetic overflow condition.
Method 2 (Recursive Approach):
In this algorithm we will discuss the recursive approach to find the last non zero digit in factorial of the given number.

Create a recursive function say lastDigit(int n, int result[], int countFive).
Now, divide each array element into its shortest divisible form by 5 and increase count of such occurrences and store it in variable say countFive.
Now divide each array element into its shortest divisible form by 2 and decrease count of such occurrences i.e, countFive–. This way we are not considering the multiplication of 2 and a 5 in our multiplication(number of 2’s present in multiplication result upto n is always more than number 0f 5’s).
Multiply each number(after removing pairs of 2’s and 5’s) and store just last digit by taking remainder by 10.
Now call recursively for smaller numbers by (currentNumber – 1) as parameter.
Method 2 : Code in C
Run
#include <stdio.h>

void lastDigit(int n, int result[], int countFive)
{
  int number = n; 

  //Base condition
  if (number == 1)
      return;


  while (number % 5 == 0) {
        number /= 5;
        countFive++;
  }


  while (countFive != 0 && (number & 1) == 0) {
        number /= 2; 
        countFive--;
  }

  result[0] = (result[0] * (number % 10)) % 10;
  lastDigit(n - 1, result, countFive);


}

int lastNon0Digit(int n)
{
   int result[] = { 1 }; // single element array.
   lastDigit(n, result, 0);
   return result[0];
}

int main()
{
   int n=5;
   printf("%d ",lastNon0Digit(n));
   return 0;
}
Output :
2
