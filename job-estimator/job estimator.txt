#include <iostream>
#include <string>
using namespace std;

int DisplayMenu(); // function
void HelpInstructions(); // procedure
void JobEstimator(); // procedure
double paintselector(double nArea); // function
double UnderCoatpaint(double PaintPrice); // function
void ItemisedEstimate(double PaintPrice, double UnderCoatpaint, double GrandTotal); // procedure that takes parameter passed to it

// declaration of global variables.
int nDay, nMonth, nYear, nHeight, nLength, nRoomArea;
string nFirstName, nLastName;

int main() // start of the Main function.
{
    int nChoice;

    nChoice = DisplayMenu(); 

    switch (nChoice)
    {
    case 1:
        cout << "\n Help \n";
        HelpInstructions();
        break;

    case 2:
        cout << "\n Job Estimator \n";
        JobEstimator();
        break;

    case 3:
        exit(0);
        break;

    default:
        cout << " ALERT: Incorrect Data Entry ";
        //cin >> nChoice;
        break;
    }

    system("pause>0");
} // end of the Main function.

int DisplayMenu() // Start of Display Menu function.
{
    int nChoice = 0;
    cout << " ====Main Menu===== \n";
    cout << " 1 - Help \n";
    cout << " 2 - Job Estimator \n";
    cout << " 3 - Exit \n" " ================== \n" " Please enter option 1, 2 or 3 to Exit \n ";
    cin >> nChoice;

    return nChoice;
} // End of Display Menu funciton.

void HelpInstructions() // Start of Help Instructions function.
{
    cout << " Make sure you enter customer name and date \n ";
    cout << " Make sure you enter the height of the room (between 2 and 6 metres) \n ";
    cout << " Make sure you enter the lenght of all four walls \n ";
    cout << " Make sure the minimum length is 1 and the maximum is 25 \n ";

    return;
}// End of Help Instructions function.

void JobEstimator() // Start of JobEstimator function.
{
    cout << " Enter your first name: ";
    cin >> nFirstName;
    cout << " Enter your last name: ";
    cin >> nLastName;
    cout << " Enter the day: ";
    cin >> nDay;
    cout << " Enter the month: ";
    cin >> nMonth;
    cout << " Enter the year: ";
    cin >> nYear;
    cout << " Enter the height of the room: ";
    cin >> nHeight;

    while (nHeight < 2 || nHeight>6)
    {
        cout << " ERROR!! Please enter a number between 2 and 6 \n ";
        cin.clear(); // clears the error
        cin.ignore(100, '\n'); // takes out 1000 characters from the buffer.
        cin >> nHeight; // prompts the user to re-enter the correct height.
    }

    cout << " Enter the length of the room: ";
    cin >> nLength;

    while (nLength < 1 || nLength>25)
    {
        cout << " ERROR!! Please enter a number between 1 and 25 \n ";
        cin.clear(); // clears the error
        cin.ignore(100, '\n'); // takes out 1000 characters from the buffer.
        cin >> nLength; // prompts the user to re-enter the correct length.
    }

    nRoomArea = nLength * nHeight; // automatically multiply the lenght and height.
    paintselector(nRoomArea);

    return;
} // End of JobEstimator function.



double paintselector(double nArea) // Start of Paint selector function.
{
    double LuxPaint = 0.0, StdPaint = 0.0, EcmyPaint = 0.0, PaintPrice{}; // declaration of local variables.
    int UserSelector;
    cout << "    Paint Selector " << endl;
    cout << " 1. Luxury Quality - " << char(156) << "2.75/m2 " << endl;
    cout << " 2. Standard Quality - " << char(156) << "2.00/m2 " << endl;
    cout << " 3. Economy Quality - " << char(156) << "0.55/m2 " << endl;
    cin >> UserSelector;

    while (UserSelector <= 0 || UserSelector >= 4)   
    {
        cout << " Enter a valid number(between 1 to 3) \n";
        cin.clear();
        cin.ignore(100, '\n');
        cin >> UserSelector;
    }

    switch (UserSelector)
    {
    case 1:
        cout << " You selected 1. Luxury Quality." << endl;
        PaintPrice = 2.75 * nArea;
        break;

    case 2:
        cout << " You selected 2. Standard Quality." << endl;
        PaintPrice = 2.00 * nArea;
        break;

    case 3:
        cout << " You selected 3. Economy Quality." << endl;
        PaintPrice = 0.55 * nArea;
        break;
    }

    UnderCoatpaint(PaintPrice); // calling the undercoat paint function in the paint selector function.
    return 0;
} // End of Paint Selector function.

double UnderCoatpaint(double PaintPrice) // start of undercoat paint function.
{
    int Num_of_Tins;
    string Response;
    double UnderCoatPaint = 8.99, UnderCoatPaintSum{}, GrandTotal{};
    cout << " Would you like an undercoat paint (yes or No)? " << endl;
    cin >> Response;

    if (Response == "Yes" || Response == "yes" || Response == "YES" || Response == "y" || Response == "Y")
    {
        cout << " Please enter a whole number to represent the number of tins of paint needed. " << endl;
        cin >> Num_of_Tins;
        UnderCoatPaintSum = UnderCoatPaint + Num_of_Tins; 
        GrandTotal = UnderCoatPaintSum + PaintPrice; 
        ItemisedEstimate(PaintPrice, UnderCoatPaintSum, GrandTotal); // calling the estimate procedure.
    }

    else if (Response == "No" || Response == "no" || Response == "NO" || Response == "n" || Response == "N")
    {
        GrandTotal = PaintPrice;
        ItemisedEstimate(PaintPrice, UnderCoatPaintSum, GrandTotal); // calling the estimate procedure
    }
    return 0;
} // end of undercoat function.

void ItemisedEstimate(double PaintPrice, double UnderCoatPaintSum, double GrandTotal) // start of the estimate procedure.
{
    cout << " Estimate \n " "+++++++++++++++++++++++++++++++++ \n";
    cout << " Customer name: " << nFirstName << " " << nLastName << endl;
    cout << " Estimate date: " << nDay << "/" << nMonth << "/" << nYear << endl;
    cout << " Wall area: " << nRoomArea << endl;
    cout << " Wall cost: " << char(156) << " " << PaintPrice << endl; // char(156) is the ASCII code for pound sign
    cout << " UnderCoat cost: " << char(156) << " " << UnderCoatPaintSum << endl;
    cout << "               ========== " << endl;
    cout << " Grand total: " << char(156) << " " << GrandTotal << endl;
    cout << "               ========== " << endl;

    return;
} // end of the estimate procedure.