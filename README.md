//-----------------------//
//   CODIGO HECHO POR    //
//   Aquiles Millán      //
//   V31.706.783         //
//   Alonso Acosta       //
//   V31.460.751         //
//   Nicole Becerra      //
//   V                   //
// Cátedra: Algortimos   //
//y estructuras de datos //
//-----------------------//


//Bibliotecas necesarias para la ejecución del codigo//
using namespace std;
#include <iostream>
#include <vector>
#include <limits>
#include <ios>
#include <bits/stdc++.h>

//Declaración de la estructura usada para los objetos de tipo weapons (armas)//
struct Weapons
{

    string name;
    int damage;
    int energycost;

};

//Lista donde se almacenan las armas creadas

vector<Weapons>Weaponslist;

//Declaración de la estructura usada para los objetos de tipo helpobjects (objetos de ayuda/ambiente) Nota: son los objetos que trabajan con respecto al campo de batalla //

struct Helpobjects
{

    string name;
    string helptype;

};

//Lista donde se almacenan los help objects creados

vector<Helpobjects>Helpobjectslist;

//Declaración de la estructura empleada para objetos de curación

struct HealingObjects
{
    string name;
    int healvalue;
    int energyboost;

};

//Lista donde  se almacenan los healing objects

vector<HealingObjects>HealingObjectsList;

//declaracion de la estructura de Razas
struct Races
{

    string name;
    int life;
    int energy;
    string ambiencedebuff;

};

//Lista donde se almacenan las Razas creadas

vector<Races>Raceslist;

struct Battlegrounds
{
    string name;
    string debuff;
};

vector<Battlegrounds>battlegroundslist;

//Estructura donde se almacenan los objetos que se utilizaran en batalla

struct Backpack
{
    string name;
    Weapons * weapon;
    HealingObjects * healing;
    Helpobjects * help;

};

vector<Backpack>backpacklist;

//Estructura donde se les asigna los datos a cada personaje 

struct Warriors
{
    string name;
    Races * race;
    Backpack * backpack;

};

vector<Warriors>Team1;
vector<Warriors>Team2;

// Funcion para visualizar los objetos de ayuda

void funcionviewhelpobjects()
{
    Helpobjects help;

    cout << "-----------------" << "\n   Help Objects list\n" << "-----------------\n";

    for (const auto& ho:Helpobjectslist)
    {
                cout << "\nHELP OBJECT NAME: " << ho.name << "\nThis object will help you in " << ho.helptype << " ambience\n" << "\n-----------------\n";
    }
}

// Funcion para crear y asignar valores a elementos de help objects

void funcioncreatehelpobjects()
{
    bool verif1 = false;

    Helpobjects help;

    cout << "\nLet's create a help object!!!\n";

    cout << "\nName: " ;
    cin>> help.name;

    while(verif1 == false)
    {
        cout << "\nOn what kind of ambience is this artifact helping you? [oxygen, heat, cold, gas, poisonous, putrid]: ";
        cin>> help.helptype;

            if(help.helptype != "oxygen" and help.helptype != "heat" and help.helptype != "cold" and help.helptype != "gas" and help.helptype != "poisonous" and help.helptype != "putrid")
            {
                cout<< "\nThat's not a valid option, please select one kind of ambience\n";
            }
            else
            {
                verif1 = true;
            }
    }
    

    Helpobjectslist.push_back(help);

    cout << "\nHelp object was created succesfully!!!\n"; 

}

// Funcion para editar o recrear un elemento de help objects

void funcionedithelpobjects()
{
    Helpobjects help;
    string namehelptodelete;

    cout << "\nLet's re create a help object!!!\n";

    cout << "-----------------" << "\n   Help Objects list\n" << "-----------------\n";

    for (const auto& ho:Helpobjectslist)
    {
                cout << "\nHELP OBJECT NAME: " << ho.name << "\nThis object will help you in " << ho.helptype << "ambience\n" << "\n-----------------\n";
    }

    cout << "-------------------------------------------------" << "\n   Select the help object do you want to edit\n" << "-------------------------------------------------\n"; 

    cin >> namehelptodelete;

    Helpobjectslist.erase(remove_if(Helpobjectslist.begin(), Helpobjectslist.end(), [namehelptodelete] (const Helpobjects& ho) {return ho.name == namehelptodelete; }), Helpobjectslist.end());

    bool verif1 = false;

    cout << "\nWrite the new data of the help object!!!\n";

    cout << "\nName: " ;
    cin>> help.name;

    while(verif1 == false)
    {
        cout << "\nOn what kind of ambience is this artifact helping you? [oxygen, heat, cold, gas, poisonous, putrid]: ";
        cin>> help.helptype;

            if(help.helptype != "oxygen" and help.helptype != "heat" and help.helptype != "cold" and help.helptype != "gas" and help.helptype != "poisonous" and help.helptype != "putrid")
            {
                cout<< "\nThat's not a valid option, please select one kind of ambience\n";
            }
            else
            {
                verif1 = true;
            }
    }
    

    Helpobjectslist.push_back(help);

    cout << "Help object re created successfully.\n";
}

// Funcion para eliminar algun objeto de ayuda

void funciondeletehelpobjects()
{
    Helpobjects help;
    string namehelptodelete;

    cout << "\nLet's delete a help object!!!\n";

    cout << "-----------------" << "\n   Help Objects list\n" << "-----------------\n";

    for (const auto& ho:Helpobjectslist)
    {
                cout << "\nHELP OBJECT NAME: " << ho.name << "\nThis object will help you in " << ho.helptype << "ambience\n" << "\n-----------------\n";
    }

    cout << "-------------------------------------------------" << "\n   Select the help object do you want to delete\n" << "-------------------------------------------------\n"; 

    cin >> namehelptodelete;

    Helpobjectslist.erase(remove_if(Helpobjectslist.begin(), Helpobjectslist.end(), [namehelptodelete] (const Helpobjects& ho) { return ho.name == namehelptodelete; }), Helpobjectslist.end());

    cout << "Help object deleted successfully.\n";
}

// Funcion para visualizar los objetos de curacion

void funcionviewhealinglobjects()
{
    cout << "-----------------" << "\n   Healing Objects list\n" << "-----------------\n";

        for (const auto& h:HealingObjectsList)
        {
                    cout << "\nHEALING NAME: " << h.name << "\nHealing Stats: \n" << " - Heal: "<< h.healvalue << "\n - Energy Boost: " << h.energyboost << "\n-----------------\n";
        }
}

// Funcion para crear y asignar valores a elementos de healing objects

