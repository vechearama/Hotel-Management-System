"""
Hotel Management System

Author: [Vecheara Ma]
Date: [Dec 02, 2025]
Version: 2.0

Description:
    This script implements a basic hotel management system that allows users to manage rooms and bookings.
    Users can add rooms, view available rooms, add bookings and view bookings.
"""

from datetime import datetime

# ----------------------------- 
# ROOM CLASS
# -----------------------------
class Room:

    def __init__(self, room_number, room_type, price_per_night):
        self.room_number = room_number              # room_number (int): Unique identifier for the room
        self.room_type = room_type                  # room_type (str): Type of room (Single, Double, Suite)
        self.price_per_night = price_per_night      # price_per_night (float): Cost of staying in the room per night
        self.is_available = True                    # is_available (bool): Whether the room is available for booking (default is available)


# -----------------------------
# BOOKING CLASS
# -----------------------------
class Booking:
    def __init__(self, customer_name, room, check_in_date, check_out_date):
        self.customer_name = customer_name          # customer_name (str): Name of the customer making the booking
        self.room = room                            # room (Room): Room object being booked
        self.check_in_date = check_in_date          # check_in_date (datetime): Check-in date
        self.check_out_date = check_out_date        # check_out_date (datetime): Check-out date


# -----------------------------
# HOTEL MANAGEMENT SYSTEM
# -----------------------------
# Define the main HotelManagementSystem class to manage rooms and bookings
class HotelManagementSystem:
    def __init__(self):
        self.rooms = []         # List to store all Room objects
        self.bookings = []      # List to store all Booking objects


     # 1. Add Room ---------------------------------------------------
    def add_room(self):
        try:
            room_number = int(input("Enter room number: "))

            # Add Validation prompting users to only enter "Single", "Double", or "Suite"
            room_type = input("Enter room type (Single, Double, Suite): ").strip().lower()
            while room_type not in ["single", "double", "suite"]:
                print("Invalid input. Please try again.")
                room_type = input("Enter room type (Single, Double, Suite): ").strip().lower()
            price_per_night = float(input("Enter price per night: "))

            # Check for duplicate room numbers
            for room in self.rooms:
                if room.room_number == room_number:
                    print(f"Room {room_number} already exists!\n")
                    return

            # Create and store the new room
            room = Room(room_number, room_type, price_per_night)
            self.rooms.append(room)
            print("Room added successfully!\n")
        except ValueError:
            print("Invalid input. Please enter valid values.\n")

    # 2. View Rooms ---------------------------------------------------
    def view_rooms(self):
        if not self.rooms:
            print("No rooms available.\n")
            return

        print("\nList of Rooms:")
        for room in self.rooms:   # iterate through the list (self.rooms = [])
            availability = "Available" if room.is_available else "Occupied"
            print(f"Room {room.room_number}, Type: {room.room_type}, Price: {room.price_per_night}, {availability}")
        print()


     # 3. Add Booking ---------------------------------------------------
    def add_booking(self):
        self.customer_name = input("Enter customer name: ")
        try:
            room_number = int(input("Enter room number: "))
            check_in_date = input("Enter check-in date (YYYY-MM-DD): ")
            check_out_date = input("Enter check-out date (YYYY-MM-DD): ")


            # Use datetime.strptime() to validate that the input date follows the format "YYYY-MM-DD"
            # Ensure the check-out date is after the check-in date.
            check_in_date_obj = datetime.strptime(check_in_date, "%Y-%m-%d")
            check_out_date_obj = datetime.strptime(check_out_date, "%Y-%m-%d")

            if check_out_date_obj < check_in_date_obj:
                raise ValueError

        except ValueError:
            print("Invalid input. Please try again.\n")
            return

        # Debugging output to show the current state of rooms
        print("\nDebug: List of rooms:")
        for room in self.rooms:
            print(f"Room {room.room_number}, Available: {room.is_available}")

        found_room = False  # Flag to track if the room exists
        for room in self.rooms:
            if room.room_number == room_number:
                found_room = True
                if room.is_available:
                    room.is_available = False  # Mark room as booked
                    booking = Booking(self.customer_name, room, check_in_date, check_out_date) # type: ignore
                    self.bookings.append(booking)
                    print("Booking added successfully!\n")
                    return
                else:
                    print("Room is already occupied!\n")
                    return

        if not found_room:
            print(f"Error: Room {room_number} does not exist. Please add the room first.\n")


    # 4. View Bookings -------------------------------------------------
    def view_bookings(self):
        if not self.bookings:
            print("No bookings available.\n")
            return

        print("\nList of Bookings:")
        for booking in self.bookings:   # iterate through the list (self.bookings = [])
            print(f"Customer: {booking.customer_name}, Room: {booking.room.room_number}, Check-in: {booking.check_in_date}, Check-out: {booking.check_out_date}")
        print()

    # 5. ROOM MENU --------------------------------------------------------
    def room_management(self):
        while True:
            print("\nRoom Management: ")
            print("     1. Add Room")
            print("     2. View Rooms")
            print("     3. Back")
            choice = input("Enter your choice: ")

            if choice == '1':
                self.add_room()
            elif choice == '2':
                self.view_rooms()
            elif choice == '3':
                return
            else:
                print("Invalid choice. Please try again.\n")


    # 6. BOOKING MENU -----------------------------------------------------
    def booking_management(self):
        while True:
            print("\nBooking Management: ")
            print("     1. Add Booking")
            print("     2. View Bookings")
            print("     3. Back")
            choice = input("Enter your choice: ")

            if choice == '1':
                self.add_booking()
            elif choice == '2':
                self.view_bookings()
            elif choice == '3':
                return
            else:
                print("Invalid choice. Please try again.\n")

        self.add_booking()
        self.view_bookings()

        
    
    # 7. MAIN MENU -------------------------------------------------------------------
    """
    ================================================================================
    Displays the main menu and handles user navigation.
    Provides options for room management, booking management, and exiting the system.
    =================================================================================
    """
    def main_menu(self):
        while True:
            print("\nHotel Management System: ")
            print("     1. Room Management")
            print("     2. Booking Management")
            print("     3. Exit")
            choice = input("Enter your choice: ")

            if choice == '1':
                self.room_management()
            elif choice == '2':
                self.booking_management()
            elif choice == '3':
                print("Exiting system. Thank you for using our service. Goodbye!")
                break
            else:
                print("Invalid choice. Please try again.\n")

# ----------------------------- Program Entry -----------------------------
if __name__ == "__main__":
    hms = HotelManagementSystem()
    hms.main_menu()