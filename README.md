# Banking_System
#include <iostream>
#include <fstream>
#include <stdio.h>
#include <cstdio>
#include <filesystem>

using namespace std;

void createAccount(){
    int ID = 0;
    string filename = to_string(ID);
    ifstream file;
    file.open(filename + ".txt");
    for(int i = 1; i < 10000; i = i + 1){
        file.close();
        filename = to_string(i);
        ID = i;
        file.open(filename + ".txt");
        if(!file){
            break;
        }
    }
    file.close();
    ofstream createFile;
    createFile.open(filename + ".txt",ios:: out);
    string name,surname,initialBalance;
    cout << "Enter Name: "; cin >> name; cout << endl;
    cout << "Enter Surname: "; cin >> surname; cout << endl;
    cout << "Enter Initial Amount Of Balance: "; cin >> initialBalance; cout << endl;
    createFile << "Name: " + name << endl;
    createFile << "Surname: " + surname << endl;
    createFile << "Balance: " + initialBalance << endl;
    createFile.close();
    cout << "Bank Account ID: " + filename << endl;
}
void balance(){
    string filename;
    cout << "Enter ID: "; cin >> filename; cout << endl;
    ifstream file;
    file.open(filename + ".txt");
    if(!file){
        cout << "Account doesn't exist" << endl;
    }
    else{
        char myChar;
        while(file){
            myChar = file.get();
            cout << myChar;
        }
    }
    file.close();
}
void deposit(int data){
    int ID;
    cout << "Enter ID: "; cin >> ID; cout << endl;
    int balance;
    if(data == 1){
        cout << "Enter amount of deposit: "; cin >> balance; cout << endl;
    }
    else{
        cout << "Enter amount of withdrawal: "; cin >> balance; cout << endl;
        balance *= -1;
    }
    ifstream file;
    string id = to_string(ID);
    file.open(id + ".txt");
    if(!file){
        cout << "Account doesn't exist" << endl;
    }
    else{
        ofstream File;
        File.open("Temp.txt",ios:: out);
        string s;
        bool check = false;
        int i = 1;
        while(file >> s){
            //cout << s << endl;
            if(s == "Balance:"){
                check = true;
                //cout << s << endl;
                File << s + " ";
            }
            else if(check == true){
                check = false;
                int sum = balance + stoi(s);
                string d = to_string(sum);
                File << d << endl;
                //cout << d << endl;
            }
            else{
                if(i %2 == 1){
                    File << s + " ";
                }else{
                    File << s << endl;
                }
                i = i + 1;
            }
        }
        file.close();
        ofstream F(id + ".txt");
        F.close();
        F.open(id + ".txt",ios::out);
        File.close();
        ifstream f;
        f.open("Temp.txt");
        string l;
        int j = 1;
        while(f >> l){
            if(j % 2 == 1){
                F << l + " ";
            }
            else{
                F << l << endl;
            }
            j = j + 1;
        }
        F.close();
        f.close();
        ofstream G("Temp.txt");
        G.close();
    }
}
void removeData(){
    cout << "Enter ID: " << endl;
    string ID;
    cin >> ID;
    ofstream file(ID + ".txt");
    //file >> ID;
    //cout << ID;
    file.close();
    file.open(ID + ".txt",ios::out);
    file << "Account is closed" << endl;
    file.close();
    cout << "Closed successfully" << endl;
}
int main(){
    cout << "Select option (1-6): " << endl;
    cout << "(1) Create an account" << endl;
    cout << "(2) Balance Enquiry" << endl;
    cout << "(3) Deposit" << endl;
    cout << "(4) Withdrawal" << endl;
    cout << "(5) Close an account" << endl;
    cout << "(6) Exit" << endl;
    int x;
    cin >> x;
    if(x == 1){
        createAccount();
        main();
    }
    else if(x == 2){
        balance();
        main();
    }
    else if(x == 3){
        deposit(1);
        main();
    }
    else if(x == 4){
        deposit(-1);
        main();
    }
    else if(x == 5){
        removeData();
        main();
    }
    else if(x == 6){
        return 0;
    }
    return 0;
}