void funcioncreatehealingobjects()
{
    bool verif1 = false;
    bool verif2 = false;

    HealingObjects healing;

    cout << "\nLet's create a healing object!!!\n";

    cout << "\nName: " ;
    cin>> healing.name;

    while(verif1 == false)
    {
        cout << "\nAmount of healing [Min:1/Max:200]: ";
        cin>> healing.healvalue;

        if(cin.fail())
        {
            cout << "\nthat's not a valid option, please select again with a valid input.\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(),'\n');
        }
        else
        {
            if(healing.healvalue > 201)
            {
                cout<< "\nthat value is too high, insert a number within the indicated range\n";
            }
            else if(healing.healvalue < 1)
            {
                cout<< "\nthat value is too low, insert a number within the indicated range\n";
            }
            else
            {
                verif1 = true;
            }
        }
    }

    while(verif2 == false)
    {
        cout << "\nAmount of energy boost [Min:100/Max:500]: ";
        cin>> healing.energyboost;

        if(cin.fail())
        {
            cout << "\nthat's not a valid option, please select again with a valid input.\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(),'\n');
        }
        else
        {
            if(healing.energyboost > 501)
            {
                cout<< "\nthat value is too high, insert a number within the indicated range\n";
            }
            else if(healing.energyboost < 100)
            {
                cout<< "\nthat value is too low, insert a number within the indicated range\n";
            }
            else
            {
                verif2 = true;
            }
        }
    }

    HealingObjectsList.push_back(healing);

    cout << "\nHealing object was created succesfully!!!\n"; 
}

// Funcion para editar o recrear un elemento de healing objects

void funcionedithealingobjects()
{
    HealingObjects healing;
    string namehealingtodelete;

    cout << "\nLet's re create a healing object!!!\n";

    cout << "-----------------" << "\n   Healing Objects list\n" << "-----------------\n";

    for (const auto& h:HealingObjectsList)
    {
                cout << "\nHEALING OBJECT NAME: " << h.name << "\n Healing stats: \n" << " Heal: "<< h.healvalue << "\n - Energy Boost: " << h.energyboost << "\n-----------------\n";
    }

    cout << "-------------------------------------------------" << "\n   Select the healing object do you want to edit\n" << "-------------------------------------------------\n"; 

    cin >> namehealingtodelete;

    HealingObjectsList.erase(remove_if(HealingObjectsList.begin(), HealingObjectsList.end(), [namehealingtodelete] (const HealingObjects& h) { return h.name == namehealingtodelete; }), HealingObjectsList.end());

    bool verif1 = false;
    bool verif2 = false;

    cout << "\nLet's re create a healing object!!!\n";

    cout << "\nName: " ;
    cin>> healing.name;

    while(verif1 == false)
    {
        cout << "\nAmount of healing [Min:1/Max:200]: ";
        cin>> healing.healvalue;

        if(cin.fail())
        {
            cout << "\nthat's not a valid option, please select again with a valid input.\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(),'\n');
        }
        else
        {
            if(healing.healvalue > 201)
            {
                cout<< "\nthat value is too high, insert a number within the indicated range\n";
            }
            else if(healing.healvalue < 1)
            {
                cout<< "\nthat value is too low, insert a number within the indicated range\n";
            }
            else
            {
                verif1 = true;
            }
        }
    }

    while(verif2 == false)
    {
        cout << "\nAmount of energy boost [Min:100/Max:500]: ";
        cin>> healing.energyboost;

        if(cin.fail())
        {
            cout << "\nthat's not a valid option, please select again with a valid input.\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(),'\n');
        }
        else
        {
            if(healing.energyboost > 501)
            {
                cout<< "\nthat value is too high, insert a number within the indicated range\n";
            }
            else if(healing.energyboost < 100)
            {
                cout<< "\nthat value is too low, insert a number within the indicated range\n";
            }
            else
            {
                verif2 = true;
            }
        }
    }

    HealingObjectsList.push_back(healing);

    cout << "\nThe healing object was re created succesfully!!!\n"; 
}

// Funcion para eliminar elementos de healing objects

void funciondeletehealingobjects()
{
    HealingObjects healing;
    string namehealingtodelete;

    cout << "\nLet's delete a healing object!!!\n";

    cout << "-----------------" << "\n   Healing Objects list\n" << "-----------------\n";

    for (const auto& h:HealingObjectsList)
    {
                cout << "\nHEALING OBJECT NAME: " << h.name << "\nHealing stats: \n" << " - Heal: "<< h.healvalue << "\n - Energy cost: " << h.energyboost << "\n-----------------\n";
    }

    cout << "-------------------------------------------------" << "\n   Select the healing object do you want to delete\n" << "-------------------------------------------------\n"; 

    cin >> namehealingtodelete;

    HealingObjectsList.erase(remove_if(HealingObjectsList.begin(), HealingObjectsList.end(), [namehealingtodelete] (const HealingObjects& h) { return h.name == namehealingtodelete; }), HealingObjectsList.end());

    cout << "Healing object deleted successfully.\n";
}

//Funcion para ver la lista de armas

void funcionvieweapons()
{
    cout << "-----------------" << "\n   Weapons list\n" << "-----------------\n";
    for (const auto& w:Weaponslist)
    {
                cout << "\nWEAPON NAME: " << w.name << "\nweapon stats: \n" << " - Damage: "<< w.damage << "\n - Energy cost: " << w.energycost << "\n-----------------\n";
    }
}

// Funcion para crear armas

void funcioncreateweapons()
{
    bool verif1 = false;
    bool verif2 = false;

    Weapons weapon;

    cout << "\nLet's create a weapon!!!\n";

    cout << "\nName: " ;
    cin>> weapon.name;

    while(verif1 == false)
    {
        cout << "\nAmount of damage per attack [Min:1/Max:1000]: ";
        cin>> weapon.damage;

        if(cin.fail())
        {
            cout << "\nthat's not a valid option, please select again with a valid input.\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(),'\n');
        }
        else
        {
            if(weapon.damage > 1001)
            {
                cout<< "\nthat value is too high, insert a number within the indicated range\n";
            }
            else if(weapon.damage < 1)
            {
                cout<< "\nthat value is too low, insert a number within the indicated range\n";
            }
            else
            {
                verif1 = true;
            }
        }
    }

    while(verif2 == false)
    {
        cout << "\nAmount of energy cost per attack [Min:100/Max:1000]: ";
        cin>> weapon.energycost;

        if(cin.fail())
        {
            cout << "\nthat's not a valid option, please select again with a valid input.\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(),'\n');
        }
        else
        {
            if(weapon.energycost > 1001)
            {
                cout<< "\nthat value is too high, insert a number within the indicated range\n";
            }
            else if(weapon.energycost < 100)
            {
                cout<< "\nthat value is too low, insert a number within the indicated range\n";
            }
            else
            {
                verif2 = true;
            }
        }
    }

    Weaponslist.push_back(weapon);

    cout << "\nWeapon was created succesfully!!!\n"; 
}

