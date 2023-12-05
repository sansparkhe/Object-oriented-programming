#include <iostream>
#include <fstream>  //library is used to read from and write to files. 
#include <string>
//using namespace std;
//we have defined a class 
class MovieTicket {
private:
    std::string movieName;
    int ticketId;
    double price;
    int availableSeats;
    //these

public:
   // this is the construter
    MovieTicket(std::string n, int id, double p, int seats)
        : movieName(std::move(n)), ticketId(id), price(p), availableSeats(seats) {}
    //here we use move to tranfer the value of string n to movieName rather than copying it
    void displayMovieDetails() const 
    {
        std::cout << "Movie Name: " << movieName << "\n";
        std::cout << "Ticket ID: " << ticketId << "\n";
        std::cout << "Price: Rs." << price << "\n";
        std::cout << "Available Seats: " << availableSeats << "\n";
    }

   
    bool sellTickets(int quantity) 
    {
        if (quantity > 0 && quantity <= availableSeats) {

            std::cout << "Tickets sold successfully!\n";
            availableSeats -= quantity;
            return true;
        } else {
            std::cout << "Not enough available seats.\n";
            return false;
        }
    }

   
    void saveToFile(std::ofstream& file) const //const is used to increase the quality of function it promises not to change non-static members of the object
    {
        file << movieName << " " << ticketId << " " << price << " " << availableSeats << "\n";
    }

    
    int getAvailableSeats() const
     {
        return availableSeats;
    }
    //with discount
    double getPrice() const {
        return price*0.8;
    }
    //without discount
    double getPrice1() const {
        return price;
    }
};


MovieTicket loadFromFile(std::ifstream& file) 
{
    std::string movieName;
    int ticketId;
    double price;
    int availableSeats;

    file >> movieName >> ticketId >> price >> availableSeats;

    return MovieTicket(movieName, ticketId, price, availableSeats);
}

// Function to buy tickets
void buyTickets(MovieTicket& movie)
 {
    std::string coupon;
   int quantity;
   std::cout << "Enter the number of tickets to buy: ";
   std::cin >> quantity;
   std::cout<<"\nDO YOU HAVE COUPON CODE :";
   std::cin>>coupon;
   if(coupon=="DIS031")
   {
    if (movie.sellTickets(quantity)) {
    std::cout << "Purchase successful! Total cost: Rs" << quantity * movie.getPrice() << "\n";
} 
else
{
    std::cout << "Purchase unsuccessful. Please try again.\n";
}

   }
   else
   { 
        std::cout<<"\n YOU HAVE TO BUY TICKETS ON NORMAL PRICE";
        if (movie.sellTickets(quantity))
        {
        std::cout << "Purchase successful! Total cost: Rs" << quantity * movie.getPrice1() << "\n";
        } 
        else
        {
        std::cout << "Purchase unsuccessful. Please try again.\n";
        }
    }
    
}

int main() {
    std::ofstream outFile("movies.txt", std::ios::app);  // Open file for appending
   
    if (!outFile.is_open())
     {
        std::cerr << "Error opening the file.\n";
        return 1;
    }

    MovieTicket movie("joker", 101, 10.0, 50); //OBJECT OF CLASS MOVIE TICKET
  
    movie.saveToFile(outFile);
  
    outFile.close();
   
    std::ifstream inFile("movies.txt");
 
    if (!inFile.is_open()) {
        std::cerr << "Error opening the file.\n";
        return 1;
    }
 
    MovieTicket loadedMovie = loadFromFile(inFile);

    std::cout << "Loaded Movie Details:\n";
    loadedMovie.displayMovieDetails();
  
    buyTickets(loadedMovie);
   
    std::cout << "Updated Movie Details:\n";
    loadedMovie.displayMovieDetails();
    
    inFile.close();
    return 0;
}
