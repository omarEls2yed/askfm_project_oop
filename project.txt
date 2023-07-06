#define _CRT_SECURE_NO_WARNINGS
#include <algorithm>
#include <array>
#include <bitset>
#include <cassert>
#include <chrono>
#include <climits>
#include <cmath>
#include <complex>
#include <cstring>
#include <functional>
#include <iomanip>
#include <iostream>
#include <map>
#include <numeric>
#include <queue>
#include <random>
#include <set>
#include <vector>
#include <stack>
#include <unordered_set>
#include <unordered_map>
#include <algorithm>
#include <fstream>
#include <string>
using namespace std;
#define ll long long
class User
{
public:
    string id;
    string name;
    string password;
    vector<User>users;
    vector<string>showUsers;
    User()
    {

    }
    User(string name, string id, string password)
    {
        this->name = name;
        this->id = id;
        this->password = password;
    }
    void saveUser(User us)
    {
        fstream outFile;
        outFile.open("save_user.txt", ios::app);
        if (outFile.is_open())
        {
            outFile << us.name << endl;
            outFile << us.id << endl;
            outFile << us.password << endl;
            outFile.close();
        }
    }
    void ShowAllUsersInSystem()
    {
        fstream myfile;
        myfile.open("save_user.txt", ios::in);
        if (myfile.is_open())
        {
            string line;
            ll counter = 0;
            //omar 2334 123
            bool cheak;
            while (getline(myfile, line))
            {
                if (counter == 0 or counter == 1)
                {
                    showUsers.push_back(line);
                    counter++;
                    cheak = 1;
                }
                else if (counter == 2 and cheak == 0)
                {
                    counter = 0;
                }
                cheak = 0;
            }
            myfile.close();
            ll counter2 = 1;
            for (int i = 0; i < showUsers.size() - 1; i++)
            {
                if (i != 1 and i != 2 and i != 3 and (i % 2 == 0))
                {
                    cout << counter2 << " - " << '(' << showUsers[i] << ')' << " with id " << '(' << showUsers[i + 1] << ')' << endl;
                    counter2++;
                }
            }
        }
    }
};
class Question {
public:
    string id_author;
    string too;
    string questionn;
    vector<string>questt;
    vector<string>showall;
    Question(string questionn, string id_author, string too)
    {
        this->questionn = questionn;
        this->id_author = id_author;
        this->too = too;
    }
    Question()
    {

    }
    void savequestion(Question qu)
    {
        fstream outFile;
        outFile.open("save questions.txt", ios::app);
        if (outFile.is_open())
        {
            outFile << qu.too << endl;
            outFile << qu.questionn << endl;
            outFile << qu.id_author << endl;
            outFile.close();
        }
    }
    void showQuestionSentToMe(string id)
    {
        fstream myfile;

        myfile.open("save questions.txt", ios::in);

        if (myfile.is_open())
        {
            string line; bool bb = 0;

            while (getline(myfile, line))
            {
                questt.push_back(line);
            }

            myfile.close();
        }
        ll counter4 = 0;
        for (int i = 0; i < questt.size() - 2; i++)
        {
            if (questt[i] == id)
            {
                cout << counter4 << " - " << questt[i + 1] << " FROM " << '(' << questt[i + 2] << ')' << endl;
            }
            counter4++;
        }
    }
    void ShowAllAnswerInSystem()
    {
        fstream myfile;

        myfile.open("save questions.txt", ios::in);

        if (myfile.is_open())
        {
            string line;
            while (getline(myfile, line))
            {
                showall.push_back(line);
            }
            myfile.close();
        }
        ll counter7 = 1;
        ll counter8 = 1;
        // 1 3 4 6 7 9 10 12 13
        for (int i = 24; i < showall.size() - 2; i += 3)
        {// to quest id auter
         // i   i+1    i+2
            cout << showall[i] << " from id " << '(' << showall[i + 1] << ')' << " to id " << '(' << showall[i + 2] << ')' << endl;
        }
    }
};
class Answer
{
public:
    string to;
    string id_authors;
    string answerr;
    vector<string>ansss;
    Answer()
    {

    }
    Answer(string answerr, string id_authors, string to)
    {
        this->answerr = answerr;
        this->id_authors = id_authors;
        this->to = to;
    }
    void saveanswer(Answer a)
    {
        fstream outFile;
        outFile.open("save answers.txt", ios::app);
        if (outFile.is_open())
        {
            outFile << a.to << endl;
            outFile << a.answerr << endl;
            outFile << a.id_authors << endl;
            outFile.close();
        }
    }
    void showAnswerSentToMe(string id)
    {
        fstream myfile;
        myfile.open("save answers.txt", ios::in);
        if (myfile.is_open())
        {
            string line; bool bb = 0;
            while (getline(myfile, line))
            {
                ansss.push_back(line);
            }
            myfile.close();
        }

        ll counter3 = 1;

        for (int i = 0; i < ansss.size() - 2; i++)
        {
            if (ansss[i] == id)
            {
                cout << counter3 << " - " << ansss[i + 1] << " FROM " << '(' << ansss[i + 2] << ')' << endl;
            }
            counter3++;
        }
    }
};
int main()
{
    cout << "Choose a number from the numbers" << endl;
    cout << "1 - sign up" << endl;// new user
    cout << "2 - login" << endl;  // old user
    ll x; cin >> x;
    User user; Answer A; Question Q;
    if (x == 1)
    {
        while (1) 
        {
            string name2;
            while (1)
            {
                cout << "enter your name" << endl;
                string name;
                cin >> name;
                fstream outFile;
                outFile.open("save_user.txt", ios::in);
                if (outFile.is_open())
                {
                    string line;
                    bool cheak = 0;
                    while (getline(outFile, line))
                    {
                        if (line == name)
                        {
                            cout << "name is already taken please choose another " << endl;
                            cheak = 1;

                        }
                    }
                    outFile.close();
                    if (cheak == 0) 
                    {
                        name2 = name;
                        break;
                    }
                }
            }
            cout << "create id please" << endl;
            string id;
            cin >> id;
            cout << "YOUR ID HAS BEEN CREATED " << endl;
            cout << "YOUR ID IS" << " " << id << endl;
            cout << "ENTER YOUR PASSWORD" << endl;
            string password;
            cin >> password;
            user = User(name2, id, password);// to create new user
            user.saveUser(user);
            cout << "Hello" << "  " << user.name << endl;
            while (1) 
            {
                cout << "please Choose operation" << endl;
                cout << "1 - send question  " << endl;
                cout << "2 - give answer to question  " << endl;
                cout << "3 - view answers sent to you  " << endl;
                cout << "4 - view question sent to you  " << endl;
                cout << "5 - view all user in system  " << endl;
                cout << "6 - view all question in the system  " << endl;
                cout << "7 - log out" << endl;
                ll yourchoise;
                cin >> yourchoise;
                if (yourchoise == 1)
                {
                    cout << "enter your question" << endl;
                    string questi;
                    cin.ignore();
                    getline(cin, questi);
                    cout << "YOUR QUESTION IS" << endl;
                    cout << questi << endl;
                    cout << "enter the id you want to ask" << endl;
                    string to_id;
                    cin >> to_id;
                    Question q(questi, user.id, to_id);
                    q.savequestion(q);
                    cout << "OK ask has been sent correctly" << endl;
                }
                else if (yourchoise == 2)
                {
                    cout << "This is question sent to you answer any of them" << endl;
                    Q.showQuestionSentToMe(user.id);
                    cout << "Please enter your answer and number of question" << endl;
                    string ans;
                    cin.ignore();
                    getline(cin, ans);
                    cout << "YOUR ANSWER IS" << endl;
                    cout << ans << endl;
                    cout << "ENTER THE ID you want to answer him" << endl;
                    string to_id;
                    cin >> to_id;
                    Answer a(ans, user.id, to_id);
                    a.saveanswer(a);
                    cout << "OK your answer has been sent" << endl;
                }
                else if (yourchoise == 3)
                {
                    A.showAnswerSentToMe(user.id);
                }
                else if (yourchoise == 4)
                {
                    Q.showQuestionSentToMe(user.id);
                }
                else if (yourchoise == 5)
                {
                    user.ShowAllUsersInSystem();
                }
                else if (yourchoise == 6)
                {
                    Q.ShowAllAnswerInSystem();
                }
                else if (yourchoise == 7)
                {
                    return 0;
                }
                cout << "if you want anothe operation choose 1 if you want to end program choose 0" << endl;
                ll ch;
                cin >> ch;
                if (ch == 0)
                {
                    break;
                }
                else 
                {
                    continue;
                }

            }
            cout << "are you want to sign up again choose 1 if you dont choose 0" << endl;
            ll kj;
            cin >> kj;
            if (kj == 0) 
            {
                break;
            }
            else 
            {
                continue;
            }
        }
    }
    else if (x == 2)
    {
        while (1)
        {
            cout << "enter your name" << endl;
            string name;
            cin >> name;
            cout << "enter your id" << endl;
            string id;
            cin >> id;
            cout << "ENTER YOUR PASSWORD" << endl;
            string password;
            cin >> password;
            user = User(name, id, password);
            fstream outFile;
            outFile.open("save_user.txt", ios::in);
            bool one = 0;
            if (outFile.is_open())
            {
                string line;
                while (getline(outFile, line))
                {
                    if (line == user.id)
                    {
                        one = 1;
                    }

                }outFile.close();
            }
            if (one == 0)
            {
                cout << "Sorry user not found" << endl; return 0;
            }
            cout << "Hello again" << "  " << user.name << endl;
            while (1)
            {
                cout << "please Choose operation" << endl;
                cout << "1 - send question" << endl;
                cout << "2 - give answer to question" << endl;
                cout << "3 - view answers sent to you" << endl;
                cout << "4 - view question sent to you" << endl;
                cout << "5 - view all user in system  " << endl;
                cout << "6 - view all question in the system  " << endl;
                cout << "7 - log out" << endl;
                ll yourchoise;
                cin >> yourchoise;
                if (yourchoise == 1)
                {
                    cout << "enter your question" << endl;
                    string questi;
                    cin.ignore();
                    getline(cin, questi);
                    cout << "YOUR QUESTION IS" << endl;
                    cout << questi << endl;
                    cout << "enter the id you want to ask" << endl;
                    string to_id;
                    cin >> to_id;
                    Question q(questi, user.id, to_id);
                    q.savequestion(q);
                    cout << "OK ask has been sent correctly" << endl;
                }
                else if (yourchoise == 2)
                {
                    cout << "This is question sent to you answer any of them" << endl;
                    Q.showQuestionSentToMe(user.id);
                    cout << "Please enter your answer and number of question" << endl;
                    string ans;
                    cin.ignore();
                    getline(cin, ans);
                    cout << "YOUR ANSWER IS" << endl;
                    cout << ans << endl;
                    cout << "ENTER THE ID you want to answer him" << endl;
                    string to_id;
                    cin >> to_id;
                    Answer a(ans, user.id, to_id);
                    a.saveanswer(a);
                    cout << "OK your answer has been sent" << endl;
                }
                else if (yourchoise == 3)
                {
                    A.showAnswerSentToMe(user.id);
                }
                else if (yourchoise == 4)
                {
                    Q.showQuestionSentToMe(user.id);
                }
                else if (yourchoise == 5)
                {
                    user.ShowAllUsersInSystem();
                }
                else if (yourchoise == 6)
                {
                    Q.ShowAllAnswerInSystem();
                }
                else if (yourchoise == 7)
                {
                    return 0;
                }
                cout << "if you want anothe operation choose 1 if you want to end program choose 0" << endl;
                ll ch;
                cin >> ch;
                if (ch == 0)
                {
                    break;
                }
                else {
                    continue;
                }

            }
            cout << "are you want to login again choose 1 if you dont choose 0" << endl;
            ll kj;
            cin >> kj;
            if (kj == 0) 
            {
                break;
            }
            else 
            {
                continue;
            }
        }
    }
    else
    {
        cout << "invalid input program end tray to open again and choose valid input" << endl;
    }
}
// walled with id 10 sent quest to ezzat  with id 5 
// and say how old are you and send another quest and say where are you from
// first i will creat walled and ezzat account
// walled will view users and choise ezzat to ask him
// sign up with walled and ezzat 
// walled sent 2 question to ezzat
// ezzat view question sent to him 
// ezzat sent answer to walled question
// walled view answers sent to him 
// try invalid login and sign up
// end the program;