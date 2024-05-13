#include<iostream>
#include <fstream>
#include <windows.h>
#include <sstream>
#include <stack> 
#include <vector>
#include <map>
#include <ctime>
#include <queue>
#include <windows.h>
#include <conio.h>
#include <string>

using namespace std;
/*-------------------------------USER.h---------------------*/
map<string, pair<int, string>>shortPath;
map<string, vector<string>> metroMap;
class Ride {
public:

    string startStation;
    string endStation;
    string username;
    string date;
    Ride() {

    }
    Ride(string start, string end, string Date) {
        startStation = start;
        endStation = end;
        date = Date;
    }
    Ride(string start, string end, string Date, string user) {
        username = user;
        startStation = start;
        endStation = end;
        date = Date;
    }
};
void insertData(string firstData, string secondData)
{
    metroMap[firstData].push_back(secondData);
    metroMap[secondData].push_back(firstData);
}

int numberOfStations(string start, string end)
{
    queue<string>level;
    shortPath[start].first = 0;
    shortPath[start].second = "none";
    level.push(start);
    while (!level.empty())
    {
        string front = level.front();
        level.pop();
        for (string child : metroMap[front])
        {
            if (shortPath.count(child) == 0)
            {
                level.push(child);
                shortPath[child].first = shortPath[front].first + 1;
                shortPath[child].second = front;
            }
        }
    }
    return shortPath[end].first;
}


string displayPath(string end) {
    // The Parent of station 
    string parent = shortPath[end].second;
    // if the parent = none , so this is the start station 
    if (shortPath[end].second == "none") {
        return end;
    }
    // insert this station
    string path = displayPath(parent);
    return path + " -> " + end;
}
void setColor(int x, int y)
{
    HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);
    if (x == y) {
        SetConsoleTextAttribute(hConsole, FOREGROUND_BLUE | FOREGROUND_INTENSITY);
    }
    else {
        SetConsoleTextAttribute(hConsole, FOREGROUND_RED | FOREGROUND_GREEN | FOREGROUND_BLUE);
    }
}

// display menu 
string display(vector<string>items) {

    int size = items.size();

    int selectIndex = 0;

    do {

        for (int i = 0; i < size; i++) {
            setColor(i, selectIndex);
            cout << items[i] << endl;
        }
        Sleep(100);
        // get input key
        char key = _getch();
        // check 
        switch (key) {
        case 72:  // Up arrow key -> incerement selectIndex if not qrual zero 
            selectIndex = (selectIndex == 0) ? size - 1 : --selectIndex;
            break;
        case 80:  // Down arrow key -> decerement selectIndex if not qrual zero 
            selectIndex = (selectIndex == size - 1) ? 0 : ++selectIndex;
            break;
        case 13:  // Enter key -> return the select item
            return items[selectIndex];
        }

        system("cls");
    } while (true);
}
void displayVector(std::vector<std::string> line) {
    for (string value : line) {
        std::cout << value << " " << endl;
    }
}

void AllPaths(string start, string end, vector<string>& path, map<string, bool>& visited) {
    visited[start] = true;
    path.push_back(start);

    if (start == end) {
        for (const auto& station : path) {
            cout << station << " -> ";
        }
        cout << endl;
    }
    else {
        for (const auto& nextStation : metroMap[start]) {
            if (!visited[nextStation]) {
                AllPaths(nextStation, end, path, visited);
            }
        }
    }

    path.pop_back();
    visited[start] = false;
}
void displayAllPaths(string start, string end) {
    map<string, bool> visited;
    vector<string> path;
    AllPaths(start, end, path, visited);
}

class User
{
public:
    string username;
    string password;
    string email;
    string gender;
    double balance;
    string date_of_registration;
    vector<Ride> rideHistory;

public:
    bool operator==(const std::string& otherUsername) const {
        return username == otherUsername;
    }
    User();
    void set_username(string name);
    string get_username();
    void set_password(string pass);
    string get_password();
    void set_email(string email);
    string get_email();
    void set_gender(string gender);
    string get_gender();
    void set_balance(double balance);
    void add_balance(double);
    double get_balance();
    void set_date_of_registration_for_files(string date);
    void set_date_of_registration();
    string get_date_of_registration();
    void registerUser(vector<User>& users, User& user);
    void loginUser(vector<User>& users, User& user);
    void viewRideHistory(const User& user);
    vector<Ride> getRideHistory()const;

};
/*--------------------------USER.cpp------------------------------------------*/
User::User()// : //subscription()//, cash_wallet_card()
{
    username = "Not assigned yet";
    password = "Not assigned yet";
    email = "Not assigned yet";
    gender = "Not assigned yet";
    balance = 0.0;
    date_of_registration = "Not assigned yet";
}

void User::set_username(string name) {
    username = name;
}


string User::get_username()
{
    return username;
}

void User::set_password(string pass) {
    password = pass;
}

string User::get_password() {
    return password;
}

void User::set_email(string em) {
    email = em;
}

string User::get_email() {
    return email;
}

void User::set_gender(string ge) {
    gender = ge;
}

string User::get_gender() {
    return gender;
}

void User::set_balance(double ba) {
    balance = ba;
}

void User::add_balance(double amount) {

    balance += amount;

}

double User::get_balance() {
    return balance;
}
/*void User::set_Subscription(Subscription& sub) {
    subscription = sub;
}*/

/*Subscription User::get_Subscription() {
    return subscription;
}*/


void User::set_date_of_registration() {
    time_t now;
    struct tm current_date;
    char date_buffer[80];
    time(&now);
    localtime_s(&current_date, &now);
    strftime(date_buffer, sizeof(date_buffer), "%d-%m-%Y %H:%M:%S", &current_date);
    date_of_registration = date_buffer;
}
string User::get_date_of_registration() {
    return date_of_registration;
}

void User::registerUser(vector<User>& users, User& user)
{
    for (int i = 0; i < users.size(); i++) {
        cout << users[i].get_username() << endl;
        cout << users[i].get_password() << endl;
        cout << users[i].get_email() << endl;
        cout << users[i].get_gender() << endl;
        // cout << users[i].get_Cash_Wallet_Card() << endl;
        cout << "Balance: " << users[i].get_balance() << endl;
        cout << "Date: " << users[i].get_date_of_registration() << endl;

    }
    string name, pw, email, gender, card;
start1:
    cout << "\tEnter User Name: ";
    cin >> name;
    user.set_username(name);
    for (size_t i = 0; i < users.size(); i++) {
        if (users[i].get_username() == name) {
            cout << "Username already exists. Please choose a different one." << endl;
            goto start1;
        }
        if (i == users.size() - 1) {
            break;
        }
    }

start:
    cout << "\tEnter A Strong Password: ";
    char c;
    while ((c = _getch()) != 13) {
        if (c == '\b') {
            if (!pw.empty()) {
                pw.pop_back();
                cout << "\b \b";
            }
        }
        else {
            pw += c;
            cout << "*";
        }
    }

    if (pw.length() >= 8) {
        user.set_password(pw);
        cout << endl;
    }
    else {
        cout << "\n\tEnter Minimum 8 Characters!\n";
        goto start;
    }


    /*for (size_t i = 0; i < users.size(); i++) {
        if (users[i].get_password()==pw) {
            cout << "Password already in use. Please choose a different one." << endl;
            goto start;
        }
    }*/

    cout << "\tEnter email: ";
    cin >> email;

    bool valid_em = false;
    while (email.length() > 0 && !valid_em) {
        if (email.length() < 10) {
            cout << "Not a valid email. Please try again.\n";
            cin >> email;
            continue;
        }
        string first_em = "@gmail.com";
        string second_em = "@yahoo.com";
        string third_em = "@hotmail.com";
        string fourth_em = "@outlook.com";
        string fifth_em = "@cis.asu.edu.eg";
        if (email.length() >= first_em.length() && email.substr(email.length() - first_em.length()) == first_em) {
            cout << "\tYou have entered a valid email." << endl;
            valid_em = true;
            user.set_email(email);
        }
        if (email.length() >= second_em.length() && email.substr(email.length() - second_em.length()) == second_em) {
            cout << "\tYou have entered a valid email." << endl;
            valid_em = true;
            user.set_email(email);
        }
        if (email.length() >= fourth_em.length() && email.substr(email.length() - fourth_em.length()) == fourth_em) {
            cout << "\tYou have entered a valid email." << endl;
            valid_em = true;
            user.set_email(email);
        }
        if (email.length() >= third_em.length() && email.substr(email.length() - third_em.length()) == third_em) {
            cout << "\tYou have entered a valid email." << endl;
            valid_em = true;
            user.set_email(email);
        }
        if (email.length() >= fifth_em.length() && email.substr(email.length() - fifth_em.length()) == fifth_em) {
            cout << "\tYou have entered a valid email." << endl;
            valid_em = true;
            user.set_email(email);
        }
        if (!valid_em) {
            cout << "Not a valid email. Please try again." << endl;
            cin >> email;
        }
    }
    cout << "\tEnter gender: ";
    cin >> gender;
    user.set_gender(gender);

    time_t now;
    struct tm current_date;
    char date_buffer[80];
    time(&now);
    localtime_s(&current_date, &now);
    strftime(date_buffer, sizeof(date_buffer), "%d-%m-%Y %H:%M:%S", &current_date);
    cout << "\tToday's date: " << date_buffer << endl;

    user.set_date_of_registration();

    users.push_back(user);
    cout << "You registered successfully." << endl;

    ofstream outfile("C:\\Users\\Fady\\Desktop\\DS C++ PROJECT\\test files\\pro3\\Registrations.txt", ios::app);
    outfile << user.get_username() << ":" << user.get_password() << ":" << user.get_email() << ":" << user.get_gender() << ":" << user.get_balance() << ":" << user.get_date_of_registration() << endl;

    outfile.close();

}


