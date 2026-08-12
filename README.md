# -isat-subtask2-
/*
Name: Liyema
Surname: Gobodwana
12.08.2026
Purpose: calculate decimal to binary
*/

#include <iostream>
#include <string>
#include <algorithm>
#include <sstream>
#include <iomanip>

using namespace std;

// Function to validate if a string matches the required number system base
bool isValidInput(const string& input, int base) {
    if (input.empty()) return false;

    // Check characters based on the base
    for (char c : input) {
        if (base == 2) {
            if (c != '0' && c != '1') return false;
        }
        else if (base == 10) {
            if (c < '0' || c > '9') return false;
        }
        else if (base == 16) {
            if (!((c >= '0' && c <= '9') || (c >= 'A' && c <= 'F') || (c >= 'a' && c <= 'f'))) {
                return false;
            }
        }
    }
    return true;
}

// Function to handle Decimal to Binary conversion
void decimalToBinary() {
    cout << "\n--- Decimal to Binary ---\n";
    string input;

    while (true) {
        cout << "Enter a positive decimal number: ";
        cin >> input;
        if (isValidInput(input, 10)) break;
        cout << "❌ Invalid format. Expected Decimal (0-9).\n";
    }

    unsigned long long decimal = stoull(input);
    if (decimal == 0) {
        cout << " Decimal 0 = Binary 0\n";
        return;
    }

    string binary = "";
    unsigned long long temp = decimal;
    while (temp > 0) {
        binary = (temp % 2 == 0 ? "0" : "1") + binary;
        temp /= 2;
    }

    cout << " Decimal " << decimal << " = Binary " << binary << "\n";
}

// Function to handle Binary to Decimal conversion
void binaryToDecimal() {
    cout << "\n--- Binary to Decimal ---\n";
    string binary;

    while (true) {
        cout << "Enter a binary number: ";
        cin >> binary;
        if (isValidInput(binary, 2)) break;
        cout << " Invalid format. Expected Binary (0-1).\n";
    }

    unsigned long long decimal = stoull(binary, nullptr, 2);
    cout << " Binary " << binary << " = Decimal " << decimal << "\n";
}

// Function to handle Decimal to Hexadecimal conversion
void decimalToHexadecimal() {
    cout << "\n--- Decimal to Hexadecimal ---\n";
    string input;

    while (true) {
        cout << "Enter a positive decimal number: ";
        cin >> input;
        if (isValidInput(input, 10)) break;
        cout << " Invalid format. Expected Decimal (0-9).\n";
    }

    unsigned long long decimal = stoull(input);

    stringstream ss;
    ss << hex << uppercase << decimal;
    string hexResult = ss.str();

    cout << " Decimal " << decimal << " = Hexadecimal " << hexResult << "\n";
}

// Function to handle Hexadecimal to Decimal conversion
void hexadecimalToDecimal() {
    cout << "\n--- Hexadecimal to Decimal ---\n";
    string hexStr;

    while (true) {
        cout << "Enter a hexadecimal number: ";
        cin >> hexStr;
        if (isValidInput(hexStr, 16)) break;
        cout << " Invalid format. Expected Hexadecimal (0-9, A-F).\n";
    }

    unsigned long long decimal = stoull(hexStr, nullptr, 16);

    transform(hexStr.begin(), hexStr.end(), hexStr.begin(), ::toupper);
    cout << " Hexadecimal " << hexStr << " = Decimal " << decimal << "\n";
}

// Demo Mode: Shows the step-by-step mathematical conversion process of Decimal to Binary
void runDemoMode() {
    cout << "\n---  DEMO MODE: Integer to Binary Step-by-Step ---\n";
    string input;

    while (true) {
        cout << "Enter an integer to see the math breakdown: ";
        cin >> input;
        if (isValidInput(input, 10)) break;
        cout << " Invalid format. Expected Decimal Integer (0-9).\n";
    }

    unsigned long long originalNum = stoull(input);
    unsigned long long temp = originalNum;
    string binaryResult = "";

    if (temp == 0) {
        cout << "0 / 2 = 0 with a remainder of 0\n";
        binaryResult = "0";
    }
    else {
        cout << "\nCalculation Steps (Divide by 2 and track the remainder):\n";
        cout << "--------------------------------------------------------\n";

        // Loop tracks the division steps and collects remainders
        while (temp > 0) {
            unsigned long long remainder = temp % 2;
            cout << temp << " / 2 = " << (temp / 2) << " | Remainder = " << remainder << "\n";
            binaryResult = to_string(remainder) + binaryResult;
            temp /= 2;
        }
    }

    cout << "--------------------------------------------------------\n";
    cout << "Read the remainders from bottom to top to get the result.\n";
    cout << " DEMO RESULT: Decimal " << originalNum << " = Binary " << binaryResult << "\n";
}

int main() {
    int choice;

    while (true) {
        cout << "\n========================================\n";
        cout << "       NUMBER CONVERTER APPLICATION     \n";
        cout << "========================================\n";
        cout << "1. Decimal to Binary\n";
        cout << "2. Binary to Decimal\n";
        cout << "3. Decimal to Hexadecimal\n";
        cout << "4. Hexadecimal to Decimal\n";
        cout << "5. Run Demo Mode (Integer to Binary Math)\n";
        cout << "6. Exit\n";
        cout << "========================================\n";
        cout << "Enter your choice (1-6): ";

        if (!(cin >> choice)) {
            cout << " Invalid choice! Please enter a number.\n";
            cin.clear();
            cin.ignore(10000, '\n');
            continue;
        }

        switch (choice) {
        case 1:
            decimalToBinary();
            break;
        case 2:
            binaryToDecimal();
            break;
        case 3:
            decimalToHexadecimal();
            break;
        case 4:
            hexadecimalToDecimal();
            break;
        case 5:
            runDemoMode();
            break;
        case 6:
            cout << "\nThank you for using the Number Converter application. Goodbye! \n";
            return 0;
        default:
            cout << " Invalid choice! Please select an option from 1 to 6.\n";
        }
    }
    return 0;
}


