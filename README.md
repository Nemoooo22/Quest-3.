#include <iostream>
#include <string>
using namespace std;

class CaesarCipher {
private:
    int shiftValue; // keeps shift key private

protected:
    string encode(const string& message) {
        string result = "";
        for (char c : message) {
            if (isalpha(c)) {
                char base = isupper(c) ? 'A' : 'a';
                c = (c - base + shiftValue) % 26 + base;
            }
            result += c;
        }
        return result;
    }

public:
    void setShiftValue(int value) {
        if (value >= 1 && value <= 13)
            shiftValue = value;
        else
            shiftValue = 1; // assumes shift is 1 if value > 13
    }

    // Encrypt message using the  shift
    string encryptMessage(const string& message) {
        return encode(message);
    }

    
    CaesarCipher(int value = 1) {
        setShiftValue(value);
    }
};


class Rot13Cipher : public CaesarCipher {
public:
    // Rot13Cipher always has a shift of 13
    Rot13Cipher() : CaesarCipher(13) {
        // Calls the base class constructor with shift = 13
    }

    string rot13(const string& message) {
        return encryptMessage(message);
    }
};

int main() {
    CaesarCipher cipher;
    string message;
    int shift;

    cout << "Enter a message: ";
    getline(cin, message);

    cout << "Enter a shift (1-13): ";
    cin >> shift;

    cipher.setShiftValue(shift);
    string encoded = cipher.encryptMessage(message);

    cout << "Encoded message (Caesar Cipher): " << encoded << endl;

     //Rot13Cipher class
    Rot13Cipher rot13;
    string rotEncoded = rot13.rot13(message);
    cout << "Encoded message (ROT13 Cipher): " << rotEncoded << endl;

    return 0;
}