void User::loginUser(vector<User>& users, User& user)
{

    string username, pw;
start:
    cout << "\tEnter Your Username: ";
    cin >> username;
    cout << "\tEnter Password: ";
    pw = "";
    char c;
    bool founded = false;
    while ((c = _getch()) != 13) {
        if (c == '\b') {
            if (!pw.empty()) {
                pw.pop_back();
                cout << "\b \b";
            }
        }
        else {
            pw += c;
            cout << "*";
        }
    }
    for (size_t i = 0; i < users.size(); ++i)
    {
        if (users[i].get_username() == username && users[i].get_password() == pw) {
            user = users[i];
            founded = true;
            cout << "\tLogin successful. Welcome, " << username << "!" << endl;
        }
    }
    if (founded == false) {

        cout << "\tInvalid username or password. Try again! " << endl;
        goto start;
    }


    // return false;
}
vector<Ride> User::getRideHistory() const {
    return rideHistory;
}

void User::viewRideHistory(const User& user) {
    vector<Ride> rideHistory = user.getRideHistory();
    for (const auto& entry : rideHistory) {
        cout << "Date: " << entry.date << " Start Station: " << entry.startStation << " Destination: " << entry.endStation << "\n\n";

    }
}
/*---------------------------------------SUBSCRIPTION.h---------------------------------*/
class Admin {
public:
    string username;
    string pass;
    vector<Ride> allRideLogs;
public:
    Admin() {
    }

    void addToRideLogs(const Ride& ride) {
        allRideLogs.push_back(ride);
    }
    void viewAllRideLogs()const {
        cout << "All Ride Logs:" << std::endl;
        if (allRideLogs.empty()) {
            cout << "No ride logs available." << std::endl;
        }
        else {
            for (const auto& ride : allRideLogs) {
                cout << "Username: " << ride.username << "Date: " << ride.date << ", Start Station: " << ride.startStation
                    << ", Destination Station: " << ride.endStation << endl;
            }
        }
    }
    string chooseLine() {
        vector<string> lines = { "Line1", "Line2", "Line3" };
        cout << "Choose a line to add a station to:" << endl;
        string lineName = display(lines);
        return lineName;

    }
    