// Funcion para editar/recrear armas 

void funcioneditweapons()
{
    Weapons weapon;
    string nameweapontodelete;

    cout << "\nLet's re create a weapon!!!\n";

    cout << "-----------------" << "\n   Weapons list\n" << "-----------------\n";

    for (const auto& w:Weaponslist)
    {
                cout << "\nWEAPON NAME: " << w.name << "\nweapon stats: \n" << " - Damage: "<< w.damage << "\n - Energy cost: " << w.energycost << "\n-----------------\n";
    }

    cout << "-------------------------------------------------" << "\n   Select the weapon do you want to edit\n" << "-------------------------------------------------\n"; 

    cin >> nameweapontodelete;

    Weaponslist.erase(remove_if(Weaponslist.begin(), Weaponslist.end(), [nameweapontodelete] (const Weapons& w) { return w.name == nameweapontodelete; }), Weaponslist.end());

    bool verif1 = false;
    bool verif2 = false;

    cout << "\nWrite the new data of the weapon!!!\n";

    cout << "\nName: " ;
    cin>> weapon.name;

    while(verif1 == false)
    {
        cout << "\nAmount of damage per attack [Min:1/Max:1000]: ";
        cin>> weapon.damage;

        if(cin.fail())
        {
            cout << "\nthat's not a valid option, please select again with a valid input.\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(),'\n');
        }
        else
        {
            if(weapon.damage > 1001)
            {
                cout<< "\nthat value is too high, insert a number within the indicated range\n";
            }
            else if(weapon.damage < 1)
            {
                cout<< "\nthat value is too low, insert a number within the indicated range\n";
            }
            else
            {
                verif1 = true;
            }
        }
    }

    while(verif2 == false)
    {
        cout << "\nAmount of energy cost per attack [Min:100/Max:1000]: ";
        cin>> weapon.energycost;

        if(cin.fail())
        {
            cout << "\nthat's not a valid option, please select again with a valid input.\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(),'\n');
        }
        else
        {
            if(weapon.energycost > 1001)
            {
                cout<< "\nthat value is too high, insert a number within the indicated range\n";
            }
            else if(weapon.energycost < 100)
            {
                cout<< "\nthat value is too low, insert a number within the indicated range\n";
            }
            else
            {
                verif2 = true;
            }
        }
    }

    Weaponslist.push_back(weapon);

    cout << "\nWeapon was re created succesfully!!!\n"; 
}

//Funcion para eleminar algun arma

void funciondeleteweapons()
{
    Weapons weapon;
    string nameweapontodelete;

    cout << "\nLet's delete a weapon!!!\n";

    cout << "-----------------" << "\n   Weapons list\n" << "-----------------\n";

    for (const auto& w:Weaponslist)
    {
                cout << "\nWEAPON NAME: " << w.name << "\nweapon stats: \n" << " - Damage: "<< w.damage << "\n - Energy cost: " << w.energycost << "\n-----------------\n";
    }

    cout << "-------------------------------------------------" << "\n   Select the weapon do you want to delete\n" << "-------------------------------------------------\n"; 

    cin >> nameweapontodelete;

    Weaponslist.erase(remove_if(Weaponslist.begin(), Weaponslist.end(), [nameweapontodelete] (const Weapons& w) { return w.name == nameweapontodelete; }), Weaponslist.end());

    cout << "Weapon deleted successfully.\n";
}

// Funcion para visualizar la lista de escenarios de batalla

void funcionviewbattlegrounds()
{
    cout << "-----------------" << "\n   Battlegrounds list\n" << "-----------------\n";

    for (const auto& b:battlegroundslist)
    {
        cout << "\nBATTLEGROUND NAME: " << b.name << "\n - Ambience debuff: " << b.debuff << "\n-----------------\n";
    }
}

//Funcion para crear un escenario de batalla

void funcioncreatebattlegrounds()
{
    bool verif1 = false;

    Battlegrounds battleground;

    cout << "\nLet's create a battleground!!!\n";

    cout << "\nName: " ;
    cin>> battleground.name;

    while(verif1 == false)
    {
        cout << "\nAmbience debuff [oxygen, heat, cold, gas, poisonous, putrid]: ";
        cin>> battleground.debuff;

        if(battleground.debuff != "oxygen" and battleground.debuff != "heat" and battleground.debuff != "cold" and battleground.debuff != "gas" and battleground.debuff != "poisonous" and battleground.debuff != "putrid")
        {
            cout<< "\nthat's not an ambience type, please select one of the indicated ones\n";
        }
        else
        {
            verif1 = true;
        }
    }

    battlegroundslist.push_back(battleground);

    cout << "\nbattleground was created succesfully!!!\n"; 
}

//Funcion para editar o recrear algun escenario de batalla

void funcioneditbattlegrounds()
{
    Battlegrounds battleground;
    string namebattlegroundtodelete;

    cout << "\nLet's re create a battleground!!!\n";

    cout << "-----------------" << "\n   Battlegrounds list\n" << "-----------------\n";

    for (const auto& b:battlegroundslist)
    {
        cout << "\nBATTLEGROUND NAME: " << b.name << "\n - Ambience debuff: " << b.debuff << "\n-----------------\n";
    }

    cout << "-----------------------------------------" << "\n   Select the battleground do you want to re create\n" << "-----------------------------------------\n"; 

    cin >> namebattlegroundtodelete;

    battlegroundslist.erase(remove_if(battlegroundslist.begin(), battlegroundslist.end(), [namebattlegroundtodelete] (const Battlegrounds& b) { return b.name == namebattlegroundtodelete; }), battlegroundslist.end());
    bool verif1 = false;

    cout << "\nInsert the new data\n";

    cout << "\nName: " ;
    cin>> battleground.name;

    while(verif1 == false)
    {
        cout << "\nAmbience debuff [oxygen, heat, cold, gas, poisonous, putrid]: ";
        cin>> battleground.debuff;

        if(battleground.debuff != "oxygen" and battleground.debuff != "heat" and battleground.debuff != "cold" and battleground.debuff != "gas" and battleground.debuff != "poisonous" and battleground.debuff != "putrid")
        {
            cout<< "\nthat's not an ambience type, please select one of the indicated ones\n";
        }
        else
        {
            verif1 = true;
        }
    }

    battlegroundslist.push_back(battleground);

    cout << "Battleground re created successfully.\n";
}

