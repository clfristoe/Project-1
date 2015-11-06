	#include <iostream>
	#include <fstream>
	#include <iomanip>
	using namespace std;
	
	void ReadInput(ifstream &, char &, int &, int &);
	float CalcFee(char &, int &, int &, float &, float &);
	void PrintFee(ofstream &, char &, int &, int &, float &, float &);
	void Footer (ofstream &); 
	void Header (ofstream &);

	int main()
	{
	char VehicleType; int TimeIn; int TimeOut; float totalCost; float totalTime;
	ifstream infile ("DATA1.TXT", ios::in); //registers input file
	ofstream outfile ("OUTPUT", ios::out); //create output file

	outfile.setf(ios::fixed); //sets the outfile to a fixed decimal length
	outfile.precision(2); //sets all float numbers to include two places after the decimal point

	Header(outfile);

	VehicleType = ' ';
	while(VehicleType != 'X') //Read input, calculate and print parking fee until the vehicle type is 'X'
	{
	ReadInput(infile, VehicleType, TimeIn, TimeOut);
	if(VehicleType == 'X') //Stop reading input if vehicle type is 'X'
		break;
	CalcFee(VehicleType, TimeIn, TimeOut, totalCost, totalTime);
	PrintFee(outfile, VehicleType, TimeIn, TimeOut, totalTime, totalCost);
	outfile << endl << endl;
	}
	Footer(outfile);
	*/
	int a,b,c,d,e,f;
	outfile<<"a b c d e f"<<endl;
	for(a=3;a>=1;a--)
	{
		for(b=1;b<3;b++)
		{
			c=a*b;
			d=c++/a;
			e=--d+b;
			f=a-b*e;
			outfile<<a<<" "<<b<<" "<<c<<" ";
			outfile<<d<<" "<<e<<" "<<f<<endl;
		}
		cout<<endl;
	}
	}

	void ReadInput(ifstream &input, char &ID, int &TI, int &TO)
	{
				// Receives - the data file which includes the vehicle type, time a vehicle entered the lot, and time a vehicle exited the lot
				// Task - Reads input and saves to corresponding variables for use in other functions
				// Returns - the vehicle type, entry time, and exit time of a single car

	input >> ID; // assign the type of vehicle (either a car, truck, or senior citizen vehicle) to ID
	input >> TI; // assign the minutes past midnight a vehicle entered the lot to TI
	input >> TO; // the minutes past midnight a vehicle exited the lot TO
	}
	
	float CalcFee(char &CarID, int &TimeIn, int &TimeOut, float &fee, float &totalTime)
	{
				// Receives - the vehicle type, time a vehicle entered the lot, and time a vehicle exited the lot
				// Task - Calculates the parking fee based on the given values
				// Returns - the total fee a vehicle owes

		// calculate the total time in the parking lot
	totalTime = ((float)TimeOut - (float)TimeIn)/60; // Convert the time from minutes to hours
	float newTime = 0.0; 
	float count = 0;
	fee = 0.0;

    // Round the total time up to the next whole number for all numbers up to fourteen
    if(totalTime <1 && totalTime >0)
        totalTime = 1;
    else if(totalTime <2 && totalTime >1)
        totalTime = 2;
    else if(totalTime <3 && totalTime >2)
        totalTime = 3;
    else if(totalTime <4 && totalTime >3)
        totalTime = 4;
    else if(totalTime <5 && totalTime >4)
        totalTime = 5;
    else if(totalTime <6 && totalTime >5)
        totalTime = 6;
    else if(totalTime <7 && totalTime >6)
        totalTime = 7;
    else if(totalTime <8 && totalTime >7)
        totalTime = 8;
    else if(totalTime <9 && totalTime >8)
        totalTime = 9;
    else if(totalTime <10 && totalTime >9)
		totalTime = 10;
	else if(totalTime <11 && totalTime >10)
		totalTime = 11;
	else if(totalTime <12 && totalTime >11)
		totalTime = 12;
	else if(totalTime <13 && totalTime >12)
		totalTime = 13;
	else totalTime = 14;
	newTime = totalTime;

	if(CarID == 'C') // calculate the fee for a car.    
	{
		while(newTime <= totalTime && newTime >0) //Calculate the fee for every hour inside the parking lot
		{
		
			while(newTime >= 6) // Calculate the fee for parking over six hours
			{	
				fee += .05f; //for every hour more than six, add five cents to the running total
				newTime--;
			}
			while(newTime > 2) // Calculate the fee for parking over two hours
			{
				fee += .15f; //for every hour more than two, add fifteen cents to the running total
				newTime--;
			}
			while(newTime > 0) // Calculate the fee for the first two hours
			{
				fee += .20f; //for the first two hours, add twenty cents to the running total
				newTime--;
			}
		}
		// end if 
	}
	
	else if( CarID == 'T') // Calculate the fee for a truck
	{
		while(newTime <= totalTime && newTime >0) //Calculate the fee for every hour inside the parking lot
		{
		
			while(newTime >= 4) // Calculate the fee for parking over four hours
			{	
				fee += .10f; //for every hour more than four, add ten cents to the running total
				newTime--;
			}
			while(newTime > 1) // Calculate the fee for parking over one hour, but less than four hours
			{
				fee += .25f; //for every hour more than one, add ten cents to the running total
				newTime--;
			}
			while(newTime > 0) // Calculate the fee for the first hour
			{
				fee += .40f; //for the first hour, add ten cents to the running total
				newTime--;
			}
		}
		// end if 
	}
	// end if
	else if (CarID == 'S') // Calculate the fee for a senior citizen car
	{
		fee = totalTime *.12f; //Multiply the time
	}
	// end if
	return fee;
	}

	void PrintFee(ofstream &Outfile, char &VT, int &Ti, int &To, float &totalT, float &totalC)

				// Receives - the vehicle type, time a vehicle entered the lot, the time a vehicle exited the lot, the total time, and the final cost
				// Task - Prints out a receipt with the type of vehicle, total time in the lot, and the amount owed
				// Returns - nothing

	{
	//Print out the input data
	Outfile << "The input data was: " << endl;
	Outfile << "  "<<VT<<" "<<Ti<<" "<<To << endl; 
	Outfile << endl;

	//Print out ticket with name of school, parking fee
	Outfile <<setw(25)<<"$$$$$$$$$$$$$$$$$$$$$$$$$"<<endl;
	Outfile <<setw(0) <<"$";
	Outfile <<setw(24)<<"$"<< endl;
	Outfile <<setw(0) <<"$	MISSOURI WESTERN";
	Outfile <<setw(5) <<"$"<< endl;
	Outfile <<setw(0) <<"$	UNIVERSITY";
	Outfile <<setw(11)<<"$"<< endl;
	Outfile <<setw(0) <<"$";
	Outfile <<setw(24)<<"$"<< endl;
	Outfile <<setw(24) <<"$$$$$$$$$$$$$$$$$$$$$$$$$"<<endl;
	Outfile <<setw(24) <<"$$$$$$$$$$$$$$$$$$$$$$$$$"<<endl;
	Outfile <<setw(0) <<"$	  PARKING FEE";
	Outfile <<setw(8)<<"$"<< endl;
	Outfile <<setw(0) <<"$";

	//Print out vehicle type
	Outfile <<setw(24)<<"$"<< endl;
	Outfile <<setw(0)<<"$  Customer";
	Outfile <<setw(14)<<"$"<< endl;
	Outfile <<setw(0)<<"$  Category:";
	if(VT == 'C') // Print out Car on the ticket if the vehicle type is C
	{
		Outfile <<setw(5)<<"Car";
		Outfile <<setw(8)<<"$"<< endl;
	}
	if(VT == 'T') // Print out Truck on the ticket if the vehicle type is T
	{
		Outfile <<setw(7)<<"Truck";
		Outfile <<setw(6)<<"$" << endl;
	}
	if(VT == 'S') // Print out SC on the ticket if the vehicle type is S 
	{
		Outfile <<setw(4)<<"SC";
		Outfile <<setw(9)<<"$" << endl;
	}
	Outfile <<setw(0) <<"$";
	Outfile <<setw(24)<<"$"<< endl;

	//Print out the total time the vehicle was in the parking lot
	Outfile <<setw(0) <<"$  Time:";
	if(totalT>9) //If the time is a double digit, print out spacing differently
	{
		Outfile <<setprecision(0)<<setw(8)<<totalT;
		if(totalT==1) //Print out "hour" (instead of hours) if the total time is one hour
		{
			Outfile <<setw(0)<<" hour";
			Outfile <<setw(4)<<"$" <<endl;
		}
		else //Print out "hours" for every other case
		{
			Outfile <<setw(0)<<" hours";
			Outfile <<setw(3)<<"$"<< endl;
		}
	}
	//end if 
	else
	{
		Outfile <<setprecision(0)<<setw(7)<<totalT;
		if(totalT==1) //Print out "hour" (instead of hours) if the total time is one hour
		{
			Outfile <<setw(0)<<" hour";
			Outfile <<setw(3)<<"$" <<endl;
		}
		else //Print out "hours" for every other case
		{
			Outfile <<setw(0)<<" hours";
			Outfile <<setw(4)<<"$"<< endl;
		}
	}
	//end else
	Outfile <<setw(0) <<"$";
	Outfile <<setw(24)<<"$"<< endl;

	// Print out the amount paid
	Outfile <<setw(0) <<"$  Amount";
	Outfile <<setw(16)<<"$"<< endl;
	Outfile <<setw(0) <<"$  Paid:";
	Outfile <<setw(7)<< "$" <<setprecision(2)<<totalC;
	Outfile <<setw(6)<<"$" << endl;
	Outfile <<setw(0) <<"$";
	Outfile <<setw(24)<<"$"<< endl;
	Outfile <<setw(24) <<"$$$$$$$$$$$$$$$$$$$$$$$$$"<<endl;
	Outfile <<endl;
}
