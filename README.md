# Decentralized-Ride-sharing
Create a WEB3-based ride-sharing platform that allows drivers and passengers to connect directly, reducing fees and increasing transparency.
import uuid
from datetime import datetime

# Simulated blockchain-based storage (in reality, you would use a blockchain platform)
blockchain_ledger = []

class RideShareContract:
    def __init__(self):
        self.rides = {}  # Stores ride details
        self.transactions = {}  # Stores transaction details
    
    def create_ride(self, passenger_id, ride_details):
        ride_id = str(uuid.uuid4())
        self.rides[ride_id] = {
            "passenger_id": passenger_id,
            "ride_details": ride_details,
            "driver_id": None,
            "status": "waiting"
        }
        return ride_id
    
    def accept_ride(self, driver_id, ride_id):
        if ride_id in self.rides:
            ride = self.rides[ride_id]
            if ride["status"] == "waiting":
                ride["driver_id"] = driver_id
                ride["status"] = "accepted"
                return True
        return False
    
    def complete_ride(self, ride_id):
        if ride_id in self.rides:
            ride = self.rides[ride_id]
            if ride["status"] == "accepted":
                ride["status"] = "completed"
                # Simulate transaction record
                transaction_id = str(uuid.uuid4())
                self.transactions[transaction_id] = {
                    "ride_id": ride_id,
                    "driver_id": ride["driver_id"],
                    "passenger_id": ride["passenger_id"],
                    "timestamp": datetime.now().isoformat()
                }
                return transaction_id
        return None

# Example usage
contract = RideShareContract()

# Passenger creates a ride
ride_id = contract.create_ride(passenger_id="P001", ride_details={"from": "Location A", "to": "Location B"})

# Driver accepts the ride
contract.accept_ride(driver_id="D001", ride_id=ride_id)

# Completing the ride
transaction_id = contract.complete_ride(ride_id=ride_id)

# Display the transaction to simulate transparency
print("Transaction details:", contract.transactions[transaction_id])
