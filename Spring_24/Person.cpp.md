```C++
/*
 * Person.cpp
 *
 *  Created on: Oct 19, 2021
 *      Author: keith
 */
#include <iostream>
#include <thread>
#include <vector>
#include <time.h>
#include <chrono> // this_thread::sleep_for(chrono::milliseconds(MILLI_SECONDS_TO_WAIT));

//TODO your includes here 
#include "../includes/Person.h"
#include "../includes/externs.h"
#include "../includes/constants.h"

//TODO your implementation here

/***
	 * Constructor
	 * @param personID identity of this person, save it
	 */
Person::Person(int id) : personID(id), numbBowlsSoupEaten(0), numbDrinksDrunk(0) {}

/***
	 * gets soup and drinks until SoupLine runs out of both then exits
	 * 
	 * runs a loop repeatedly asking for soup and drinks from msl, the soupline global
	 * calls msl.getSoup(personID)
	 * If call returns NOT_YOUR_TURN then gives other threads a chance by waiting MILLI_SECONDS_TO_WAIT
	 * If call returns BOWL_OF_SOUP then increment numbBowlsSoupEaten
	 * If call returns OUT_OF_SOUP then stop asking for soup
	 * 
	 * calls msl.getDrink(personID)
	 * If call returns NOT_YOUR_TURN then gives other threads a chance by waiting MILLI_SECONDS_TO_WAIT
	 * If call returns DRINK then increment numbDrinksDrunk
	 * If call returns OUT_OF_DRINKS then stop asking for drinks
	 * 
	 * If soupline is out of both soup and drinks this function exits
	 * @return void
	 */
void Person::eatlunch() {
    bool soupAvailable = true;
    bool drinksAvailable = true;

    while (soupAvailable || drinksAvailable) {
        int soupStatus = msl.getSoup(personID);
        if (soupStatus == BOWL_OF_SOUP) {
            numbBowlsSoupEaten++;
        } else if (soupStatus == OUT_OF_SOUP) {
            soupAvailable = false;
        }

        int drinkStatus = msl.getDrink(personID);
        if (drinkStatus == DRINK) {
            numbDrinksDrunk++;
        } else if (drinkStatus == OUT_OF_DRINKS) {
            drinksAvailable = false;
        }

        if (soupStatus == NOT_YOUR_TURN || drinkStatus == NOT_YOUR_TURN) {
            std::this_thread::sleep_for(std::chrono::milliseconds(MILLI_SECONDS_TO_WAIT));
        }
    }
}



```