    std::vector<std::string> addStation(vector<string> line1, std::vector<std::string> line2, std::vector<std::string> line3, string  lineName) {
        vector<string>& lineStations = (lineName == "Line1") ? line1 :
            (lineName == "Line2") ? line2 :
            (lineName == "Line3") ? line3 : line1;

        while (true) {


            cout << "Enter the name of the new station:" << endl;
            string newStation;
            cin >> newStation;

            auto found = find(lineStations.begin(), lineStations.end(), newStation);
            if (found != lineStations.end()) {
                cout << "The station '" << newStation << "' already exists in the line." << endl;
                cout << "Do you want to try again? [y/n]";
                char choice1;
                cin >> choice1;
                if (choice1 == 'n' || choice1 == 'N') {
                    break;
                }
                if (choice1 == 'y' || choice1 == 'Y') {
                    continue;
                }
            }



            cout << "Current stations in " << lineName << ":" << endl;


            cout << "Choose a station to place the new station before or after:" << endl;
            string chosenStation = display(lineStations);
            while (true) {
                cout << "Do you want to place the new station before or after '" << chosenStation << "?" << endl;
                cout << "Press 'b' for before and 'a' for after." << endl;
                char choice;
                cin >> choice;
                choice = tolower(choice);

                auto it = find(lineStations.begin(), lineStations.end(), chosenStation);

                if (choice == 'b' || choice == 'B') {
                    lineStations.insert(it, newStation);
                    break;
                }
                else if (choice == 'a' || choice == 'A') {
                    lineStations.insert(it + 1, newStation);
                    break;
                }
                else {
                    cout << "Invalid choice. The station was not added." << endl;
                    continue;
                }
            }
            cout << "Updated stations in " << lineName << ":" << endl;

            if (lineName == "Line1") {
                line1 = lineStations;
                displayVector(line1);
                return line1;

            }
            else if (lineName == "Line2") {
                line2 = lineStations;
                displayVector(line2);
                return line2;


            }
            if (lineName == "Line3") {
                line3 = lineStations;
                displayVector(line3);
                return line3;


            }




        }

    }
  /* 
  void createSubscription(vector<User>& users, User& user, map<string, Subscription>& subscriptions)
    {


    start:
        cout << "Enter username for user \n";
        string usersnamee;
        bool founded = false;
        cin >> usersnamee;
        for (size_t i = 0; i < users.size(); ++i)
        {
            if (users[i].get_username() == usersnamee) {
                user = users[i];
                founded = true;
                cout << "\tLogin successful. Welcome, " << usersnamee << "!" << endl;
                break;
            }
        }
        if (founded == false) {

            cout << "\t This email not found, Try again! " << endl;
            goto start;
        }



        for (size_t index = 0; index < users.size(); index++)
        {
            if (users[index].get_username() == user.get_username())
            {
                Subscription sub;
                sub.username = users[index].get_username();
                sub.userEmail = users[index].get_email();
                sub.set_subsicription_date();
                sub.purchaseSubscription();
            start5:
                cout << "\t 1. Student Card\n";
                cout << "\t 2. Public Card \n";
                cout << "\t 3. Cash Wallet Card\n";
                cout << "\t 4. Back\n";
                cout << "\t Please choose an option: ";
                int ch;
                cin >> ch;
                if (ch == 1 || ch == 2)
                {
                    if (ch == 1) {
                        sub.Student_Card();
                        sub.Student_Card_info();
                        sub.set_type("Student Card");
                        cout << "\t Please choose The stage (1 - 2 - 3 - 4) : ";
                        int st;
                        cin >> st;
                        sub.set_stage(st);
                        sub.get_Subscription_cost();

                    }
                    else if (ch == 2) {
                        sub.Public_card_info();
                        sub.set_type("Public Card");
                        cout << "\t 1. Yearly Subscription\n";
                        cout << "\t 2. Monthly Subscription\n";
                        cout << "\t Please choose an option: ";
                        int choice;
                        cin >> choice;
                        if (choice == 1) { sub.Yearly_Subscription(); }
                        else if (choice == 2) { sub.Monthly_Subscription(); }
                        cout << "\t Please choose The stage (1 - 2 - 3 - 4) : ";
                        int stage;
                        cin >> stage;
                        sub.set_stage(stage);
                        sub.get_Subscription_cost();

                    }

                start1:
                    cout << "\t Confirm Your Subscription ? \n";
                    cout << "\t 1.Confirm \n";
                    cout << "\t 2.Cancel\n";
                    cout << "\t Enter Choice: ";
                    cin >> ch;
                    if (ch == 1) {
                        bool valied = sub.Subscription_confermation(users[index]);
                        if (valied == false) {
                            cout << "\t Would you like to add money to your wallet? \n";
                            cout << "\t 1. Add\n";
                            cout << "\t 2. Cancel\n";
                            cout << "\t Enter a choice : ";
                            int choice;
                            cin >> choice;
                            if (choice == 1) {
                                cout << "\t Enter amount of money that u want to add to yr wallet : ";
                                double money;
                                cin >> money;
                                users[index].add_balance(money);
                                cout << "\t Money added Successfully!!\n";
                                cout << "\t Your Currant Balance : " << users[index].get_balance() << endl;
                                goto start1;
                            }
                            else {
                                goto start1;
                            }

                        }
                        else if (valied == true) {
                            subscriptions.insert(make_pair(sub.username, sub));//pro3
                            ofstream outfile("C:\\Users\\Fady\\Desktop\\DS C++ PROJECT\\test files\\pro3\\Subscribtions.txt", ios::app);
                            //Ticket file data : name // email // type // yearly // Monthly // Stage // cost // date
                            outfile << "\t" << sub.username << " : " << sub.userEmail << " : " << sub.get_type() << " : " << sub.get_Yearly_Subscription() << " : " << sub.get_Monthly_Subscription() << ":" << sub.get_stage() << " : " << sub.cost << " : " << sub.get_subscribtion_date() << endl;
                            outfile.close();
                            int back;
                            do {
                                cout << "\t Press 1 to return to Home Page : ";
                                cin >> back;
                            } while (back != 1);
                        }

                    }
                    else if (ch == 2)
                    {
                        goto start5;
                    }
                }
            }

        }
    }
    /*
   // (map<string, Subscription>& subscriptions)
    void modifySubscription(map<string, Subscription>& subscriptions) {
      start:
         cout << "Enter username for user \n";
         string usersnamee;
         bool founded = false;
         cin >> usersnamee;
         for (size_t i = 0; i < users.size(); ++i)
         {
             if (users[i].get_username() == usersnamee) {
                 user = users[i];
                 founded = true;
                 cout << "\tLogin successful. Welcome, " << usersnamee << "!" << endl;
                 break;
             }
         }
         if (founded == false) {
             cout << "\t This email not found, Try again! " << endl;
             goto start;
         }
     }
   
    void removeSubscription(vector<User>& users, User& user, map<string, Subscription>& subscriptions) {
    start:
        cout << "Enter username for user \n";
        string usersnamee;
        bool founded = false;
        cin >> usersnamee;
        for (size_t i = 0; i < users.size(); ++i)
        {
            if (users[i].get_username() == usersnamee) {
                user = users[i];
                founded = true;
                cout << "\tLogin successful. Welcome, " << usersnamee << "!" << endl;
                break;
            }
        }
        if (founded == false) {

            cout << "\t This email not found, Try again! " << endl;
            goto start;
        }




        Subscription sub;
        for (size_t i = 0; i < users.size(); ++i) {
            if (users[i].get_username() == user.get_username()) {
                subscriptions.erase(users[i].get_username());
                //   sub.set_type("Not assigned yet");
                break;
            }
        }

    }
    */
    std::vector<std::string>  removeStation(std::vector<std::string> line1, std::vector<std::string> line2, std::vector<std::string> line3, string  lineName) {


        vector<string>& lineStations = (lineName == "Line1") ? line1 :
            (lineName == "Line2") ? line2 :
            (lineName == "Line3") ? line3 : line1;
        cout << "Choose the station you want remove:" << endl;
        string chosenStation = display(lineStations);
        auto it = find(lineStations.begin(), lineStations.end(), chosenStation);
        lineStations.erase(it);
        cout << "Updated stations in " << lineName << ":" << endl;

        if (lineName == "Line1") {
            line1 = lineStations;
            displayVector(line1);
            return line1;
        }
        else if (lineName == "Line2") {
            line2 = lineStations;
            displayVector(line2);
            return line2;
        }
        if (lineName == "Line3") {
            line3 = lineStations;
            displayVector(line3);
            return line3;
        }



    }
    std::vector<std::string> editStation(std::vector<std::string> line1, std::vector<std::string> line2, std::vector<std::string> line3, string  lineName) {
        vector<string>& lineStations = (lineName == "Line1") ? line1 :
            (lineName == "Line2") ? line2 :
            (lineName == "Line3") ? line3 : line1;
        std::cout << "Choose the station you want to rename" << endl;
        string chosenStation = display(lineStations);
        string newStation;
        std::cout << "Enter the new station name: " << endl;
        cin >> newStation;
        auto it = find(lineStations.begin(), lineStations.end(), chosenStation);
        *it = newStation;
        cout << "Updated stations in " << lineName << ":" << endl;

        if (lineName == "Line1") {
            line1 = lineStations;
            displayVector(line1);
            return line1;
        }
        else if (lineName == "Line2") {
            line2 = lineStations;
            displayVector(line2);
            return line2;
        }
        if (lineName == "Line3") {
            line3 = lineStations;
            displayVector(line3);
            return line3;
        }

    }

    void view_acc(vector<User>& users) {
        for (User value : users) {
            std::cout << "User's name: " << value.username << endl;
            std::cout << "User's gender: " << value.gender << endl;
            std::cout << "User's date of registration: " << value.date_of_registration << endl;
            std::cout << "User's email: " << value.email << endl;
            std::cout << "User's balance: " << value.balance << endl;
            std::cout << "---------------------------" << endl;
        }

    }
    string select_acc(vector<User>& users) {
        int size = users.size();

        int selectIndex = 0;
        do {
            // pprint items
            for (int i = 0; i < size; i++) {

                setColor(i, selectIndex);
                std::cout << users[i].username << endl;
            }
            Sleep(100);

            char key = _getch();

            switch (key) {
            case 72:
                selectIndex = (selectIndex == 0) ? size - 1 : --selectIndex;
                break;
            case 80:
                selectIndex = (selectIndex == size - 1) ? 0 : ++selectIndex;
                break;
            case 13:
                return users[selectIndex].username;
            }

            system("cls");
        } while (true);
    }
    vector<User> remove_acc(vector<User> users) {
        std::cout << "Choose the account you want remove:" << endl;
        string username = select_acc(users);
        auto it = find(users.begin(), users.end(), username);
        users.erase(it);
        view_acc(users);
        return users;


    }
    vector <User> edit_acc(vector<User>& users) {
        std::cout << "Choose the account you want edit:" << endl;
        string username = select_acc(users);
        auto it = find(users.begin(), users.end(), username);

        std::cout << "User's name: " << it->username << endl;
        std::cout << "User's gender: " << it->gender << endl;
        std::cout << "User's date of registration: " << it->date_of_registration << endl;
        std::cout << "User's email address: " << it->email << endl;
        std::cout << "User's balance: " << it->balance << endl;
        vector<string> options = { "Name","Password","Email" };
        string choice = display(options);
        if (choice == "Name") {
            string newname;
            bool found;
            do {
                found = false;
                std::cout << "Please enter the new Name: " << endl;
                cin >> newname;
                for (User user : users) {
                    if (newname == user.username) {
                        std::cout << "Username already exists!" << endl;
                        found = true;
                        break;

                    }


                }
            } while (found);
            it->username = newname;

        }
        else if (choice == "Password") {
            string newpass, verify;

            while (true) {
                std::cout << "Please enter the your curent password: " << endl;
                std::cin >> verify;
                if (it->password != verify) {
                    std::cout << "Password incorrect!" << endl;
                }
                else {
                    while (true) {
                        std::cout << "Please enter the new password: " << endl;
                        std::cin >> newpass;
                        if (newpass.length() >= 8) {
                            it->password;
                            break;
                        }
                        else {
                            std::cout << "Password must be 8 characters or more!" << endl;;
                        }
                    }
                    break;
                }
            }
        }
        else if (choice == "Email") {
            string newmail;
            bool valid = false;
            string emails[5] = { "@gmail.com" ,"@yahoo.com" ,"@hotmail.com" ,"@outlook.com" ,"@cis.asu.edu.eg" };

            while (!valid) {
                std::cout << "Please enter the new email address: " << std::endl;
                std::cin >> newmail;

                for (int i = 0; i < 5; i++) {
                    if (newmail.length() >= emails[i].length() &&
                        newmail.substr(newmail.length() - emails[i].length()) == emails[i]) {
                        it->email = newmail;
                        valid = true;
                        break;
                    }
                }

                if (!valid) {
                    std::cout << "Email not valid! Please try again." << std::endl;
                }
            }
        }

        return users;

    }


};
class Subscription
{
public:
    string date;
    string date2;
    string type;
    int stage;
    bool yearly;
    bool monthly;
    double cost;
    string username;
    string userEmail;
    int number_trips;

public:
    Subscription();
    void set_type(string);
    string get_type();
    void set_stage(int);
    int get_stage();
    void get_Subscription_cost();
    void Yearly_Subscription();
    void Monthly_Subscription();
    bool get_Monthly_Subscription();
    bool get_Yearly_Subscription();
    void set_subsicription_date();
    string get_subscribtion_date();
    void purchaseSubscription();
    void Student_Card();
    void Student_Card_info();
    void Public_card_info();
    void Public_Card();
    bool Subscription_confermation(User&);

