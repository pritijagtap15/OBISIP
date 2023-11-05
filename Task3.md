import java.util.*;
class BankAccountSystem 
{
	String name;
    //username
	String username;
    //password of that user
	String password;
    //account no of user
	String accountNo;
    //balance available for user
	double balance = 1000000;
	int transactions = 0;
    // transaction history
	String transactionHistory = "";
    //Registration page
	public void register() 
	{
		Scanner sc = new Scanner(System.in);
		System.out.print("\nUser plz Enter Your Name : ");
		this.name = sc.nextLine();
		System.out.print("\nEnter Your Username : ");
		this.username = sc.nextLine();
		System.out.print("\nEnter Your Password : ");
		this.password = sc.nextLine();
		System.out.print("\nEnter Your Account Number :  ");
		this.accountNo = sc.nextLine();
		System.out.println("\nYou have Successfully Registered in Our Bank......Thank You!!!");
		System.out.println("Plz Kindly Login!!!");
	}
    //Log in page
	public boolean loginSystem() 
	{
		boolean isLogin = false;
		Scanner sc = new Scanner(System.in);
		do 
		{
			System.out.print("\nEnter Your Username : ");
			String Username = sc.nextLine();
			if ( Username.equals(username) ) 
			{
				do
				{
					System.out.print("\nEnter Your Password : ");
					String Password = sc.nextLine();
					if ( Password.equals(password) ) 
					{
						System.out.print("\nYou have Logged in Successfully!!!");
						isLogin = true;
					}
					else 
					{
						System.out.println("\nIncorrect Password");
					}
				}while ( !isLogin );
			}
			else 
			{
				System.out.println("\nUsername not found");
			}
		}while ( !isLogin );
		return isLogin;
	}
    //Transfer Money
	public void transfer() 
	{

		Scanner sc = new Scanner(System.in);
		System.out.print("\nEnter Recipient's Name : ");
		String receipent = sc.nextLine();
		System.out.print("\nEnter amount to transfer : ");
		float amount = sc.nextFloat();
		try 
		{
			if ( balance >= amount ) 
			{
				if ( amount <= 50000f ) 
				{
					transactions++;
					balance -= amount;
					System.out.println("\nSuccessfully Transferred to " + receipent);
					String str = amount + " Rs transferred to " + receipent + "\n";
					transactionHistory = transactionHistory.concat(str);
				}
				else 
				{
					System.out.println("\nSorry but our bank have some limits. The Maximum Limit is Rs.50000.00 only");
				}
			}
			else 
			{
				System.out.println("\nSorry Insufficient Balance");
			}
		}
		catch ( Exception e) 
		{
            System.out.println(e);
		}
	}
    //Money Withdraw
    public void withdraw() 
	{
		System.out.print("\nEnter amount to withdraw :  ");
		Scanner sc = new Scanner(System.in);
		float amount = sc.nextFloat();
		try 
		{
			if ( balance >= amount ) 
			{
				transactions++;
				balance -= amount;
				System.out.println("\nWithdraw Successful");
				String str = amount + " Rs Withdrawed\n";
				transactionHistory = transactionHistory.concat(str);

			}
			else 
			{
				System.out.println("\nInsufficient Balance");
			}

		}
		catch ( Exception e) 
		{
             System.out.println(e);
		}
	}
    //Money Deposit
	public void deposit() 
	{	
		System.out.print("\nEnter amount to deposit : ");
		Scanner sc = new Scanner(System.in);
		float amount = sc.nextFloat();	
		try 
		{
			if ( amount <= 1000000f ) 
			{
				transactions++;
				balance += amount;
				System.out.println("\nSuccessfully Deposited");
				String str = amount + " Rs deposited\n";
				transactionHistory = transactionHistory.concat(str);
			}
			else 
			{
				System.out.println("\nSorry. The Maximum Limit is Rs.1000000.00 only");
			}	
		}
		catch ( Exception e) 
		{
             System.out.println(e);
		}
	}
	public void checkBalance() 
	{
		System.out.println("\n" + balance + " Rs");
	}
	public void transHistory() 
	{
		if ( transactions == 0 ) 
		{
			System.out.println("\nEmpty");
		}
		else 
		{
			System.out.println("\n" + transactionHistory);
		}
	}
}
class ATM_InterfaceSystem 
{
	public static int takeIntegerInput(int limit) 
	{
		int input = 0;
		boolean flag = false;
		while ( !flag ) 
		{
			try 
			{
				Scanner sc = new Scanner(System.in);
				input = sc.nextInt();
				flag = true;

				if ( flag && input > limit || input < 1 ) 
				{
					System.out.println("Choose the number between 1 to " + limit);
					flag = false;
				}
			}
			catch ( Exception e ) 
			{
				System.out.println("Enter only integer value");
				flag = false;
			}
		};
		return input;
	}
	public static void main(String[] args) 
	{
		System.out.println("\n*************** WELCOME TO HDFC BANK ATM SYSTEM **************\n");
		System.out.println("1.REGISTER \n2.EXIT");
		System.out.print("Plz Enter Your Choice : ");
		int choice = takeIntegerInput(2);
		if ( choice == 1 ) 
		{
			BankAccountSystem b = new BankAccountSystem();
			b.register();
			do
			{
				System.out.println("\n1.LOGIN \n2.EXIT");
				System.out.print("Enter Your Choice : ");
				int ch = takeIntegerInput(2);
				if ( ch == 1 ) 
				{
					if (b.loginSystem()) 
					{
						System.out.println("\n\n**********WELCOME USER " + b.name + " ***********\n");
						boolean isFinished = false;
						while (!isFinished) 
						{
							System.out.println("\n1.Withdraw \n2.Deposit \n3.Transfer \n4.Transaction History \n5.Check Balance \n6.Exit");
							System.out.print("\nEnter Your Choice - ");
							int c = takeIntegerInput(6);
							switch(c) 
							{
								case 1:
								b.withdraw();
								break;
								case 2:
								b.deposit();
								break;
								case 3:
								b.transfer();
								break;
								case 4:
                b.transHistory();
								break;
								case 5:
                b.checkBalance();
								break;
								case 6:
								isFinished = true;
								break;
							}
						}
					}
				}
				else 
				{
					System.exit(0);
				}
			}while(true);
		}
		else 
		{
			System.exit(0);
		}
	}
}	
