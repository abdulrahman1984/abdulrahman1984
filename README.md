- 👋 Hi, I’m @abdulrahman1984
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
abdulrahman1984/abdulrahman1984 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
using System;

namespace SimpleCalculator
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Simple Calculator in C#\r");
            Console.WriteLine("------------------------\n");

            double memory = 0;

            while (true)
            {
                Console.WriteLine("Choose an option:");
                Console.WriteLine("\t1 - Add");
                Console.WriteLine("\t2 - Subtract");
                Console.WriteLine("\t3 - Multiply");
                Console.WriteLine("\t4 - Divide");
                Console.WriteLine("\t5 - Square Root");
                Console.WriteLine("\t6 - Power");
                Console.WriteLine("\t7 - Percentage");
                Console.WriteLine("\t8 - Recall Memory");
                Console.WriteLine("\t9 - Clear Memory");
                Console.WriteLine("\t0 - Exit");
                Console.Write("Your option? ");

                string option = Console.ReadLine();

                if (option == "0") break;

                switch (option)
                {
                    case "1":
                        PerformOperation((a, b) => a + b, "add");
                        break;
                    case "2":
                        PerformOperation((a, b) => a - b, "subtract");
                        break;
                    case "3":
                        PerformOperation((a, b) => a * b, "multiply");
                        break;
                    case "4":
                        PerformOperation((a, b) => a / b, "divide", true);
                        break;
                    case "5":
                        PerformSingleOperation(a => Math.Sqrt(a), "square root");
                        break;
                    case "6":
                        PerformOperation(Math.Pow, "power");
                        break;
                    case "7":
                        PerformOperation((a, b) => a * b / 100, "percentage");
                        break;
                    case "8":
                        Console.WriteLine($"Memory recall: {memory}");
                        break;
                    case "9":
                        memory = 0;
                        Console.WriteLine("Memory cleared.");
                        break;
                    default:
                        Console.WriteLine("Invalid option.");
                        break;
                }
            }

            Console.Write("Press any key to close the Calculator console app...");
            Console.ReadKey();
        }

        private static void PerformOperation(Func<double, double, double> operation, string operationName, bool checkDivideByZero = false)
        {
            double num1 = GetNumber($"Enter first number to {operationName}: ");
            double num2 = GetNumber($"Enter second number to {operationName}: ");

            if (checkDivideByZero && num2 == 0)
            {
                Console.WriteLine("Cannot divide by zero.");
                return;
            }

            double result = operation(num1, num2);
            Console.WriteLine($"The result of {operationName}ing {num1} and {num2} is: {result}");
        }

        private static void PerformSingleOperation(Func<double, double> operation, string operationName)
        {
            double num = GetNumber($"Enter number to {operationName}: ");
            double result = operation(num);
            Console.WriteLine($"The result of {operationName}ing {num} is: {result}");
        }

        private static double GetNumber(string prompt)
        {
            Console.Write(prompt);
            while (!double.TryParse(Console.ReadLine(), out double number))
            {
                Console.Write("Invalid input. Please enter a valid number: ");
            }
            return number;
        }
    }
}
