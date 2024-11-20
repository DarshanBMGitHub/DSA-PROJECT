#include <iostream>
#include <iomanip>
#include <string>
using namespace std;

// Structure to store vehicle information
struct Vehicle {
    string type;           // Type of vehicle
    int count;             // Number of vehicles of this type
    double tollCharge;     // Toll charge per vehicle
    double revenue;        // Total revenue from this vehicle type

    // Constructor
    Vehicle(string t = "", double charge = 0.0)
        : type(t), count(0), tollCharge(charge), revenue(0.0) {}
};

// Structure to store toll booth data
struct TollBooth {
    Vehicle cars{"car", 130};
    Vehicle bikes{"bike", 0};
    Vehicle buses{"two-axle bus", 460};
    Vehicle trucks{"two-axle truck", 560};
    Vehicle threeAxles{"three-axle", 720};
    double totalRevenue = 0.0;

    // Function to add a vehicle
    void addVehicle(const string &vehicleType) {
        if (vehicleType == "car") {
            cars.count++;
            cars.revenue += cars.tollCharge;
            totalRevenue += cars.tollCharge;
            cout << "Car added. Toll: ₹" << cars.tollCharge << endl;
        } else if (vehicleType == "bike") {
            bikes.count++;
            cout << "Bike added. Toll: Free" << endl;
        } else if (vehicleType == "two-axle") {
            string twoAxleType;
            cout << "Enter type of two-axle vehicle (bus/truck): ";
            cin >> twoAxleType;

            if (twoAxleType == "bus") {
                buses.count++;
                buses.revenue += buses.tollCharge;
                totalRevenue += buses.tollCharge;
                cout << "Two-Axle Bus added. Toll: ₹" << buses.tollCharge << endl;
            } else if (twoAxleType == "truck") {
                trucks.count++;
                trucks.revenue += trucks.tollCharge;
                totalRevenue += trucks.tollCharge;
                cout << "Two-Axle Truck added. Toll: ₹" << trucks.tollCharge << endl;
            } else {
                cout << "Invalid type of two-axle vehicle!" << endl;
            }
        } else if (vehicleType == "three-axle") {
            threeAxles.count++;
            threeAxles.revenue += threeAxles.tollCharge;
            totalRevenue += threeAxles.tollCharge;
            cout << "Three-Axle Commercial Vehicle added. Toll: ₹" << threeAxles.tollCharge << endl;
        } else {
            cout << "Invalid vehicle type!" << endl;
        }
    }

    // Function to display the toll booth report
    void displayReport() const {
        cout << "\nToll Booth Report:" << endl;
        cout << "===================" << endl;
        cout << "Cars: " << cars.count << " | Revenue: ₹" << fixed << setprecision(2) << cars.revenue << endl;
        cout << "Bikes: " << bikes.count << " | Revenue: ₹" << bikes.revenue << endl;
        cout << "Two-Axle Buses: " << buses.count << " | Revenue: ₹" << buses.revenue << endl;
        cout << "Two-Axle Trucks: " << trucks.count << " | Revenue: ₹" << trucks.revenue << endl;
        cout << "Three-Axle Commercial Vehicles: " << threeAxles.count << " | Revenue: ₹" << threeAxles.revenue << endl;
        cout << "-------------------" << endl;
        cout << "Total Revenue: ₹" << totalRevenue << endl;
    }
};

int main() {
    TollBooth tollBooth;
    int choice;
    string vehicleType;

    do {
        cout << "\nToll Management System" << endl;
        cout << "1. Add Vehicle" << endl;
        cout << "2. Display Report" << endl;
        cout << "3. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            cout << "Enter vehicle type (car/bike/two-axle/three-axle): ";
            cin >> vehicleType;
            tollBooth.addVehicle(vehicleType);
            break;

        case 2:
            tollBooth.displayReport();
            break;

        case 3:
            cout << "Exiting the system. Thank you!" << endl;
            break;

        default:
            cout << "Invalid choice! Please try again." << endl;
        }
    } while (choice != 3);

    return 0;
}
