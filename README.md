# Bank-Management-System.223
using System;
using System.Collections.Generic;

namespace bankacc
{

    public class BankAccount
    {
        public int AccountNumber { get; set; }
        public string Name { get; set; }
        public double Balance { get; set; }
        public int AccountPin { get; set; }

        public void Withdraw(double amount)
        {
            if (amount > 0 && amount <= Balance)
            {
                Balance -= amount;
            }
            else
            {
                Console.WriteLine("Invalid withdrawal amount. Please try again.");
            }
        }

        public void Deposit(double amount)
        {
            if (amount > 0)
            {
                Balance += amount;
            }
            else
            {
                Console.WriteLine("Invalid deposit amount. Please try again.");
            }
        }
    }

    class Program
    {
        static List<BankAccount> accounts = new List<BankAccount>();

        static void Main(string[] args)
        {
            bool isRunning = true;
            //Do the following while isRunning is true
            while (isRunning)
            {
                //  Display the options the user has to choose from.
                try
                {
                    //
                    Console.WriteLine(@"----------------------------------
 Welcome to The Real World Bank! 
----------------------------------");
                    Console.WriteLine("1. Create Account");
                    Console.WriteLine("2. Login");
                    Console.WriteLine("3. Exit");
                    Console.Write("Enter your choice: ");
                    //Get user's choice
                    int choice = int.Parse(Console.ReadLine());
                    if (choice == 1)
                    {
                        Console.Clear();
                        CreateAccount();
                    }
                    else if (choice == 2)
                    {
                        Login();
                    }
                    else if (choice == 3)
                    {
                        isRunning = false;
                        return;
                    }
                    else
                    {
                        Console.WriteLine("Invalid choice");
                    }
                    continue;
                }
                //If the users gives wrong input i.e alphabets display a message
                catch
                {
                    Console.WriteLine("Invalid choice");
                    continue;
                }
            }
            Console.ReadKey();
        }

        static void CreateAccount()
        {
            //Create an instance of the BankAccount class
            BankAccount account = new BankAccount();
            Console.Write("Enter Account Holder Name: ");
            //Get the user's name
            account.Name = Console.ReadLine();
            //Create an instance of the Random class
            Random accno = new Random();
            //Generate a random account number between 100000 and 200000 
            account.AccountNumber = accno.Next(100000, 200001);
            //Find the account number entered, in the accounts list 
            BankAccount ExistingAccountNumber = accounts.Find(a => a.AccountNumber == account.AccountNumber);
            //If the account number already exists, generate another account number
            if (ExistingAccountNumber != null)
            {
                account.AccountNumber = accno.Next(100000, 200001);
                Console.WriteLine("Your account number is " + account.AccountNumber);
            }
            else
            {
                Console.WriteLine("Your account number is " + account.AccountNumber);
            }

            //Generate a random pin 
            account.AccountPin = accno.Next(1000, 10000);
            BankAccount ExistingAccountPin = accounts.Find(a => a.AccountPin == account.AccountPin);
            if (ExistingAccountPin != null)
            {
                account.AccountPin = accno.Next(100000, 200001);
                Console.WriteLine("Your pin is " + account.AccountPin);
            }
            else
            {
                Console.WriteLine("Your pin is " + account.AccountPin);
            }
            try
            {
                Console.Write("Enter Initial Balance: ");
                account.Balance = double.Parse(Console.ReadLine());
                accounts.Add(account);
                Console.WriteLine("Account created successfully.");
            }
            catch
            {
                Console.WriteLine("Wrong input.");
            }
            Console.Clear();
            PerformAccountOperations(account);
        }

        static void Login()
        {
            Console.Clear();
            Console.Write("Enter Account Number: ");
            int accountNumber = int.Parse(Console.ReadLine());
            BankAccount account = accounts.Find(a => a.AccountNumber == accountNumber);
            if (account != null)
            {
                Console.Write("Enter pin: ");
                int accountPin = int.Parse(Console.ReadLine());
                BankAccount pin = accounts.Find(a => a.AccountPin == accountPin);
                if (pin != null)
                {
                    PerformAccountOperations(account);
                }
                else
                {
                    Console.WriteLine("Wrong pin. Try again.");
                }
            }
            else
            {
                Console.WriteLine("Account not found.");
            }
        }


        static void PerformAccountOperations(BankAccount account)
        {
            bool run = true;
            while (run)
            {
                Console.WriteLine("Account Operations:");
                Console.WriteLine("1. Withdraw");
                Console.WriteLine("2. Deposit");
                Console.WriteLine("3. Check Balance");
                Console.WriteLine("4. Change pin");
                Console.WriteLine("5. Logout");
                Console.Write("Enter your choice: ");
                int choice = Convert.ToInt32(Console.ReadLine());

                if (choice == 1)
                {
                    Console.Clear();
                    Console.Write("Enter the amount to withdraw: ");
                    double amountToWithdraw = Convert.ToDouble(Console.ReadLine());
                    account.Withdraw(amountToWithdraw);
                    Console.WriteLine("Withdrawal successful. Current balance: " + account.Balance);
                }
                else if (choice == 2)
                {
                    Console.Clear();
                    Console.Write("Enter the amount to deposit: ");
                    double amountToDeposit = Convert.ToDouble(Console.ReadLine());
                    account.Deposit(amountToDeposit);
                    Console.WriteLine("Deposit successful. Current balance: " + account.Balance);
                }
                else if (choice == 3)
                {
                    Console.Clear();
                    Console.WriteLine("Current balance: " + account.Balance);
                }
                else if (choice == 4)
                {
                    Console.Clear();
                    Console.Write("Enter pin: ");
                    int accountPin = int.Parse(Console.ReadLine());
                    BankAccount pin = accounts.Find(a => a.AccountPin == accountPin);
                    if (pin != null)
                    {
                        accountPin = int.Parse(Console.ReadLine());
                        Console.Write("Enter new pin: ");
                        account.AccountPin = accountPin;
                        Console.WriteLine("Pin changed successfully.");
                    }
                    else
                    {
                        Console.WriteLine("Wrong pin. Try again.");
                    }
                }
                else if (choice == 5)
                {
                    Console.Clear();
                    Console.WriteLine("Logout successful. Goodbye, " + account.Name + "!");
                    run = false;
                }
                else
                {
                    Console.Clear();
                    Console.WriteLine("Invalid choice. Please try again.");
                    continue;
                }
                Console.WriteLine();
            }
        }


    }
}
