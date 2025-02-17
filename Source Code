


#include<iostream>
#include<string>
#include<vector>
#include<fstream>
#include<iomanip>


using namespace std;


int ReadIntegerPositiveNumber()
{
	int Number = 0;
	cin >> Number;
	while (cin.fail())//what the user input can integer not save.
	{
		cin.clear();
		cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
		cout << "Invalid number!, Enter a valid number\n";
		cin >> Number;
	}
	return Number;
}

string Readstring(string Massege)
{
	string s;
	cout << Massege << endl;
	getline(cin >> ws, s);
	return s;
}
char ReadChar(string massege)
{
	char Name;

	cout << massege;
	cin >> Name;

	return Name;
}

short ReadPositiveNumber(short from, short to)
{
	short Number = 0;
	cin >> Number;
	while (cin.fail() || Number<from || Number>to)//what the user input can integer not save.
	{
		cin.clear();
		cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
		cout << "Invalid number!, Enter a valid number\n";
		cin >> Number;
	}
	return Number;
}

enum enWithdrawChoises {
	twenty = 1, fifty = 2, haunderd = 3, twoHanderds = 4, fourHandred = 5, sixhandred = 6
	, eightHandred = 7, oneTausend = 8, Exit = 9
};

enum enTransation { Deposit = 1, QuiqWithdraw = 2, Withdraw = 3, Showbalance = 4, logout = 5 };


void GoToTransActionMenue();
void DoingWhatChoiseInTransationMinue();


const string FileNameOfClients = "Clients.txt";//Important to write ".txt" Othereways file will not be found.

struct stClientInfo
{
	string name, Telefonnumber, AcountNumber, PINcode;
	double Balance = 0;
	bool markt = false;
};

stClientInfo MainClient;


vector<string>  SplitString(string str, string delim)
{
	vector<string> vWords;

	string word = " ";
	short pos = 0, counter = 0;
	while ((pos = short(str.find(delim))) != std::string::npos)
	{
		word = str.substr(0, pos);

		if (word != "")
		{
			vWords.push_back(word);
		}
		str.erase(0, pos + delim.length());
	}


	if (str != "")
	{

		vWords.push_back(str);
	}


	return vWords;

}

stClientInfo FillStructurFromVector(string info)
{
	vector<string>vstr = SplitString(info, "#//#");
	stClientInfo Client;
	Client.AcountNumber = vstr[0];
	Client.PINcode = vstr[1];
	Client.name = vstr[2];
	Client.Telefonnumber = vstr[3];
	Client.Balance = stod(vstr[4]);
	return Client;

}

vector<stClientInfo> Fillvectorfromfile(string filename)
{
	vector<stClientInfo>vClient;
	fstream file;

	file.open(filename, ios::in);

	if (file.is_open())
	{
		string filecontent;
		stClientInfo sClientinfo;
		while (getline(file, filecontent))
		{
			sClientinfo = FillStructurFromVector(filecontent);
			vClient.push_back(sClientinfo);
		}
		file.close();
	}return vClient;
}

void PrintBalance(stClientInfo Client)
{
	cout << "your Balance after action = " << Client.Balance << endl;


}

bool FindClientWithAcountNumber(vector<stClientInfo>vClientInfo, string AcountNumber, stClientInfo& ClientInfo)
{
	for (stClientInfo& s : vClientInfo)
	{
		if (s.AcountNumber == AcountNumber)
		{
			ClientInfo = s;
			return true;
		}

	}return 0;


}

string ConvertStructurToString(stClientInfo Client)
{
	string st = Client.AcountNumber + "#//#" + Client.PINcode + "#//#" +
		Client.name + "#//#" + Client.Telefonnumber + "#//#" + to_string(Client.Balance);
	return st;
}

vector<stClientInfo> UpdateClientInVector(vector<stClientInfo>vStClients, stClientInfo UpdateAcount)
{


	for (stClientInfo& s : vStClients)
	{
		if (s.AcountNumber == UpdateAcount.AcountNumber)
		{
			s = UpdateAcount;
			break;
		}

	}return vStClients;
}