// Funcion para eliminar algun escenario de batalla

void funciondeletebattlegrounds()
{
    Battlegrounds battleground;
    string namebattlegroundtodelete;

    cout << "\nLet's delete a battleground!!!\n";

    cout << "-----------------" << "\n   Battlegrounds list\n" << "-----------------\n";

    for (const auto& b:battlegroundslist)
    {
        cout << "\nBATTLEGROUND NAME: " << b.name << "\n - Ambience debuff: " << b.debuff << "\n-----------------\n";
    }

    cout << "-----------------------------------------" << "\n   Select the battleground do you want to delete\n" << "-----------------------------------------\n"; 

    cin >> namebattlegroundtodelete;

    battlegroundslist.erase(remove_if(battlegroundslist.begin(), battlegroundslist.end(), [namebattlegroundtodelete] (const Battlegrounds& b) { return b.name == namebattlegroundtodelete; }), battlegroundslist.end());

    cout << "Battleground deleted successfully.\n";
}

// Funcion para ver razas

void funcionviewraces()
{
    cout << "-----------------" << "\n   Races list\n" << "-----------------\n";
    for (const auto& r : Raceslist)
    {
        cout << "\nRACE NAME: " << r.name << "\nRace stats: \n" << " - Life: "<< r.life << "\n - Energy: " << r.energy << "\n - Ambience debuff: " << r.ambiencedebuff << "\n-----------------\n";
    }
}

// Funcion para crear una raza 

void funcioncreateraces()
{
    bool verif1 = false;
    bool verif2 = false;
    bool verif3 = false;

    Races race;

    cout << "\nLet's create a race!!!\n";

    cout << "\nName: " ;
    cin>> race.name;

    while(verif1 == false)
    {
        cout << "\nAmount of life [Min:2/Max:1000]: ";
        cin>> race.life;

        if(cin.fail())
        {
            cout << "\nthat's not a valid option, please select again with a valid input.\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(),'\n');
        }
        else
        {
            if(race.life > 1001)
            {
                cout<< "\nthat value is too high, insert a number within the indicated range\n";
            }
            else if(race.life < 1)
            {
                cout<< "\nthat value is too low, insert a number within the indicated range\n";
            }
            else
            {
                verif1 = true;
            }
        }
    }

    while(verif2 == false)
    {
        cout << "\nAmount of energy [Min:2/Max:1000]: ";
        cin>> race.energy;

        if(cin.fail())
        {
            cout << "\nthat's not a valid option, please select again with a valid input.\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(),'\n');
        }
        else
        {
            if(race.energy > 1001)
            {
                cout<< "\nthat value is too high, insert a number within the indicated range\n";
            }
            else if(race.energy < 1)
            {
                cout<< "\nthat value is too low, insert a number within the indicated range\n";
            }
            else
            {
                verif2 = true;
            }
        }
    }

    while(verif3 == false)
    {
        cout << "\nAmbience debuff [oxygen, heat, cold, gas, poisonous, putrid]: ";
        cin>> race.ambiencedebuff;

        if(race.ambiencedebuff != "oxygen" and race.ambiencedebuff != "heat" and race.ambiencedebuff != "cold" and race.ambiencedebuff != "gas" and race.ambiencedebuff != "poisonous" and race.ambiencedebuff != "putrid")
        {
            cout<< "\nthat's not an ambience type, please select one of the indicated ones\n";
        }
        else
        {
            verif3 = true;
        }
    }

    Raceslist.push_back(race);

    cout << "\nRace was created succesfully!!!\n"; 

}

// Funcion para editar o recrear una raza

void funcioneditraces()
{
    Races race;
    string nameracetoedit;

    cout << "\nLet's re create a race!!!\n";

    cout << "-----------------" << "\n   Races list\n" << "-----------------\n";

    for (const auto& r : Raceslist)
    {
        cout << "\nRACE NAME: " << r.name << "\nRace stats: \n" << " - Life: "<< r.life << "\n - Energy: " << r.energy << "\n - Ambience debuff: " << r.ambiencedebuff << "\n-----------------\n";
    }

    cout << "-------------------------------------------------" << "\n   Select the race do you want to edit\n" << "-------------------------------------------------\n"; 

    cin >> nameracetoedit;

    Raceslist.erase(remove_if(Raceslist.begin(), Raceslist.end(), [nameracetoedit] (const Races& r) { return r.name == nameracetoedit; }), Raceslist.end());

    bool verif1 = false;
    bool verif2 = false;
    bool verif3 = false;

    cout << "\nNow put the new data for this race!!!\n";

    cout << "\nName: " ;
    cin>> race.name;

    while(verif1 == false)
    {
        cout << "\nAmount of life [Min:2/Max:1000]: ";
        cin>> race.life;

        if(cin.fail())
        {
            cout << "\nthat's not a valid option, please select again with a valid input.\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(),'\n');
        }
        else
        {
            if(race.life > 1001)
            {
                cout<< "\nthat value is too high, insert a number within the indicated range\n";
            }
            else if(race.life < 1)
            {
                cout<< "\nthat value is too low, insert a number within the indicated range\n";
            }
            else
            {
                verif1 = true;
            }
        }
    }

    while(verif2 == false)
    {
        cout << "\nAmount of energy [Min:2/Max:1000]: ";
        cin>> race.energy;

        if(cin.fail())
        {
            cout << "\nthat's not a valid option, please select again with a valid input.\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(),'\n');
        }
        else
        {
            if(race.life > 1001)
            {
                cout<< "\nthat value is too high, insert a number within the indicated range\n";
            }
            else if(race.life < 1)
            {
                cout<< "\nthat value is too low, insert a number within the indicated range\n";
            }
            else
            {
                verif2 = true;
            }
        }
    }

    while(verif3 == false)
    {
        cout << "\nAmbience debuff [oxygen, heat, cold, gas, poisonous, putrid]: ";
        cin>> race.ambiencedebuff;

        if(race.ambiencedebuff != "oxygen" and race.ambiencedebuff != "heat" and race.ambiencedebuff != "cold" and race.ambiencedebuff != "gas" and race.ambiencedebuff != "poisonous" and race.ambiencedebuff != "putrid")
        {
            cout<< "\nthat's not an ambience type, please select one of the indicated ones\n";
        }
        else
        {
            verif3 = true;
        }
    }

    Raceslist.push_back(race);

    cout << "\nRace was re created succesfully!!!\n";

}