    void set_expire_date();
    string get_expire_date();
    void set_number_trips();
    int get_number_trips();
    void decrement_number_trips();

};
/*-----------------------------------------SUBSCRIPTION.cpp-----------------------------*/
Subscription::Subscription()
{
    date = "Not assigned yet";
    type = "Not assigned yet";
    stage = 0;
    yearly = false;
    monthly = false;
    cost = 0.0;
    username = "Not assigned yet";
    userEmail = "Not assigned yet";
    number_trips = 0;
}


///////////////////////////////////////////////////////////////////////////////////////////////////////////////
void Subscription::set_number_trips()
{
    if (type == "Student Card") {
        number_trips = 180;
    }
    else if (type == "Public Card") {
        if (monthly == 1) {
            number_trips = 60;
        }
        else if (yearly == 1) {
            number_trips = 730;
        }
    }
}
int Subscription::get_number_trips()
{
    return number_trips;
}
void Subscription::decrement_number_trips() {
    if (type == "Student Card") {
        if (number_trips > 0) {
            number_trips--;
        }
        else {
            cout << "there is no tickets " << "\n";
        }
    }
    else if (type == "Public Card") {
        if (monthly == 1) {
            if (number_trips > 0) {
                number_trips--;
            }
            else {
                cout << "there is no tickets " << "\n";
            }
        }
        else if (yearly == 1) {
            if (number_trips > 0) {
                number_trips--;
            }
            else {
                cout << "there is no tickets " << "\n";
            }
        }
    }
}
void Subscription::set_expire_date()
{

    /*time_t now;
     struct tm current_date;
     char date_buffer[80];
     time(&now);
     localtime_s(&current_date, &now);
    // strftime(date_buffer, sizeof(date_buffer), "%d-%m-%Y", &current_date);
     date2 = date_buffer;
     current_date.tm_mon += 3;
     mktime(&current_date);
     strftime(date_buffer, sizeof(date_buffer), "%d-%m-%Y", &current_date);
     date2 = date_buffer;*/
    time_t now;
    struct tm current_date;
    char date_buffer[80];
    time(&now);
    localtime_s(&current_date, &now);

    // Set default expiration date to 3 months from the current date
    if (type == "Student Card") {
        current_date.tm_mon += 3;
    }
    else if (type == "Public Card") {
        // If monthly subscription, set expiration date to 1 month from current date
        if (monthly == 1 && yearly == 0) {
            current_date.tm_mon += 1;
        }
        // If yearly subscription, set expiration date to 12 months from current date
        else if (yearly == 1 && monthly == 0) {
            current_date.tm_mon += 12;
        }
    }

    // Update expiration date
    mktime(&current_date);
    strftime(date_buffer, sizeof(date_buffer), "%d-%m-%Y", &current_date);
    date2 = date_buffer;

}
string Subscription::get_expire_date()
{
    return date2;
}

///////////////////////////////////////////////////////////////////////////////////////////////////////////////

void Subscription::set_type(string t)
{
    type = t;
}

string Subscription::get_type()
{
    return type;
}

void Subscription::set_stage(int x)
{
    stage = x;
}

int Subscription::get_stage()
{
    return stage;
}

void Subscription::get_Subscription_cost()
{
    if (type == "Student Card") {
        switch (stage)
        {
        case 1:
            cout << "\t .Your Subscription costs 33 LE \n";
            cost = 33;
            break;
        case 2:
            cout << "\t .Your Subscription costs 41 LE \n";
            cost = 41;
            break;
        case 3:
            cout << "\t .Your Subscription costs 50 LE \n";
            cost = 50;
            break;
        case 4:
            cout << "\t .Your Subscription costs 65 LE \n";
            cost = 65;
            break;
        default:
            cout << "\t Not Valied!, Try Again \n";
            break;
        }
    }
    else if (type == "Public Card") {
        if (yearly == true && monthly == false) {
            switch (stage)
            {
            case 1:
                cout << "\t .Your Yearly Subscription costs 1500 LE \n";
                cost = 1500;
                break;
            case 2:
                cout << "\t .Your Yearly Subscription costs 2500 LE \n";
                cost = 2500;
                break;
            case 3:
                cout << "\t .Your Yearly Subscription costs 3500 LE \n";
                cost = 3500;
                break;
            case 4:
                cout << "\t .Your Yearly Subscription costs 4500 LE \n";
                cost = 4500;
                break;
            default:
                cout << "\t Not Valied!, Try Again \n";
                break;
            }
        }
        else if (yearly == false && monthly == true) {
            switch (stage)
            {
            case 1:
                cout << "\t .Your Monthly Subscription costs 230 LE \n";
                cost = 230;
                break;
            case 2:
                cout << "\t .Your Monthly Subscription costs 290 LE \n";
                cost = 290;
                break;
            case 3:
                cout << "\t .Your Monthly Subscription costs 340 LE \n";
                cost = 340;
                break;
            case 4:
                cout << "\t .Your Monthly Subscription costs 450 LE \n";
                cost = 450;
                break;
            default:
                cout << "\t Not Valied!, Try Again \n";
                break;
            }
        }
    }
}

void Subscription::Yearly_Subscription()
{
    yearly = true;
    monthly = false;
}

void Subscription::Monthly_Subscription()
{
    monthly = true;
    yearly = false;
}

bool Subscription::get_Monthly_Subscription()
{
    return monthly;
}

bool Subscription::get_Yearly_Subscription()
{
    return yearly;
}

void Subscription::set_subsicription_date()
{
    time_t now;
    struct tm current_date;
    char date_buffer[80];
    time(&now);
    localtime_s(&current_date, &now);
    strftime(date_buffer, sizeof(date_buffer), "%d-%m-%Y", &current_date);
    date = date_buffer;

}

string Subscription::get_subscribtion_date()
{
    return date;
}

void Subscription::purchaseSubscription()
{

    cout << "\t\tsubscription options:\n";
    cout << "\t                                                             \n";
    cout << "\t1. student card:\n";
    cout << "\t   - 33 LE for stage #1 (1-9 stations)\n";
    cout << "\t   - 41 LE for stage #2 (10-16 stations)\n";
    cout << "\t   - 50 LE for stage #3 (17-23 stations)\n";
    cout << "\t   - 65 LE for stage #4 (greater than 23 stations)\n";
    cout << "\t                                                             \n";
    cout << "\t                                                             \n";
    cout << "\t2. public card (monthly) : \n";
    cout << "\t   - 230 LE for stage #1 (1-9 stations)\n";
    cout << "\t   - 290 LE for stage #2 (10-16 stations)\n";
    cout << "\t   - 340 LE for stage #3 (17-23 stations)\n";
    cout << "\t   - 450 LE for stage #4 (greater than 23 stations)\n";
    cout << "\t                                                             \n";
    cout << "\t   public card (yearly):\n";
    cout << "\t   - 1500 LE for stage #1 (1-9 stations)\n";
    cout << "\t   - 2500 LE for stage #2 (10-16 stations)\n";
    cout << "\t   - 3500 LE for stage #3 (17-23 stations)\n";
    cout << "\t   - 4500 LE for stage #4 (greater than 23 stations)\n";
    cout << "\t                                                             \n";
    cout << "\t                                                             \n";
    cout << "\t3. cash wallet card:" << endl;
    cout << "\t   - No fixed amount. charges individual tickets according to metro stages.\n";
    cout << "\t                                                             \n";

}