void SaveFileWithChagedData(vector<stClientInfo>vstr)
{
	fstream file;

	file.open(FileNameOfClients, ios::out);
	// we should always use this form ios::out will great a file if no one were saved,and ios::app will append date in the file.

	if (file.is_open())
	{
		for (stClientInfo s : vstr)
		{
			if (s.markt != true)
			{
				file << ConvertStructurToString(s) << endl;
			}

		}file.close();//do not forget it.
	}
}

void PrintTransactionScreen()
{
	system("cls");

	cout << "\n===============================================\n\n";
	cout << "    A T M   M A I N   M E N U E   S C R E E N   \n\n";
	cout << "===============================================\n";
	cout << "  [1] Deposit .\n";
	cout << "  [2] Quick Withdrew  \n";
	cout << "  [3] Normal Withdrew  \n";
	cout << "  [4] Show The Balance.\n";
	cout << "  [5] Log out .\n";

	cout << "\n=============================================\n";
}

void PrintWithdrawScreen()
{
	system("cls");

	cout << "\n===============================================\n\n";
	cout << "         Quick Withdraw Screen  \n\n";
	cout << "===============================================\n";
	cout << "  [1] 20 .\n";
	cout << "  [2] 50  \n";
	cout << "  [3] 100\n";
	cout << "  [4] 200\n";
	cout << "  [5] 400\n";
	cout << "  [6] 600\n";
	cout << "  [7] 800\n";
	cout << "  [8] 1000\n";
	cout << "  [9] Exit \n";

	cout << "\n=============================================\n";
}

void DoDepositAction()
{
	cout << "\n\n   -------------------------------------\n";
	cout << "                  Deposit Screen            \n";
	cout << "       -------------------------------------\n\n";
	vector<stClientInfo>vStClients = Fillvectorfromfile(FileNameOfClients);

	if (tolower(ReadChar("\nDo you want to deposit in this Acount ? Y/N ?\n")) == 'y')
	{
		cout << "How many should deposit ?\n";
		MainClient.Balance += double((ReadIntegerPositiveNumber()));
		vStClients = UpdateClientInVector(vStClients, MainClient);
		SaveFileWithChagedData(vStClients);

		PrintBalance(MainClient);
	}
	GoToTransActionMenue();

}

short CalculateQuickWithdraw(short num)
{
	switch (num)
	{
	case enWithdrawChoises::twenty:
		return 20;
		break;
	case enWithdrawChoises::fifty:
		return 50;
		break;
	case enWithdrawChoises::haunderd:
		return 100;
		break;
	case enWithdrawChoises::twoHanderds:
		return 200;
		break;
	case enWithdrawChoises::fourHandred:
		return 400;
		break;
	case enWithdrawChoises::sixhandred:
		return 600;
		break;
	case enWithdrawChoises::eightHandred:
		return 800;
		break;
	case enWithdrawChoises::oneTausend:
		return 1000;
		break;
	default:
		system("cls");
		cout << " not a qultie number !! \n";
		DoingWhatChoiseInTransationMinue();
		break;

	}
}

int CheckWithdraw()
{
	cout << "Your balance is " << MainClient.Balance << endl;

	cout << "\nHow many should withdraw ? enter a number which multiple of 5?\n";
	int Withdrawnum = ReadIntegerPositiveNumber();
	while ((Withdrawnum % 5) != 0)
	{
		cout << "Please enter a number which multiple of 5\n";
		Withdrawnum = ReadIntegerPositiveNumber();

	}

	while (MainClient.Balance < Withdrawnum)
	{
		cout << "\n The amount exeeds your balance!!\n You can not withdraw more than \n" << MainClient.Balance;
		cout << "\n Pleas enter a mount less or equal than " << MainClient.Balance << endl;
		Withdrawnum = (ReadIntegerPositiveNumber());

	}return Withdrawnum;
}

void DoWithdrawAction()
{
	cout << "\n\n       -------------------------------------\n";
	cout << "                   Withdraw Screen            \n";
	cout << "           -------------------------------------\n\n";

	vector<stClientInfo>vStClients = Fillvectorfromfile(FileNameOfClients);
	int Amount = CheckWithdraw();

	MainClient.Balance -= Amount;

	vStClients = UpdateClientInVector(vStClients, MainClient);
	SaveFileWithChagedData(vStClients);
	PrintBalance(MainClient);
	GoToTransActionMenue();

}

