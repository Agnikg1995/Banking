# Banking
class BankAccount:
    def __init__(self, account_number, username, password, account_holder, balance=0):
        self.account_number = account_number
        self.username = username
        self.password = password  # Password attribute
        self.account_holder = account_holder
        self.balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            print(f"Successfully deposited ${amount}. New balance: ${self.balance}.")
        else:
            print("Deposit amount must be positive.")

    def withdraw(self, amount):
        if 0 < amount <= self.balance:
            self.balance -= amount
            print(f"Successfully withdrew ${amount}. New balance: ${self.balance}.")
        else:
            print("Withdrawal amount exceeds balance or is invalid.")

    def get_balance(self):
        return self.balance

    def display_account_info(self):
        print(f"Account Number: {self.account_number}")
        print(f"Account Holder: {self.account_holder}")
        print(f"Current Balance: ${self.balance}")


class BankSystem:
    def __init__(self):
        self.accounts = {}

    def create_account(self, account_number, username, password, account_holder):
        if account_number not in self.accounts:
            if username not in [account.username for account in self.accounts.values()]:
                self.accounts[account_number] = BankAccount(account_number, username, password, account_holder)
                print(f"Account created for {account_holder} with username {username}.")
            else:
                print("Username already exists. Please choose a different username.")
        else:
            print("Account number already exists.")

    def login(self, account_number, password):
        if account_number in self.accounts:
            account = self.accounts[account_number]
            if account.password == password:
                return account
            else:
                print("Incorrect password.")
                return None
        else:
            print("Account not found.")
            return None


def main():
    bank_system = BankSystem()

    while True:
        print("\nWelcome to the Banking System!")
        print("1. Login to an existing account")
        print("2. Create a new account")
        choice = input("Choose an option: ")

        if choice == '1':
            account_number = input("Enter your account number: ")
            password = input("Enter your password: ")
            account = bank_system.login(account_number, password)

            if account:
                while True:
                    print("\n1. Deposit\n2. Withdraw\n3. Check Balance\n4. Exit")
                    option = input("Choose an option: ")

                    if option == '1':
                        amount = float(input("Enter amount to deposit: "))
                        account.deposit(amount)
                    elif option == '2':
                        amount = float(input("Enter amount to withdraw: "))
                        account.withdraw(amount)
                    elif option == '3':
                        print(f"Current balance: ${account.get_balance()}")
                    elif option == '4':
                        break
                    else:
                        print("Invalid option.")

        elif choice == '2':
            account_number = input("Enter a new account number: ")
            username = input("Choose a username: ")
            password = input("Choose a password: ")
            account_holder = input("Enter your name: ")
            bank_system.create_account(account_number, username, password, account_holder)

        else:
            print("Invalid option.")

        cont = input("Do you want to continue? (yes/no): ")
        if cont.lower() != 'yes':
            break


if __name__ == "__main__":
    main()