// Funcion para eliminar alguna raza

void funciondeleteraces()
{
    Races race;
    string nameracetodelete;

    cout << "\nLet's delete a race!!!\n";

    cout << "-----------------" << "\n   Races list\n" << "-----------------\n";

    for (const auto& r : Raceslist)
    {
                cout << "\nRACE NAME: " << r.name << "\nRace stats: \n" << " - Life: "<< r.life << "\n - Energy: " << r.energy << "\n-----------------\n";
    }

    cout << "-----------------------------------------" << "\n   Select the race do you want to delete\n" << "-----------------------------------------\n"; 

    cin >> nameracetodelete;

    Raceslist.erase(remove_if(Raceslist.begin(), Raceslist.end(), [nameracetodelete] (const Races& r) { return r.name == nameracetodelete; }), Raceslist.end());

    cout << "Race deleted successfully.\n";

}

// Funcion para  entrar al sub menu de razas

void funcionraces()
{
    bool volveralmenu;
    volveralmenu = false;

    while(volveralmenu == false)
    {
        bool verificacion;
        verificacion = false;

        while(verificacion == false)
        {
            int menuvalue;
            cout << "----------------------------------------" << "\n" << " what dou you wanna do?"<< "\n" << "----------------------------------------";
            cout << "\n" << " - VIEW RACES [1]" << "\n" << "" << "\n" << " - CREATE RACE [2]" << "\n" << "" << "\n" << " - EDIT RACE [3]" << "\n" << "" << "\n" << " - DELETE RACE [4]" << "\n"<< "" << "\n" << " - RETURN TO MAIN MENU[5]" << "\n";
            cout << "\n" << "----------------------------------------" << "\n" << "    SELECT AN OPTION [FROM 1 TO 5]: " << "\n" << "----------------------------------------" << "\n";
            cin >> menuvalue;

            if(cin.fail())
            {
                cout << "\nthat's not a valid option, please select again using a number.\n";
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(),'\n');
            }
            else
            {
                if(menuvalue != 1 and menuvalue != 1 and menuvalue != 2 and menuvalue != 3 and menuvalue != 4 and menuvalue != 5)
                {
                    cout<< "\nInvalid number, select again.\n";
                }
                else
                {
                    switch (menuvalue)
                    {
                    case 1:

                        funcionviewraces();
                        verificacion = true;
                        break;

                    case 2:
                    {

                        funcioncreateraces();
                        verificacion = true;
                        break;

                    }
                    case 3:

                        funcioneditraces();
                        verificacion = true;
                        break;

                    case 4:

                        funciondeleteraces();
                        verificacion = true;
                        break;
                        
                    case 5:

                        cout<< "\nReturning to main menu.\n";
                        verificacion = true;
                        volveralmenu = true;
                        break;

                    }
                }
            }
        }
    }

}

Weapons* FindWeaponByName(const string& weaponname) 
{

    for (auto& weapon:Weaponslist) 
    {
        if (weapon.name == weaponname) 
        {
            return &weapon;
        }
    }
    return nullptr;
}

bool assignWeaponToBackpackByName(Backpack& backpack, const string& weaponname)
{
    Weapons * weapon = FindWeaponByName(weaponname);

    if (weapon)
    {
        backpack.weapon = weapon; 
        return true;
    } 
    return false;
}

HealingObjects* FindHealingObjectByName(const string& healingobjectname) 
{

    for (auto& healing:HealingObjectsList) 
    {
        if (healing.name == healingobjectname) 
        {
            return &healing;
        }
    }
    return nullptr;

}

bool assignHealingObjectToBackpackByName(Backpack& backpack, const string& healingname)
{
    HealingObjects * healing = FindHealingObjectByName(healingname);

    if (healing)
    {
        backpack.healing = healing; 
        return true;
    } 
    return false;
}

Helpobjects* FindHelpObjectByName(const string& helpobjectname) 
{

    for (auto& help:Helpobjectslist) 
    {
        if (help.name == helpobjectname) 
        {
            return &help;
        }
        
    }
    return nullptr;
}

bool assignHelpObjectToBackpackByName(Backpack& backpack, const string& helpname)
{
    Helpobjects * help = FindHelpObjectByName(helpname);

    if (help)
    {
        backpack.help = help; 
        return true;
    } 
    return false;
}

Races* FindRaceByName(const string& racename) 
{

    for (auto& race:Raceslist) 
    {
        if (race.name == racename) 
        {
            return &race;
        }

    }
    return nullptr;
}

bool assignRaceToWarriorByName(Warriors& warrior, const string& racename)
{
    Races* race = FindRaceByName(racename);

    if (race)
    {
        warrior.race = race; 
        return true;
    } 
    return false;
}

Backpack* FindBackpackByName(const string& backpackname) 
{

    for (auto& backpack:backpacklist) 
    {
        if (backpack.name == backpackname) 
        {
            return &backpack;
        }

    }
    return nullptr;
}

bool assignBackpackToWarriorByName(Warriors& warrior, const string& backpackname)
{
    Backpack* backpack = FindBackpackByName(backpackname);

    if (backpack)
    {
        warrior.backpack = backpack; 
        return true;
    } 
    return false;
}


