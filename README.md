#include <iostream>
#include <string>
#include <cmath>

using namespace std;
int max_resistor =20 ;

double calc_series(double resistor[],int n_resistor )
{
double total = 0;
for(int i=0 ;i<n_resistor ;i++)
total += resistor[i];
return total ;
}
double calc_parallel(double resistor[],int n_resistor )
{
double total = 0;
for(int i=0 ;i<n_resistor ;i++){
        if(resistor[i] ==0){
            return INFINITY ;
        }
total+= 1/resistor[i] ;
}
return 1/total ;
}

double calc_circuit(const string &input, int &index) {
    char connection_type = '\0';
    int n_resistor = 0;
    double resistor[max_resistor];

    while (index < input.length()) {
        char current = input[index];


        if (current == ' ' || current == ',') {
            index++;
            continue;
        }


        if (current == 'e') {
            index++;
            break;
        }


        if (current == 'S' || current == 's' || current == 'P' || current == 'p') {
            if (connection_type == '\0') {
                connection_type = current;
                index++;
            } else {

                index++;
                if (n_resistor >= max_resistor) {
                    cout << "Error: Too many resistors." << endl;
                    exit(0);
                }
                resistor[n_resistor++] = calc_circuit(input, index);
            }
        }

        else if (isdigit(current) || current == '.') {
            double value = 0;
            bool isDecimal = false;
            double decimalPlace = 0.1;

            while (index < input.length() && (isdigit(input[index]) || input[index] == '.')) {
                if (input[index] == '.') {
                    isDecimal = true;
                } else if (isdigit(input[index])) {
                    if (isDecimal) {
                        value += (input[index] - '0') * decimalPlace;
                        decimalPlace *= 0.1;
                    } else {
                        value = value * 10 + (input[index] - '0');
                    }
                }
                index++;
            }

            if (n_resistor >= max_resistor) {
                cout << "Error: Too many resistors." << endl;
                exit(0);
            }
            resistor[n_resistor++] = value;
        } else {
            cout << "Wrong Description" << endl;
            exit(0);
        }
    }


    if (connection_type == '\0') {
        cout << "Wrong Description" << endl;
        exit(0);
    }

    if (connection_type == 'S' || connection_type == 's') {
        if (n_resistor < 1) {
            cout << "Incorrect Input" << endl;
            exit(0);
        }
        return calc_series(resistor, n_resistor);
    } else if (connection_type == 'P' || connection_type == 'p') {
        if (n_resistor < 2) {
            cout << "Incorrect Input" << endl;
            exit(0);
        }
        return calc_parallel(resistor, n_resistor);
    } else {
        cout << "Wrong Description" << endl;
        exit(0);
    }
}

int main(){

    string input ;
    int index =0 ;
    cout<< " Circuit Description"<<endl;
    getline(cin ,input);
    double totalResistors =calc_circuit(input ,index) ;
    cout<<"Total Resistance ="<< totalResistors <<endl;
    return 0 ;
}