void DoQuickWithdraw()
{

	vector<stClientInfo>vStClients = Fillvectorfromfile(FileNameOfClients);
	PrintWithdrawScreen();
	cout << "Your balance is " << MainClient.Balance << endl;


	cout << "Please enter the amount, which should withdraw \n";
	short ChoiseNumber = ReadPositiveNumber(1, 9);
	if (ChoiseNumber == 9)
	{
		DoingWhatChoiseInTransationMinue();
		return;
	}
	short Amount = CalculateQuickWithdraw(ChoiseNumber);


	while (MainClient.Balance < Amount)
	{
		system("cls");
		cout << "\nYou can not withdraw more than \n" << MainClient.Balance;
		cout << "\n Pleas enter a mount less or equal than " << MainClient.Balance << endl;

		cout << "  [1] 20 .\n";
		cout << "  [2] 50  \n";
		cout << "  [3] 100\n";
		cout << "  [4] 200\n";
		cout << "  [5] 400\n";
		cout << "  [6] 600\n";
		cout << "  [7] 800\n";
		cout << "  [8] 1000\n";
		cout << "  [9] Exit \n";
		ChoiseNumber = ReadPositiveNumber(1, 9);
		if (ChoiseNumber == 9)
		{
			DoingWhatChoiseInTransationMinue();
			return;
		}
		Amount = CalculateQuickWithdraw(ChoiseNumber);
	}

	MainClient.Balance -= Amount;

	vStClients = UpdateClientInVector(vStClients, MainClient);
	SaveFileWithChagedData(vStClients);
	PrintBalance(MainClient);
	GoToTransActionMenue();


}

void ShowBalancesOfClient()
{

	cout << "\n\n       -------------------------------------\n";
	cout << "                    Balance Screen           \n";
	cout << "           -------------------------------------\n";


	cout << "\n your Balace = " << MainClient.Balance << endl;
	GoToTransActionMenue();

}

void DoingWhatChoiseInTransationMinue()
{
	PrintTransactionScreen();
	cout << " Plese  Choose what do you want to do : ";

	switch (ReadPositiveNumber(1, 5))
	{
	case enTransation::Deposit:
		system("cls");
		DoDepositAction();

		break;
	case enTransation::QuiqWithdraw:
		system("cls");
		DoQuickWithdraw();

		break;
	case enTransation::Withdraw:
		system("cls");
		DoWithdrawAction();

		break;
	case enTransation::Showbalance:
		system("cls");
		ShowBalancesOfClient();

		break;
	case enTransation::logout:
		system("cls");
		cout << "end";
		break;

	default:
		system("cls");
		cout << " not a qultie number !! \n";
		GoToTransActionMenue();
		break;

	}
}

void GoToTransActionMenue()
{
	cout << "\nPress any Key to go to Transaction menue : ";
	cout << system("pause>0");
	DoingWhatChoiseInTransationMinue();
}


bool UserCheck(string AcountNumber, int PinCoud)
{

	vector<stClientInfo>vUser = Fillvectorfromfile(FileNameOfClients);
	return (FindClientWithAcountNumber(vUser, AcountNumber, MainClient) &&
		MainClient.PINcode == to_string(PinCoud));
}

void LogInScreen()
{


	cout << "========================================\n\n";
	cout << "    L O G   IN     S C R E E N    \n\n";
	cout << "========================================\n\n";
	string ClientNumber = "";
	int PIN = 0;
	ClientNumber = Readstring("Please enter the Acount number \n");

	cout << "Please enter the PIN \n";
	PIN = ReadIntegerPositiveNumber();
	while (!UserCheck(ClientNumber, PIN))
	{
		cout << "Acount number or PIN is not correct\n ";

		ClientNumber = Readstring("Please enter the a vailed acount number!\n");
		cout << "Please enter the PIN \n";
		PIN = ReadIntegerPositiveNumber();
	}
	DoingWhatChoiseInTransationMinue();

}




int main()
{
	LogInScreen();
	return 0;

}