void funcionbackpack()
{
    bool verif1 = false;
    bool verif2 = false;
    bool verif3 = false;
    bool verif4 = false;
    bool verif5 = false;

    Backpack backpack;
    Weapons weapon;
    HealingObjects healing;
    Helpobjects help;

    string object1;
    string object2;
    string object3;
    string object4;
    string object5;

    cout<< "\n----------------------------------\n"<< "\n What's on the warrior's backpack? \n" << "\n----------------------------------\n";

    while(verif1 == false)
    {

        cout<<"\n"<< "\n//Select object 1//: ";
        cin >> object1;

        if (assignWeaponToBackpackByName(backpack, object1))
        {
            cout << "\nThe weapon: " << backpack.weapon->name << " has been selected " << endl;
            verif1 = true;

        }else if(assignHealingObjectToBackpackByName(backpack, object1)) 
        {
            cout << "\nThe Healing object: " << backpack.healing->name << " has been selected " << endl;
            verif1 = true;

        }else if(assignHelpObjectToBackpackByName(backpack, object1)) 
        {
            cout << "\nThe Help object: " << backpack.help->name << " has been selected " << endl;
            verif1 = true;

        }else
        {
            cout<< "\nThat's not an existing object, please select one valid object ";
        }
    }

    while(verif2 == false)
    {

        cout<<"\n"<< "\n//Select object 2//: ";
        cin >> object2;

        if (assignWeaponToBackpackByName(backpack, object2))
        {
            cout << "\nThe weapon: " << backpack.weapon->name << " has been selected " << endl;
            verif2 = true;

        }else if(assignHealingObjectToBackpackByName(backpack, object2)) 
        {
            cout << "\nThe Healing object: " << backpack.healing->name << " has been selected " << endl;
            verif2 = true;

        }else if(assignHelpObjectToBackpackByName(backpack, object2)) 
        {
            cout << "\nThe Help object: " << backpack.help->name << " has been selected " << endl;
            verif2 = true;

        }else
        {
            cout<< "\nThat's not an existing object, please select one valid object ";
        }
    }

    while(verif3 == false)
    {

        cout<<"\n"<< "\n//Select object 3//: ";
        cin >> object3;

        if (assignWeaponToBackpackByName(backpack, object3))
        {
            cout << "\nThe weapon: " << backpack.weapon->name << " has been selected " << endl;
            verif3 = true;

        }else if(assignHealingObjectToBackpackByName(backpack, object3)) 
        {
            cout << "\nThe Healing object: " << backpack.healing->name << " has been selected " << endl;
            verif3 = true;

        }else if(assignHelpObjectToBackpackByName(backpack, object3)) 
        {
            cout << "\nThe Help object: " << backpack.help->name << " has been selected " << endl;
            verif3 = true;

        }else
        {
            cout<< "\nThat's not an existing object, please select one valid object ";
        }
    }

    while(verif4 == false)
    {

        cout<<"\n"<< "\n//Select object 4//: ";;
        cin >> object4;

        if (assignWeaponToBackpackByName(backpack, object4))
        {
            cout << "\nThe weapon: " << backpack.weapon->name << " has been selected " << endl;
            verif4 = true;

        }else if(assignHealingObjectToBackpackByName(backpack, object4)) 
        {
            cout << "\nThe Healing object: " << backpack.healing->name << " has been selected " << endl;
            verif4 = true;

        }else if(assignHelpObjectToBackpackByName(backpack, object4)) 
        {
            cout << "\nThe Help object: " << backpack.help->name << " has been selected " << endl;
            verif4 = true;

        }else
        {
            cout<< "\nThat's not an existing object, please select one valid object ";
        }
    }

    while(verif5 == false)
    {

        cout<<"\n"<< "\n//Select object 5//: ";;
        cin >> object5;

        if (assignWeaponToBackpackByName(backpack, object5))
        {
            cout << "\nThe weapon: " << backpack.weapon->name << " has been selected " << endl;
            verif5 = true;

        }else if(assignHealingObjectToBackpackByName(backpack, object5)) 
        {
            cout << "\nThe Healing object: " << backpack.healing->name << " has been selected " << endl;
            verif5 = true;

        }else if(assignHelpObjectToBackpackByName(backpack, object5)) 
        {
            cout << "\nThe Help object: " << backpack.help->name << " has been selected " << endl;
            verif5 = true;

        }else
        {
            cout<< "\nThat's not an existing object, please select one valid object ";
        }
    }


}

void funcioncharacter()
{
    bool verif1 = false;
    Warriors warrior;
    Races race;
    Backpack backpack;
    string racename;

    cout << "\nSelect de Character info: \n" << "\n---------------------------\n";

    cout << "\n- NAME: " ;
    cin>> warrior.name;

    while(verif1 == false)
    {
        cout << "\n- RACE: ";
        cin>> racename;

        if (assignRaceToWarriorByName(warrior, racename))
        {
            cout << "//The " << warrior.race->name << " race has been selected// " << endl;
            verif1 = true;
        }
        else
        {
            cout << "That's not a valid Race, try again"<<endl;
        }
    }

    backpack.name = warrior.name;
    funcionbackpack();
    backpacklist.push_back(backpack);

    assignBackpackToWarriorByName(warrior, backpack.name);

}

void funcionteam1()
{
    Warriors warrior;

    for(int i = 0; i < 3; i = i + 1)
    {
        funcioncharacter();
        Team1.push_back(warrior);
    }
}

void funcionteam2()
{
    Warriors warrior;

    for(int i = 0; i < 3; i = i + 1)
    {
        funcioncharacter();
        Team1.push_back(warrior);
    }
}


