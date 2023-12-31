lab_03_assignment
class Flight:
    def init(self, flight_id, source, destination, price):
        self.flight_id = flight_id
        self.source = source
        self.destination = destination
        self.price = price

class FlightTable:
    def init(self):
        self.flights = []

    def add_flight(self, flight):
        self.flights.append(flight)

    def flights_for_city(self, city):
        return [flight for flight in self.flights if city in [flight.source, flight.destination]]

    def flights_from_city(self, city):
        return [flight for flight in self.flights if flight.source == city]

    def flights_between_cities(self, city1, city2):
        return [flight for flight in self.flights if flight.source == city1 and flight.destination == city2]

    def print_flights(self, flights):
        if not flights:
            print("No flights found.")
        else:
            print("{:<10} {:<10} {:<10} {:<10}".format("Flight ID", "From", "To", "Price"))
            for flight in flights:
                print("{:<10} {:<10} {:<10} {:<10}".format(flight.flight_id, flight.source, flight.destination, flight.price))

def main():
    flight_table = FlightTable()

    flight_table.add_flight(Flight("AI161E90", "BLR", "BOM", 5600))
    flight_table.add_flight(Flight("BR161F91", "BOM", "BBI", 6750))
    flight_table.add_flight(Flight("AI161F99", "BBI", "BLR", 8210))
    flight_table.add_flight(Flight("VS171E20", "JLR", "BBI", 5500))
    flight_table.add_flight(Flight("AS171G30", "HYD", "JLR", 4400))
    flight_table.add_flight(Flight("AI131F49", "HYD", "BOM", 3499))

    cities = {
        "BLR": "Bengaluru",
        "BOM": "Mumbai",
        "BBI": "Bhubaneswar",
        "HYD": "Hyderabad",
        "JLR": "Jabalpur",
    }

    while True:
        print("\nSearch Options:")
        print("1. Flights for a particular City")
        print("2. Flights From a city")
        print("3. Flights between two given cities")
        print("4. Quit")

        choice = input("Enter your choice: ")

        if choice == "1":
            city_code = input("Enter city code (e.g., BLR, BOM, BBI, HYD, JLR): ")
            city_name = cities.get(city_code, "Unknown")
            flights = flight_table.flights_for_city(city_code)
            print(f"Flights for {city_name}:")
            flight_table.print_flights(flights)

        elif choice == "2":
            city_code = input("Enter city code (e.g., BLR, BOM, BBI, HYD, JLR): ")
            city_name = cities.get(city_code, "Unknown")
            flights = flight_table.flights_from_city(city_code)
            print(f"Flights from {city_name}:")
            flight_table.print_flights(flights)

        elif choice == "3":
            city1_code = input("Enter source city code: ")
            city2_code = input("Enter destination city code: ")
            city1_name = cities.get(city1_code, "Unknown")
            city2_name = cities.get(city2_code, "Unknown")
            flights = flight_table.flights_between_cities(city1_code, city2_code)
            print(f"Flights from {city1_name} to {city2_name}:")
            flight_table.print_flights(flights)

        elif choice == "4":
            break

        else:
            print("Invalid choice. Please try again.")

if name == "main":
    main()