void Subscription::Student_Card()
{
    string email;
    bool valid_em = false;
    while (!valid_em) {
        cout << "\tEnter your student email: ";
        cin >> email;
        if (email.length() < 10) {
            cout << "\tNot a valid email. Please try again.\n";
            continue;
        }
        string fifth_em = "@cis.asu.edu.eg";
        if (email.length() >= fifth_em.length() && email.substr(email.length() - fifth_em.length()) == fifth_em) {
            cout << "\tYou have entered a valid email.\n";
            valid_em = true;
        }
        else {
            cout << "\tNot a student email. Please try again.\n";
        }
    }

}

void Subscription::Student_Card_info()
{
    cout << "\t Student pays fixed amount of money every 3 months for 180 trips for limted stations.\n";
    cout << "\t   - 33 LE for stage #1 (1-9 stations)\n";
    cout << "\t   - 41 LE for stage #2 (10-16 stations)\n";
    cout << "\t   - 50 LE for stage #3 (17-23 stations)\n";
    cout << "\t   - 65 LE for stage #4 (greater than 23 stations)\n";

}

void Subscription::Public_card_info()
{
    cout << "\t Person pays fixed amount of money : \n";
    cout << "\t every 1 month for 60 trips for limted stations\n";
    cout << "\t   - 230 LE for stage #1 (1-9 stations)\n";
    cout << "\t   - 290 LE for stage #2 (10-16 stations)\n";
    cout << "\t   - 340 LE for stage #3 (17-23 stations)\n";
    cout << "\t   - 450 LE for stage #4 (greater than 23 stations)\n";
    cout << "\t                                                             \n";
    cout << "\t every 1 year for 730 trips for limted stations\n";
    cout << "\t   - 1500 LE for stage #1 (1-9 stations)\n";
    cout << "\t   - 2500 LE for stage #2 (10-16 stations)\n";
    cout << "\t   - 3500 LE for stage #3 (17-23 stations)\n";
    cout << "\t   - 4500 LE for stage #4 (greater than 23 stations)\n";

}

void Subscription::Public_Card()
{
    cout << "\t You choose public card \n";
}
bool Subscription::Subscription_confermation(User& user)
{
    bool confermed = false;
    if (user.balance >= this->cost) {
        user.balance = user.balance - this->cost;
        cout << "\t Your ticket booked scussefully...\n";
        confermed = true;
    }
    else {
        cout << "\tSorry, you don't have enough money in your wallet to book this ticket\n";
        confermed = false;
    }
    return confermed;
}
/*----------------------------------TICKET.h---------------------------*/
class Ticket
{
private:
    int type;
    int cost;
    string Time_of_booking;

public:
    Ticket();
    void Tickets_info();
    void Select_ticket(int);
    void Selected_ticketinfo();
    void set_Time_of_booking();
    string get_Time_of_booking();
    bool Ticket_confermation(User&);
    string get_time_of_booking();
    int Ticket_cost();
    int get_type();
};
/*----------------------------------TICKET.cpp------------------------------*/
Ticket::Ticket()
{
    type = 0;
    cost = 0;
    Time_of_booking = "Not assigned yet";
}
void Ticket::Tickets_info()
{
    cout << "\t Our Metro Tickets:\n";
    cout << "\t Type (1) --> 6 L.E --> From 1 station to 9 Stations\n";
    cout << "\t Type (2) --> 8 L.E --> From 10 station to 16 Stations\n";
    cout << "\t Type (3) --> 12 L.E --> From 17 station to 23 Stations\n";
    cout << "\t Type (4) --> 15 L.E --> More than 23 Stations \n";
}

void Ticket::Select_ticket(int num_of_stations)
{
    if (num_of_stations >= 1 && num_of_stations <= 9) {
        type = 1;
        cost = 6;
    }
    else if (num_of_stations >= 10 && num_of_stations <= 16) {
        type = 2;
        cost = 8;
    }
    else if (num_of_stations >= 17 && num_of_stations <= 23) {
        type = 3;
        cost = 12;
    }
    else if (num_of_stations >= 23) {
        type = 4;
        cost = 15;
    }
}

void Ticket::Selected_ticketinfo()
{
    if (type == 1) {
        cout << "\t Your ticket is Type (1) \n";
        cout << "\t Your ticket costs : 6 L.E \n";
        cout << "\t Time of booking : " << Time_of_booking << endl;
    }
    else if (type == 2) {
        cout << "\t Your ticket is Type (2) \n";
        cout << "\t Your ticket costs : 8 L.E \n";
        cout << "\t Time of booking : " << Time_of_booking << endl;
    }
    else if (type == 3) {
        cout << "\t Your ticket is Type (3) \n";
        cout << "\t Your ticket costs : 12 L.E \n";
        cout << "\t Time of booking : " << Time_of_booking << endl;
    }
    else {
        cout << "\t Your ticket is Type (4) \n";
        cout << "\t Your ticket costs : 15 L.E \n";
        cout << "\t Time of booking : " << Time_of_booking << endl;
    }
}

void Ticket::set_Time_of_booking()
{
    time_t now;
    struct tm current_date;
    char date_buffer[80];
    time(&now);
    localtime_s(&current_date, &now);
    strftime(date_buffer, sizeof(date_buffer), "%d-%m-%Y %H:%M", &current_date);
    Time_of_booking = date_buffer;

}

string Ticket::get_Time_of_booking()
{
    cout << Time_of_booking << endl;
    return Time_of_booking;
}

bool Ticket::Ticket_confermation(User& user)
{
    bool confermed = false;
    if (user.balance >= cost) {
        user.balance = user.balance - cost;
        cout << "\t Your ticket booked scussefully...\n";
        confermed = true;
    }
    else {
        cout << "\tSorry, you don't have enough money in your wallet to book this ticket\n";
        confermed = false;
    }
    return confermed;
}

string Ticket::get_time_of_booking()
{
    return Time_of_booking;
}

int Ticket::Ticket_cost()
{
    return cost;
}

int Ticket::get_type()
{
    return type;
}
/*----------------------------------CASHWALLETCARD.h----------------------------------*/
class CashWalletCard
{

    string date;
    double amount;
    string username;
    string userEmail;

public:
    void Cash_Wallet_Card_info();
    void set_username(string name);
    string get_username();
    void set_userEmail(string);
    string get_userEmail();
    void set_amount(double);
    double get_amount();
    void set_cash_wallet_card(double);
    double get_cash_wallet_card();
    bool CashWalletCard_confermation(User&);
    void Cash_Wallet_Card(int);
    void Cash_Wallet_date();
    string get_date();
};

/*----------------------------------------CASHWALLETCARD.cpp------------------------------*/
void CashWalletCard::Cash_Wallet_Card_info()
{
    cout << "\t Person pays amount of (Multiples of 10) \n";
    cout << "\t cannot exceed 400 LE and not limited to a specific period \n";

}
void CashWalletCard::set_username(string name)
{
    username = name;
}
string CashWalletCard::get_username()
{
    return username;
}
void CashWalletCard::set_userEmail(string em)
{
    userEmail = em;
}
string CashWalletCard::get_userEmail()
{
    return userEmail;
}
void CashWalletCard::set_amount(double am)
{
    amount = am;
}
double CashWalletCard::get_amount()
{
    return amount;
}
void CashWalletCard::set_cash_wallet_card(double money)
{
    amount = money;
}