void funciongotowar()
{
    cout << "\n------------------------------------------------------------------------------------------------------------\n"<< "\nNOTE: Make sure you have already prepared everything you need to create characters!!!!!!!!\n" << "\n------------------------------------------------------------------------------------------------------------\n";
    cout << "\n-------------------------------\n"<< "\nLET'S CREATE THE FIRST TEAM: \n" << "\n-------------------------------\n";

    funcionteam1();

    cout <<"\n-------------------------------\n"<< "\nLET'S CREATE THE SECOND TEAM: \n" << "\n-------------------------------\n";;

    funcionteam2();
}
// Funcion para  entrar al sub menu de escenarios de batalla
void funcionbattlegrounds()
{
    bool volveralmenu;
    volveralmenu = false;

    while(volveralmenu == false)
    {
        bool verificacion;
        verificacion = false;

        while(verificacion == false)
        {
            int menuvalue;
            cout << "----------------------------------------" << "\n" << " What dou you want to do?"<< "\n" << "----------------------------------------";
            cout << "\n" << " - VIEW BATTLEGROUNDS [1]" << "\n" << "" << "\n" << " - CREATE A BATTLEGROUND [2]" << "\n" << "" << "\n" << " - EDIT BATTLEGROUND [3]" << "\n" << "" << "\n" << " - DELETE BATTLEGROUND [4]" << "\n"<< "" << "\n" << " - RETURN TO MAIN MENU[5]" << "\n";
            cout << "\n" << "----------------------------------------" << "\n" << "    SELECT AN OPTION [FROM 1 TO 5]: " << "\n" << "----------------------------------------" << "\n";
            cin >> menuvalue;

            if(cin.fail())
            {
                cout << "\nthat's not a valid option, please select again using a number.\n";
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(),'\n');
            }
            else
            {
                if(menuvalue != 1 and menuvalue != 1 and menuvalue != 2 and menuvalue != 3 and menuvalue != 4 and menuvalue != 5)
                {
                    cout<< "\nInvalid number, select again.\n";
                }
                else
                {
                    switch (menuvalue)
                    {
                    case 1:

                        funcionviewbattlegrounds();
                        verificacion = true;
                        break;

                    case 2:

                        funcioncreatebattlegrounds();
                        verificacion = true;
                        break;

                    case 3:

                        funcioneditbattlegrounds();
                        verificacion = true;
                        break;

                    case 4:

                        funciondeletebattlegrounds();
                        verificacion = true;
                        break;

                    case 5:

                        cout<< "\nReturning to main menu.\n";
                        verificacion = true;
                        volveralmenu = true;
                        break;

                    }
                }
            }
        }
    }

}
// Funcion para  entrar al sub menu de armas
void funcionweapons()
{
    bool volveralmenu;
    volveralmenu = false;

    while(volveralmenu == false)
    {
        bool verificacion;
        verificacion = false;

        while(verificacion == false)
        {
            int menuvalue;
            cout << "----------------------------------------" << "\n" << " What dou you want to do?"<< "\n" << "----------------------------------------";
            cout << "\n" << " - VIEW WEAPONS [1]" << "\n" << "" << "\n" << " - CREATE A WEAPON [2]" << "\n" << "" << "\n" << " - EDIT WEAPON [3]" << "\n" << "" << "\n" << " - DELETE A WEAPON [4]" << "\n"<< "" << "\n" << " - RETURN TO OBJECTS MENU[5]" << "\n";
            cout << "\n" << "----------------------------------------" << "\n" << "    SELECT AN OPTION [FROM 1 TO 5]: " << "\n" << "----------------------------------------" << "\n";
            cin >> menuvalue;

            if(cin.fail())
            {
                cout << "\nthat's not a valid option, please select again using a number.\n";
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(),'\n');
            }
            else
            {
                if(menuvalue != 1 and menuvalue != 2 and menuvalue != 3 and menuvalue != 4 and menuvalue != 5)
                {
                    cout<< "\nInvalid number, select again.\n";
                }
                else
                {
                    switch (menuvalue)
                    {
                    case 1:

                        funcionvieweapons();
                        verificacion = true;
                        break;

                    case 2:

                        funcioncreateweapons();
                        verificacion = true;
                        break;

                    case 3:

                        funcioneditweapons();
                        verificacion = true;
                        break;

                    case 4:

                        funciondeleteweapons();
                        verificacion = true;
                        break;

                    case 5:

                        cout<< "\nReturning to objects menu.\n";
                        verificacion = true;
                        volveralmenu = true;
                        break;

                    }
                }
            }
        }
    }

}
// Funcion para  entrar al sub menu del sub menu de objetos de curacion
void funcionhelpobjects()
{
    bool volveralmenu;
    volveralmenu = false;

    while(volveralmenu == false)
    {
        bool verificacion;
        verificacion = false;

        while(verificacion == false)
        {
            int menuvalue;
            cout << "----------------------------------------" << "\n" << " What dou you want to do?"<< "\n" << "----------------------------------------";
            cout << "\n" << " - VIEW HELP OBJECTS [1]" << "\n" << "" << "\n" << " - CREATE HELP OBJECT [2]" << "\n" << "" << "\n" << " - EDIT HELP OBJECT [3]" << "\n" << "" << "\n" << " - DELETE HELP OBJECT [4]" << "\n"<< "" << "\n" << " - RETURN TO OBJECTS MENU[5]" << "\n";
            cout << "\n" << "----------------------------------------" << "\n" << "    SELECT AN OPTION [FROM 1 TO 5]: " << "\n" << "----------------------------------------" << "\n";
            cin >> menuvalue;

            if(cin.fail())
            {
                cout << "\nthat's not a valid option, please select again using a number.\n";
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(),'\n');
            }
            else
            {
                if(menuvalue != 1 and menuvalue != 1 and menuvalue != 2 and menuvalue != 3 and menuvalue != 4 and menuvalue != 5)
                {
                    cout<< "\nInvalid number, select again.\n";
                }
                else
                {
                    switch (menuvalue)
                    {
                    case 1:

                        funcionviewhelpobjects();
                        verificacion = true;
                        break;

                    case 2:

                        funcioncreatehelpobjects();
                        verificacion = true;
                        break;

                    case 3:

                        funcionedithelpobjects();
                        verificacion = true;
                        break;

                    case 4:

                        funciondeletehelpobjects();
                        verificacion = true;
                        break;

                    case 5:

                        cout<< "\nReturning to objects menu.\n";
                        verificacion = true;
                        volveralmenu = true;
                        break;

                    }
                }
            }
        }
    }
}
// Funcion para  entrar al sub menu del sub menu de objetos de ayuda
void funcionhealingobjects()
{
    bool volveralmenu;
    volveralmenu = false;

    while(volveralmenu == false)
    {
        bool verificacion;
        verificacion = false;

        while(verificacion == false)
        {
            int menuvalue;
            cout << "----------------------------------------" << "\n" << " What dou you want to do?"<< "\n" << "----------------------------------------";
            cout << "\n" << " - VIEW HEALING OBJECTS [1]" << "\n" << "" << "\n" << " - CREATE HEALING OBJECT [2]" << "\n" << "" << "\n" << " - EDIT HEALING OBJECT [3]" << "\n" << "" << "\n" << " - DELETE HEALING OBJECT [4]" << "\n"<< "" << "\n" << " - RETURN TO OBJECTS MENU[5]" << "\n";
            cout << "\n" << "----------------------------------------" << "\n" << "    SELECT AN OPTION [FROM 1 TO 5]: " << "\n" << "----------------------------------------" << "\n";
            cin >> menuvalue;

            if(cin.fail())
            {
                cout << "\nthat's not a valid option, please select again using a number.\n";
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(),'\n');
            }
            else
            {
                if(menuvalue != 1 and menuvalue != 1 and menuvalue != 2 and menuvalue != 3 and menuvalue != 4 and menuvalue != 5)
                {
                    cout<< "\nInvalid number, select again.\n";
                }
                else
                {
                    switch (menuvalue)
                    {
                    case 1:

                        funcionviewhealinglobjects();
                        verificacion = true;
                        break;

                    case 2:

                        funcioncreatehealingobjects();
                        verificacion = true;
                        break;

                    case 3:

                        funcionedithealingobjects();
                        verificacion = true;
                        break;

                    case 4:

                        funciondeletehealingobjects();
                        verificacion = true;
                        break;

                    case 5:

                        cout<< "\nReturning to objects menu.\n";
                        verificacion = true;
                        volveralmenu = true;
                        break;

                    }
                }
            }
        }
    }
}
// Funcion para  entrar al sub menu de objetos
void funcionobjects()
{
    bool salir;
    salir = false;

    while(salir == false)
    {
        bool verificacion;
        verificacion = false;

        while(verificacion == false)
        {
            int menuvalue;
            cout << "----------------------------------------" << "\n" << " What dou you want to do?"<< "\n" << "----------------------------------------";
            cout << "\n" << " - WEAPONS [1]" << "\n" << "" << "\n" << " - HELP OBJECTS [2]" << "\n" << "" << "\n" << " - HEALING OBJECTS [3]" << "\n"<< "" << "\n" << " - RETURN TO MAIN MENU[4]" << "\n";
            cout << "\n" << "----------------------------------------" << "\n" << "    SELECT AN OPTION [FROM 1 TO 4]: " << "\n" << "----------------------------------------" << "\n";
            cin >> menuvalue;

            if(cin.fail())
            {
                cout << "\nthat's not a valid option, please select again using a number.\n";
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(),'\n');
            }
            else
            {
                if(menuvalue != 1 and menuvalue != 2 and menuvalue != 3 and menuvalue != 4)
                {
                    cout<< "\nInvalid number, select again.\n";
                }
                else
                {
                    switch (menuvalue)
                    {
                    case 1:

                        funcionweapons();
                        verificacion = true;
                        break;

                    case 2:

                        funcionhelpobjects();
                        verificacion = true;
                        break;

                    case 3:

                        funcionhealingobjects();
                        verificacion = true;
                        break;


                    case 4:

                        cout<< "\nReturning to main menu.\n";
                        verificacion = true;
                        salir = true;
                        break;

                    }
                }
            }
        }
    }

}
// Funcion para  entrar a la descripcion de historia y normas de juego
void funciontutorial()
{
    bool volveralmenu;
    volveralmenu = false;

    while(volveralmenu == false)
    {
        bool verificacion;
        verificacion = false;

        while(verificacion == false)
        {
            int menuvalue;
            cout << "-----------------------------------------------------------------------------------------------------------------------------";
            cout << "\n" << "In the year 3100, humanity has allied with some other alien races to achieve"<< "\n";
            cout << "\n" << "defeat the enemies, but there is a conviction that some of them are spies of the"<< "\n";
            cout << "\n" << "Andromedans and others are simply traitors, so not all humans are loyal and neither"<< "\n";
            cout << "\n" << "aliens, no one can really be sure which side each student belongs to."<< "\n";
            cout << "\n" << "Furthermore, some Andromedans are against their government and against war,"<< "\n";
            cout << "\n" << "Consequently, they are allies of humanity."<< "\n";
            cout << "\n" << "Each breed, due to the characteristics of its species, has differences depending on the"<< "\n";
            cout << "\n" << "battle area, whether in the air, space, on the Moon, on Mars, at sea or on Earth, will have"<< "\n";
            cout << "\n" << "more facilities or more difficulties, for example, humans can only fight in the air with a"<< "\n";
            cout << "\n" << "SKY jet that allows them to fly, while the Ashtar can fly without the need for a device"<< "\n";
            cout << "\n" << "some, however, the Ashtar do not support the Earth's atmosphere and need a device"<< "\n";
            cout << "\n" << "to breathe. Additionally, some races have more strength, that is, more energy."<< "\n";
            cout << "\n" << "Space is very big, new races of aliens can be added, with"<< "\n";
            cout << "\n" << "different characteristics. You can also design new accessories that restore health,"<< "\n";
            cout << "\n" << "energy, that protect like shields, or that are weapons. Weapons in the year 3100 never fail because"<< "\n";
            cout << "\n" << "that the AI that controls them avoids any error."<< "\n";
            cout << "------------------------------------------------------------------------------------------------------------------------------";
            cout << "\n" << " - RETURN TO MAIN MENU [1]" << "\n";
            cin >> menuvalue;

            if(cin.fail())
            {
                cout << "\nthat's not a valid option, please select again using a number.\n";
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(),'\n');
            }
            else
            {
                if(menuvalue != 1)
                {
                    cout<< "\nInvalid number, select again.\n";
                }
                else
                {
                    switch (menuvalue)
                    {
                    case 1:

                        cout<< "\nReturning to main menu.\n";
                        verificacion = true;
                        volveralmenu = true;
                        break;
                    
                    }
                }
            }
        }
    }
}
// Funcion principal de menu para ingresar a todo lo demas
void funcionmenu()
{
    bool salir;
    salir = false;

    while(salir == false)
    {
        bool verificacion;
        verificacion = false;

        while(verificacion == false)
        {
            int menuvalue;
            cout << "----------------------------------------" << "\n" << "  WELCOME CHIEFS, WHAT'S ON YOUR MIND?"<< "\n" << "----------------------------------------";
            cout << "\n" << " - GO TO WAR [1]" << "\n" << "" << "\n" << " - RACES [2]" << "\n" << "" << "\n" << " - BATTLEGROUNDS [3]" << "\n" << "" << "\n" << " - OBJECTS [4]" << "\n" << "" << "\n" << " - DESCRIPTION TUTORIAL [5]"<< "\n" << "" << "\n" << " - QUIT [6]" << "\n";
            cout << "\n" << "----------------------------------------" << "\n" << "    SELECT AN OPTION [FROM 1 TO 6]: " << "\n" << "----------------------------------------" << "\n";
            cin >> menuvalue;

            if(cin.fail())
            {
                
                cout << "that's not a valid option, please select again using a number.\n";
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(),'\n');
            }
            else
            {
                if(menuvalue != 1 and menuvalue != 1 and menuvalue != 2 and menuvalue != 3 and menuvalue != 4 and menuvalue != 5 and menuvalue != 6)
                {
                    cout<< "\nInvalid number, select again.\n";
                }
                else
                {
                    switch (menuvalue)
                    {
                    case 1:

                        funciongotowar();
                        verificacion = true;
                        break;

                    case 2:

                        funcionraces();
                        verificacion = true;
                        break;
                    
                    case 3:

                        funcionbattlegrounds();
                        verificacion = true;
                        break;

                    case 4:
                        
                        funcionobjects();
                        verificacion = true;
                        break;

                    case 5: 

                        funciontutorial();
                        verificacion = true;
                        break;
                    
                    case 6:
                        cout<< "\n"<<"-------------------------------------------"<< "\n";
                        cout<<"\n"<<"THANKS FOR PLAYING, SEE YOU NEXT TIME PAL"<< "\n";
                        cout<< "\n"<<"-------------------------------------------"<< "\n";
                        verificacion = true;
                        salir = true;
                        break;

                    }
                }
            }
        }
    }

}

int main()
{
    funcionmenu();     
}
