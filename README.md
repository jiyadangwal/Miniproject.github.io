# Miniproject.github.io
The Tiffin Service Management System is a simple console-based mini project developed using C++. This project helps in managing customer details, food orders, billing, and delivery records in an organized way. It uses basic C++ concepts such as classes, objects, functions, loops, and file handling.

#include <iostream>
#include <fstream>
#include <vector>
#include <string>
using namespace std;
class Customer 
{
public:
    int id;
    string name;
    string phone;
    string address;
    string plan;
    string menu;
    int presentDays;
};
class Feedback {
public:
    int customerId;
    string message;
};
class Menu {
public:
    string type;
    vector<string> items;
};
vector<Customer> customers;
vector<Feedback> feedbacks;
vector<Menu> menus;
int calculateBill(Customer c) {
        if (c.plan == "Daily" || c.plan == "daily")
        return c.presentDays * 60;
        if (c.plan == "Weekly" || c.plan == "weekly")
        return (700 / 7) * c.presentDays;
        if (c.plan == "Monthly" || c.plan == "monthly")
        return (2500 / 30) * c.presentDays;
         return 0;
}
void addCustomer() 
{
    Customer c;
    c.presentDays = 0;
    cout << "\nEnter ID: ";
    cin >> c.id;
    cin.ignore();
    cout << "Enter Name: ";
    getline(cin, c.name);
    cout << "Enter Phone: ";
    getline(cin, c.phone);
    cout << "Enter Address: ";
    getline(cin, c.address);
    cout << "Enter Plan (Daily/Weekly/Monthly): ";
    getline(cin, c.plan);
    cout << "Enter Menu (Veg/Non-Veg/Jain): ";
    getline(cin, c.menu);
    customers.push_back(c);
    cout << "Customer Added Successfully!\n";
}
void viewCustomers() 
{
        cout << "\n----- CUSTOMER LIST -----\n";
     for (int i = 0; i < (int)customers.size(); i++) 
{
        cout << "ID: " << customers[i].id << endl;
        cout << "Name: " << customers[i].name << endl;
        cout << "Plan: " << customers[i].plan << endl;
        cout << "Menu: " << customers[i].menu << endl;
        cout << "Present Days: " << customers[i].presentDays << endl;
        cout << "-------------------------\n";
    }
}
void markAttendance() 
{
     int id;
    cout << "\nEnter Customer ID: ";
    cin >> id;
     for (int i = 0; i < (int)customers.size(); i++) {
         if (customers[i].id == id)
 {
            char ch;
            cout << "Is customer present today? (y/n): ";
            cin >> ch;
            if (ch == 'y' || ch == 'Y') 
{
             customers[i].presentDays++;
             cout << "Attendance Marked!\n";
            }
            else 
{
cout << "Marked Absent\n";
            }
 return;
        }
    }
cout << "Customer Not Found!\n";
}
void generateBill()
 {
    int id;
            cout << "\nEnter Customer ID: ";
    cin >> id;
for (int i = 0; i < (int)customers.size(); i++) 
{
 if (customers[i].id == id) 
{
Customer c = customers[i];
int amount = calculateBill(c);
cout << "\n----- FINAL BILL -----\n";
            cout << "Name: " << c.name << endl;
            cout << "Plan: " << c.plan << endl;
            cout << "Menu: " << c.menu << endl;
            cout << "Present Days: " << c.presentDays << endl;
            cout << "Total Amount: Rs " << amount << endl;
 	ofstream file("bills.txt", ios::app);
file << c.id << " "
             << c.name << " "
             << c.presentDays << " "
             << amount << endl;
 file.close();
 return;
        }
    }
cout << "Customer Not Found!\n";
}
void addMenu()
 {
 Menu m;
 int n;
 cout << "\nEnter Menu Type (Veg/Non-Veg/Jain): ";
   	 cin >> m.type;
cout << "How many items: ";
    	cin >> n;
cin.ignore();
for (int i = 0; i < n; i++) 
{
string item;
cout << "Enter item " << i + 1 << ": ";
getline(cin, item);
m.items.push_back(item);
    }
menus.push_back(m);
cout << "Menu Added Successfully!\n";
}
void viewMenu() 
{
cout << "\n----- MENU LIST -----\n";
for (int i = 0; i < (int)menus.size(); i++) {
cout << "\n" << menus[i].type << " Menu:\n";
for (int j = 0; j < (int)menus[i].items.size(); j++) {
cout << "- " << menus[i].items[j] << endl;
        }
    }
}
void addFeedback()
 {
Feedback f;
 cout << "\nEnter Customer ID: ";
cin >> f.customerId;
cin.ignore();
cout << "Enter Feedback: ";
getline(cin, f.message);
feedbacks.push_back(f);
cout << "Feedback Saved!\n";
}
void viewFeedback()
 {
cout << "\n----- FEEDBACK -----\n";
for (int i = 0; i < (int)feedbacks.size(); i++)
{
cout << "Customer ID: " << feedbacks[i].customerId << endl;
cout << "Message: " << feedbacks[i].message << endl;
cout << "--------------------\n";
    }
}
int main()
 {
int choice;
 do
 {
cout << "\n===== TIFFIN SERVICE MANAGEMENT SYSTEM =====\n";
cout << "1. Add Customer\n";
cout << "2. View Customers\n";
cout << "3. Mark Attendance\n";
cout << "4. Generate Bill\n";
cout << "5. Add Menu\n";
cout << "6. View Menu\n";
cout << "7. Add Feedback\n";
cout << "8. View Feedback\n";
cout << "0. Exit\n";
cout << "Enter Choice: ";
cin >> choice;
switch (choice) 
{
case 1:
            addCustomer();
            break;
case 2:
            viewCustomers();
            break;
case 3:
            markAttendance();
            break;
case 4:
            generateBill();
            break;
case 5:
            addMenu();
            break;
case 6:
            viewMenu();
            break;
case 7:
            addFeedback();
            break;
case 8:
            viewFeedback();
            break;
case 0:
            cout << "Thank You!\n";
break;
default:
            cout << "Invalid Choice!\n";
        }
 } 
while (choice != 0);
return 0;
}