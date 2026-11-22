# Bank-Management-Application
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

class BankAccount {
private:
    int accountNumber;
    string name;
    double balance;

public:
    void createAccount() {
        cin >> accountNumber;
        cin.ignore();
        getline(cin, name);
        cin >> balance;

        ofstream file("accounts.txt", ios::app);
        file << accountNumber << " "
             << name << " "
             << balance << endl;
        file.close();
    }

    void displayBalance(int accNo) {
        ifstream file("accounts.txt");

        int acc;
        string customerName;
        double bal;

        while (file >> acc >> customerName >> bal) {
            if (acc == accNo) {
                cout << customerName << endl;
                cout << bal << endl;
                return;
            }
        }

        cout << "Account Not Found";
        file.close();
    }
};

int main() {
    BankAccount account;
    int choice, accNo;

    do {
        cin >> choice;

        switch (choice) {
            case 1:
                account.createAccount();
                break;

            case 2:
                cin >> accNo;
                account.displayBalance(accNo);
                break;
        }
    } while (choice != 3);

    return 0;
}