double CashWalletCard::get_cash_wallet_card()
{
    return amount;

}
bool CashWalletCard::CashWalletCard_confermation(User& user)
{
    bool confermed = false;
    if (user.balance >= this->amount) {
        user.balance = user.balance - this->amount;
        cout << "\t Your ticket booked scussefully...\n";
        confermed = true;
    }
    else {
        cout << "\t Sorry, you don't have enough money in your wallet to book this ticket. \n";
        confermed = false;
    }
    return confermed;
}
void CashWalletCard::Cash_Wallet_Card(int wallet)
{

    cout << "\t there is no time limit in cash wallet card  \n";

}

void CashWalletCard::Cash_Wallet_date()
{
    time_t now;
    struct tm current_date;
    char date_buffer[80];
    time(&now);
    localtime_s(&current_date, &now);
    strftime(date_buffer, sizeof(date_buffer), "%d-%m-%Y %H:%M:%S", &current_date);
    date = date_buffer;

}
string CashWalletCard::get_date()
{
    return date;

}
/*--------------------------------------------------------------------------*/
vector<User> parse_user_from_line(const string& line, vector<User>& users) {
    User user;
    istringstream iss(line);
    string temp;

    getline(iss >> ws, user.username, ':');
    getline(iss >> ws, user.password, ':');
    getline(iss >> ws, user.email, ':');
    getline(iss >> ws, user.gender, ':');
    // getline(iss >> ws, user.card, ':');
    iss >> user.balance;
    iss.ignore();
    getline(iss >> ws, user.date_of_registration);

    users.push_back(user);
    return users;
}


void Save_Users_Function(vector<User>& users, string& filename, User user) {
    ofstream outfile(filename, ios::trunc);
    if (!outfile) {
        cerr << "Error opening file for writing: " << filename << endl;
        return;
    }
    for (int i = 0; i < users.size(); i++) {
        cout << users[i].get_username() << endl;
        cout << users[i].get_password() << endl;
        cout << users[i].get_email() << endl;
        cout << users[i].get_gender() << endl;
        // cout << users[i].get_Cash_Wallet_Card() << endl;
        cout << "Balance: " << users[i].get_balance() << endl;
        cout << "Date: " << users[i].get_date_of_registration() << endl;

    }
    if (users.empty()) {
        cerr << "No users to save." << endl;
        return;
    }
    for (const auto& user : users) {
        outfile << user.username << ':' << user.password << ':' << user.email << ':' << user.balance << ':' << user.date_of_registration << '\n';
    }
    outfile.close();
    cout << "User data saved to file: " << filename << endl;

}


