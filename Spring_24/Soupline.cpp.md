```C++
/*
 * Soupline.cpp
 *
 *  Created on: Oct 19, 2021
 *      Author: keith
 */
#include <algorithm>
#include <mutex>
//TODO your includes here 
#include "../includes/Soupline.h"
#include "../includes/externs.h"


#include "../includes/Soupline.h"
#include "../includes/externs.h"


//TODO your implementation here

Soupline::Soupline(int numbBowlsSoup, int numbDrinks) : numbBowlsSoupLeft(numbBowlsSoup), numbDrinksLeft(numbDrinks) {}

void Soupline::restock(int numbBowlsSoup, int numbDrinks) {
    this->numbBowlsSoupLeft = numbBowlsSoup;
    this->numbDrinksLeft = numbDrinks;
}

int Soupline::getSoup(int personID) {
    std::lock_guard<std::mutex> lockSoup(soup_mutex);
    if (numbBowlsSoupLeft == 0) {
        return OUT_OF_SOUP;
    }
    std::lock_guard<std::mutex> lockCustomer(my_customers_mutex);
    //get the fewest bowls of soup served to a customer
    int fewestBowls = getFewestBowlsOfSoupServedToACustomer();
    //searching if the customer exists in the vector and get access to it
    std::vector<customer>::iterator custs = std::find_if(my_customers.begin(), my_customers.end(), [personID](customer c) {
        return c.personID == personID;
    });
    if (custs == my_customers.end()) {
        customer newCust;
        newCust.personID = personID;
        newCust.numbBowlsSoup = 1;
        newCust.numbDrinks = 0;
        my_customers.push_back(newCust);

        numbBowlsSoupLeft--;
        return BOWL_OF_SOUP;
    } else {
        // check to see if there is anybody else in the queue
        if (my_customers.size() == 1) {
            return NOT_YOUR_TURN;
        }
        // checking to see if its the customers turn
        if (custs->numbBowlsSoup == fewestBowls && numbBowlsSoupLeft > 0) {
            numbBowlsSoupLeft--;
            custs->numbBowlsSoup++;
            return BOWL_OF_SOUP;
        }
        return NOT_YOUR_TURN;
    }
}

int Soupline::getDrink(int personID) {
    std::lock_guard<std::mutex> lockDrink(drink_mutex);
    if (numbDrinksLeft == 0) {
        return OUT_OF_DRINKS;
    }
    std::lock_guard<std::mutex> lockCustomer(my_customers_mutex);
    //get the fewest drinks served to a customer
    int fewestDrinks = getFewestDrinksServedToACustomer();
    //searching if the customer exists in the vector and get access to it 
    std::vector<customer>::iterator custs = std::find_if(my_customers.begin(), my_customers.end(), [personID](customer c) {
        return c.personID == personID;
    });
    if (custs == my_customers.end()) {
        customer newCust;
        newCust.personID = personID;
        newCust.numbBowlsSoup = 0;
        newCust.numbDrinks = 1;
        my_customers.push_back(newCust);

        numbDrinksLeft--;
        return DRINK;
    } else {
        // check to see if there is anybody else in the queue
        if (my_customers.size() == 1) {
            return NOT_YOUR_TURN;
        }
        // checking to see if its the customers turn
        if (custs->numbDrinks == fewestDrinks && numbDrinksLeft > 0) {
            numbDrinksLeft--;
            custs->numbDrinks++;
            return DRINK;
        }
        return NOT_YOUR_TURN;
    }
}

int Soupline::getFewestBowlsOfSoupServedToACustomer() {
    if (my_customers.empty()) {
        return ZERO;
    }
    int min = my_customers[0].numbBowlsSoup;
    for (auto c : my_customers) {
        if (c.numbBowlsSoup < min) {
            min = c.numbBowlsSoup;
        }
    }
    return min;
}

int Soupline::getFewestDrinksServedToACustomer() {
    if (my_customers.empty()) {
        return ZERO;
    }
    int min = my_customers[0].numbDrinks;
    for (auto c : my_customers) {
        if (c.numbDrinks < min) {
            min = c.numbDrinks;
        }
    }
    return min;
}



```