int main(int argc, char* argv[]) {
    string userChoise, startStations, endStations;

    vector<string>
        choseMenu = {
        "Line1", "Line2", "Line3" },
        line1 = {
         "Helwan","Ain Helwan","Helwan University","Wadi Hof","Hadayek Helwan",
         "Elmasraa","Tura El-Esmant","Kozzika","Tora El-Balad","Sakanat El-Maadi",
         "Maadi","Hadayek El-Maadi","Dar El-Salam","El-Zahraa",  "Mar Girgis", "El-Malek El-Saleh",
         "Al-Sayeda Zeinab", "Saad Zaghloul", "Sadat", "Nasser", "Orabi", "Al-Shohadaa", "Ghamra",
         "El-Demerdash", "Manshiet El-Sadr", "Kobri El-Qobba", "Hammamat El-Qobba", "Saray El-Qobba",
         "Hadayeq El-Zaitoun", "Helmeyet El-Zaitoun", "El-Matareyya", "Ain Shams", "Ezbet El-Nakhl", "El Marg", "New Marg" },
         line2 = {
          "El Monib", "Sakiat Mekky", "Omm El-Masryeen", "Giza", "Faisal", "Cairo University",
          "El Bohoth", "Dokki", "Opera", "Sadat", "Mohamed Naguib", "Attaba", "Al-Shohadaa", "Masarra", "Rod El-Farag",
          "St. Teresa", "Khalafawy", "Mezallat", "Koliet El-Zeraa", "Shubra Al Khaimah" },
          line3 = {
           "Adly Mansour","Haykesteb","Omar Ibn El Khattab","Qubaa","Hesham Barakat","El Nozha","El Shams Club",
           "Alf Maskan","Heliopolis","Haroun","Al-Ahram","Koleyet El-Banat","Stadium","Fair Zone","Abbassiya",
           "Abdou Pasha","El-Geish","Bab El Shaarlya","Attaba","Nasser","Maspero","Safaa Hijazy","Kit-Kat" };
    // insert data (create the metro graph)
    for (int i = 0; i < line1.size() - 1; ++i)
    {
        insertData(line1[i], line1[i + 1]);
    }
    for (int i = 0; i < line2.size() - 1; ++i)
    {
        insertData(line2[i], line2[i + 1]);
    }
    for (int i = 0; i < line3.size() - 1; ++i)
    {
        insertData(line3[i], line3[i + 1]);
    }
    vector<User> users;
    ifstream file("C:\\Users\\Fady\\Desktop\\DS C++ PROJECT\\test files\\pro3\\Registrations.txt");
    string line;

    if (file.is_open()) {
        while (getline(file, line)) {
            users = parse_user_from_line(line, users);
        }
        file.close();
    }
    else {
        cerr << "Error: Unable to open file." << endl;
    }


    User userr;
    map <string, Subscription> subscriptions;
    map <string, CashWalletCard> Cash_Wallet_Cards;
    bool exit = false;
    while (!exit) {
    start:
        system("cls");
        int choice1;
        cout << "\t Welcome to metro mate!" << endl << "\Are you an 1)admin or a 2)user?" << endl;
        cin >> choice1;
        if (choice1 == 1) {
            string username, pass;
            while (true) {
                cout << "Please enter your username:" << endl;
                cin >> username;
                if (username == "admin" || username == "Admin") {
                    break;
                }
                else {
                    cout << "Wrong username,try again!" << endl;
                }
            }
            while (true) {
                cout << "Please enter your password:" << endl;
                pass = "";
                char c;
                bool founded = false;
                while ((c = _getch()) != 13) {
                    if (c == '\b') {
                        if (!pass.empty()) {
                            pass.pop_back();
                            cout << "\b \b";
                        }
                    }
                    else {
                        pass += c;
                        cout << "*";
                    }
                }
                if (pass == "admin" || pass == "Admin") {
                    break;
                }
                else {
                    cout << "Wrong password,try again!" << endl;

                }

            }
            Admin admin;
            string linename;
            cout << "Login successful!" << endl;
            cout << "Please choose an option from the menu!\n";
            vector<string> options = { "1)View all users account","2)Edit a user's account","3)Remove a user's account","4)Add a station","5)Edit a station","6)Remove a station,7)Subscription plan managment,8)view All Ride Logs "};
            string option;
            option = display(options);
            if (option == options[0]) {
                admin.view_acc(users);
            }
            else if (option == options[1]) {
                users = admin.edit_acc(users);
            }
            else if (option == options[2]) {
                users = admin.remove_acc(users);
            }
            else if (option == options[3]) {
                cout << "Which line do you want to add to?" << endl;
                linename = admin.chooseLine();
                if (linename == "Line1") {
                    line1 = admin.addStation(line1, line2, line3, linename);
                }
                else if (linename == "Line2") {
                    line2 = admin.addStation(line1, line2, line3, linename);
                }
                else {
                    line3 = admin.addStation(line1, line2, line3, linename);
                }
            }
            else if (option == options[4]) {
                cout << "Which line do you want to remove from?" << endl;

                linename = admin.chooseLine();
                if (linename == "Line1") {
                    line1 = admin.removeStation(line1, line2, line3, linename);
                }
                else if (linename == "Line2") {
                    line2 = admin.removeStation(line1, line2, line3, linename);
                }
                else {
                    line3 = admin.removeStation(line1, line2, line3, linename);
                }
            }
            else if (option == options[5])
            {
                cout << "In Which line is the station you want to edit?" << endl;

                linename = admin.chooseLine();
                if (linename == "Line1") {
                    line1 = admin.editStation(line1, line2, line3, linename);
                }
                else if (linename == "Line2") {
                    line2 = admin.editStation(line1, line2, line3, linename);
                }
                else {
                    line3 = admin.editStation(line1, line2, line3, linename);
                }

            }
            /*
            else if (option == options[7])
            {
                cout << "1. Create subscription plan to user " << "\n";
                cout << "2. modify subscription plan to user" << "\n";
                cout << "3. remove subscription plan to user" << "\n";
                int choice;
                cin >> choice;
                switch (choice)
                {
                case 1:
                    admin.createSubscription(users, userr, subscriptions);

                    break;
                case 2:


                    // admin.modifySubscription(subscriptions);
                    break;
                case 3:
                    admin.removeSubscription(users, userr, subscriptions);
                    break;
                default:
                    cout << "Invalid choice\n";
                    break;
                }

            }

            */
          else if (option == options[8])
            {
                for (int index = 0; index < users.size(); index++)
                {
                    users[index].viewRideHistory(users[index]);
                }
           }
        }
        else if (choice1 == 2) {


            int choice;
            cout << "\t Welcome!! Please choose an option:\n";
            cout << "\t 1. Register\n";
            cout << "\t 2. Login\n";
            cout << "\t 3. Exit\n";
            cout << "\t Enter Choice: ";
            cin >> choice;
            if (choice == 1) {
                userr.registerUser(users, userr);
            }
            else if (choice == 2) {
                userr.loginUser(users, userr);
            }
            else if (choice == 3) {
                system("cls");
                exit = true;
                cout << "\tGood Luck!\n";
                string filepath = "C:\\Users\\Fady\\Desktop\\DS C++ PROJECT\\test files\\pro3\\Registrations.txt";
                Save_Users_Function(users, filepath, userr);
                Sleep(3000);
                break;
            }
            for (int index = 0; index < users.size(); index++) {
                if (users[index].get_username() == userr.get_username()) {

                start2:
                    cout << "\t Welcome!! Please choose an option:\n";
                    cout << "\t 1. Make a Ride\n";
                    cout << "\t 2. Subscriptions \n";
                    cout << "\t 3. View profile\n";
                    cout << "\t 4. Balance\n";
                    cout << "\t 5. View Ride History\n";
                    cout << "\t 6. Back\n";
                    cout << "\t Enter Choice: ";
                    cin >> choice;
                    if (choice == 1) {
                        if (subscriptions.find(users[index].get_username()) != subscriptions.end()) {
                            Subscription userSubscription = subscriptions[users[index].get_username()];
                            cout << "\tyou have an active subscription:\n";
                            cout << "\ttype: " << userSubscription.get_type() << "\n";
                            cout << "\tstage: " << userSubscription.get_stage() << "\n";
                            cout << "\tsubscription Start Date: " << userSubscription.get_subscribtion_date() << "\n";
                            cout << "\tsubscription Expiry Date: " << userSubscription.get_expire_date() << "\n";
                        }
                        else {
                            cout << "\tyou don't have an active subscription.\n";
                        }
                        Ticket* ticket = new Ticket();
                    start3:
                        string startStation, endStation;
                        cout << "use up and down arrow :)\n";
                        setColor(5, 1);//change color to defualt
                        cout << "Which line are you starting from?\n";
                        userChoise = display(choseMenu);

                        cout << "Please enter the start station\n";
                        if (userChoise == "Line1") {
                            userChoise = display(line1);
                        }
                        else if (userChoise == "Line2") {
                            userChoise = display(line2);
                        }
                        else if (userChoise == "Line3") {
                            userChoise = display(line3);
                        }
                        startStation = userChoise;

                        cout << "Which line will you go to?\n";
                        userChoise = display(choseMenu);

                        cout << "Please enter the end station\n";
                        if (userChoise == "Line1") {
                            userChoise = display(line1);
                        }
                        else if (userChoise == "Line2") {
                            userChoise = display(line2);
                        }
                        else if (userChoise == "Line3") {
                            userChoise = display(line3);
                        }
                        endStation = userChoise;


                        cout << "********* All possible paths between " << startStation << " and " << endStation << " *********" << endl;
                        displayAllPaths(startStation, endStation);
                        int numStations = numberOfStations(startStation, endStation);
                        setColor(1, 1);// change color to blue
                        cout << "The number of stations in your trip is " << numStations << "\n" << "Your The Tiket Price is : ";
                        if (numStations <= 9) {
                            cout << 6;
                        }
                        else if (numStations <= 16) {
                            cout << 8;
                        }
                        else if (numStations <= 23) {
                            cout << 12;
                        }
                        else {

                            cout << 15;
                        }

                        setColor(4, 2);

                        // Display All stations in the trip
                        cout << "\nTrip stations:";
                        setColor(1, 1);// change color to blue
                        cout << displayPath(endStation) << "\n";
                        setColor(1, 2);



                        ticket->set_Time_of_booking();
                        ticket->Selected_ticketinfo();
                    start4:
                        int ch;
                        cout << "\t Confirm Your Ticket ? \n";
                        cout << "\t 1.Confirm \n";
                        cout << "\t 2.Cancel\n";
                        cout << "\t Enter Choice: ";
                        cin >> ch;
                        if (ch == 1) {
                            bool valied = ticket->Ticket_confermation(users[index]);
                            if (valied == false) {
                                cout << "\t Would you like to add money to your wallet? \n";
                                cout << "\t 1. Add\n";
                                cout << "\t 2. Cancel\n";
                                cout << "\t Enter a choice : ";
                                int choice;
                                cin >> choice;
                                if (choice == 1) {
                                    cout << "\t Enter amount fo money that u want to add to yr wallet : ";
                                    double money;
                                    cin >> money;

                                    users[index].add_balance(money);
                                    cout << "\t Money added " << users[index].balance << " L.E to ur balance Successfully!!\n";
                                    cout << "\t Current Balance : " << users[index].balance << endl;
                                    goto start4;
                                }
                                else {
                                    goto start4;
                                }

                            }
                            else if (valied == true) {
                                ofstream outfile("C:\\Users\\Fady\\Desktop\\DS C++ PROJECT\\test files\\pro3\\Tickets.txt", ios::app);
                                //Ticket file data : name // email // current station // target station // ticket fees // date
                                outfile << "\t" << users[index].get_username() << " : " << users[index].get_email() << " : " << ticket->get_type() << " : " << ticket->Ticket_cost() << " : " << ticket->get_time_of_booking() << endl;
                                outfile.close();
                            }
                            Ride ride = Ride(startStation, endStation, ticket->get_time_of_booking());
                            users[index].rideHistory.push_back(ride);
                        }
                        else if (ch == 2) {

                            goto start2;
                        }
                        int back;
                        do {
                            cout << "\t Press 1 to return to Home Page : ";
                            cin >> back;
                        } while (back != 1);
                        goto start2;
                    }
                    else if (choice == 2) {
                        Subscription sub;
                        sub.username = users[index].get_username();
                        sub.userEmail = users[index].get_email();
                        sub.set_subsicription_date();
                        sub.purchaseSubscription();
                    start5:
                        cout << "\t 1. Student Card\n";
                        cout << "\t 2. Public Card \n";
                        cout << "\t 3. Cash Wallet Card\n";
                        cout << "\t 4. Back\n";
                        cout << "\t Please choose an option: ";
                        int ch;
                        cin >> ch;
                        if (ch == 1 || ch == 2)
                        {
                            if (ch == 1) {
                                sub.Student_Card();
                                sub.Student_Card_info();
                                sub.set_type("Student Card");
                                cout << "\t Please choose The stage (1 - 2 - 3 - 4) : ";
                                int st;
                                cin >> st;
                                sub.set_stage(st);
                                sub.get_Subscription_cost();

                            }
                            else if (ch == 2) {
                                sub.Public_card_info();
                                sub.set_type("Public Card");
                                cout << "\t 1. Yearly Subscription\n";
                                cout << "\t 2. Monthly Subscription\n";
                                cout << "\t Please choose an option: ";
                                int choice;
                                cin >> choice;
                                if (choice == 1) { sub.Yearly_Subscription(); }
                                else if (choice == 2) { sub.Monthly_Subscription(); }
                                cout << "\t Please choose The stage (1 - 2 - 3 - 4) : ";
                                int stage;
                                cin >> stage;
                                sub.set_stage(stage);
                                sub.get_Subscription_cost();

                            }

                        start1:
                            cout << "\t Confirm Your Subscription ? \n";
                            cout << "\t 1.Confirm \n";
                            cout << "\t 2.Cancel\n";
                            cout << "\t Enter Choice: ";
                            cin >> ch;
                            if (ch == 1) {
                                bool valied = sub.Subscription_confermation(users[index]);
                                if (valied == false) {
                                    cout << "\t Would you like to add money to your wallet? \n";
                                    cout << "\t 1. Add\n";
                                    cout << "\t 2. Cancel\n";
                                    cout << "\t Enter a choice : ";
                                    int choice;
                                    cin >> choice;
                                    if (choice == 1) {
                                        cout << "\t Enter amount of money that u want to add to yr wallet : ";
                                        double money;
                                        cin >> money;
                                        users[index].add_balance(money);
                                        cout << "\t Money added Successfully!!\n";
                                        cout << "\t Your Currant Balance : " << users[index].get_balance() << endl;
                                        goto start1;
                                    }
                                    else {
                                        goto start1;
                                    }

                                }
                                else if (valied == true) {
                                    subscriptions.insert(make_pair(sub.username, sub));
                                    ofstream outfile("C:\\Users\\Fady\\Desktop\\DS C++ PROJECT\\test files\\pro3\\Subscribtions.txt", ios::app);
                                    //Ticket file data : name // email // type // yearly // Monthly // Stage // cost // date
                                    outfile << "\t" << sub.username << " : " << sub.userEmail << " : " << sub.get_type() << " : " << sub.get_Yearly_Subscription() << " : " << sub.get_Monthly_Subscription() << ":" << sub.get_stage() << " : " << sub.cost << " : " << sub.get_subscribtion_date() << endl;
                                    outfile.close();
                                    int back;
                                    do {
                                        cout << "\t Press 1 to return to Home Page : ";
                                        cin >> back;
                                    } while (back != 1);
                                    goto start2;
                                }

                            }
                            else if (ch == 2) {
                                goto start5;
                            }


                        }
                        else if (ch == 3) {
                            CashWalletCard cash_wallet;
                            cash_wallet.set_username(users[index].username);
                            cash_wallet.set_userEmail(users[index].email);
                            cash_wallet.Cash_Wallet_Card_info();
                            int money;
                            cout << "\t Enter the amount of money that you want to add to your card : ";
                            cin >> money;
                            if (money > 400) {
                                cout << "\t Card limit Cannot exceed 400 LE! Try Again. \n";
                                goto start;
                            }
                            else {
                                cash_wallet.set_cash_wallet_card(money);
                            }
                        start6:
                            cout << "\t Confirm Your Cash Wallet Card ? \n";
                            cout << "\t 1.Confirm \n";
                            cout << "\t 2.Cancel\n";
                            cout << "\t Enter Choice: ";
                            cin >> ch;
                            if (ch == 1) {
                                bool valied = cash_wallet.CashWalletCard_confermation(users[index]);
                                if (valied == false) {
                                    cout << "\t Would you like to add money to your wallet? \n";
                                    cout << "\t 1. Add\n";
                                    cout << "\t 2. Cancel\n";
                                    cout << "\t Enter a choice : ";
                                    int choice;
                                    cin >> choice;
                                    if (choice == 1) {
                                        cout << "\t Enter amount of money that u want to add to yr wallet : ";
                                        double money;
                                        cin >> money;
                                        users[index].add_balance(money);
                                        cout << "\t Money added Successfully!!\n";
                                        cout << "\t Your Currant Balance : " << users[index].get_balance() << endl;
                                        goto start6;
                                    }
                                    else {
                                        goto start6;
                                    }

                                }
                                else if (valied == true) {
                                    Cash_Wallet_Cards.insert(make_pair(cash_wallet.get_username(), cash_wallet));
                                    ofstream outfile("C:\\Users\\Fady\\Desktop\\DS C++ PROJECT\\test files\\pro3\\Cash_Wallet_Cards.txt", ios::app);
                                    //Ticket file data : name // email // amount // date
                                    outfile << "\t" << cash_wallet.get_username() << " : " << cash_wallet.get_userEmail() << ":" << cash_wallet.get_amount() << ":" << cash_wallet.get_date() << endl;
                                    outfile.close();
                                    int back;
                                    do {
                                        cout << "\t Press 1 to return to Home Page : ";
                                        cin >> back;
                                    } while (back != 1);
                                    goto start2;
                                }

                            }
                            else if (ch == 2) {
                                goto start5;
                            }


                        }
                        else if (ch == 4)
                        {
                            goto start5;
                        }
                        else {
                            cout << "\t Not valid option. Try Again \n";
                            goto start5;
                        }


                    }
                    else if (choice == 3) {
                        cout << "----UPDATE USER INFORMATION----\n";

                        cout << "Choose the information you want to update:\n";
                        cout << "1. Update Username\n";
                        cout << "2. Update Password\n";
                        cout << "3. Update Email\n";

                        cout << "Enter the number of the option you want to choose: ";
                        int option;
                        cin >> option;

                        string name, pw, email;
                        bool valid_em = false;
                        int i = 0;
                        bool ch = true;
                        switch (option) {
                        case 1:
                            cout << "current user name : " << userr.get_username() << endl;
                            cout << "\tEnter  new user Name: ";
                            //string name;
                            cin >> name;
                            userr.set_username(name);
                            for (i = 0; i < users.size(); i++) {
                                if (users[i].get_username() == name) {
                                    cout << "Username already exists. Please choose a different one." << endl;

                                }
                                if (i == users.size() - 1) {

                                    cout << "Username updated to: " << name << endl;
                                    break;
                        case 2:

                            while (ch) {
                                cout << "Enter new password: ";
                                cin >> pw;
                                if (pw.length() >= 8) {

                                    userr.set_password(pw);
                                    ch = false;
                                }
                                else {
                                    cout << "\tEnter Minimum 8 Characters!\n";
                                }
                            }
                            break;
                        case 3:
                            cout << "Enter new email: ";
                            cin >> email;

                            while (email.length() > 0 && !valid_em) {
                                if (email.length() < 10) {
                                    cout << "Not a valid email. Please try again.\n";
                                    cin >> email;
                                    continue;
                                }
                                string first_em = "@gmail.com";
                                string second_em = "@yahoo.com";
                                string third_em = "@hotmail.com";
                                string fourth_em = "@outlook.com";
                                string fifth_em = "@cis.asu.edu.eg";
                                if (email.length() >= first_em.length() && email.substr(email.length() - first_em.length()) == first_em) {
                                    cout << "\tYou have entered a valid email." << endl;
                                    valid_em = true;
                                    userr.set_email(email);
                                }
                                if (email.length() >= second_em.length() && email.substr(email.length() - second_em.length()) == second_em) {
                                    cout << "\tYou have entered a valid email." << endl;
                                    valid_em = true;
                                    userr.set_email(email);
                                }
                                if (email.length() >= fourth_em.length() && email.substr(email.length() - fourth_em.length()) == fourth_em) {
                                    cout << "\tYou have entered a valid email." << endl;
                                    valid_em = true;
                                    userr.set_email(email);
                                }
                                if (email.length() >= third_em.length() && email.substr(email.length() - third_em.length()) == third_em) {
                                    cout << "\tYou have entered a valid email." << endl;
                                    valid_em = true;
                                    userr.set_email(email);
                                }
                                if (email.length() >= fifth_em.length() && email.substr(email.length() - fifth_em.length()) == fifth_em) {
                                    cout << "\tYou have entered a valid email." << endl;
                                    valid_em = true;
                                    userr.set_email(email);
                                }
                                if (!valid_em) {
                                    cout << "Not a valid email. Please try again." << endl;
                                    cin >> email;
                                }
                            }

                            break;

                        default:
                            cout << "Invalid option. Please choose a valid option.\n";
                            break;
                                }

                                return 0;

                            }
                        }

                    }
                    else if (choice == 4) {

                    }
                    else if (choice == 5) {
                        users[index].viewRideHistory(users[index]);
                    }
                    else if (choice == 6) {
                        goto start;
                    }
                    else {
                        cout << "\t Unvalid Option \n";
                        goto start2;
                    }
                    Sleep(3000);
                }
                else {
                    continue;
                }
            }
        }
    }

    // QCoreApplication a(argc, argv);

  // return a.exec();

}
